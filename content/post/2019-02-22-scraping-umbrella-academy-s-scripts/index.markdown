---
title: Scraping Umbrella Academy's scripts
author: Cécile Sauder
date: '2019-02-22'
tags:
  - rvest
topics:
  - scraping
  - umbrella academy
  - series
header: https://m.media-amazon.com/images/I/81pJBOc71wL._SS500_.jpg
---


## Why Umbrella Academy ?   

I'm a big fan of [Ellen Page](https://en.wikipedia.org/wiki/Ellen_Page) ! I really love her 😍. [Juno](https://www.imdb.com/title/tt0467406/) is one of my favorite movies, no, actually it's even my favorite movie. Besides, the soundtrack is my ⏰ 🎶.   
So I had to watch this series, and it is awesome ! (Okay, maybe I'm a little biased). I've only seen the first five episodes so far. I'm taking my time because I know I'll be super sad 😭 when I'm done with the season. I'll try not to spoil myself too much by analyzing the scripts... challenging !  

<p align="center">
![](https://tel.img.pmdstatic.net/fit/http.3A.2F.2Fprd2-bone-image.2Es3-website-eu-west-1.2Eamazonaws.2Ecom.2Ftel.2F2018.2F10.2F08.2Ffc869c14-0bff-4651-aa98-37775ce1695f.2Ejpeg/540x400/quality/80/thumbnail.jpeg)
</p>

## Scraping the scripts

To start, load the essential packages, **tidyverse** to do everything tidy, **rvest** to scrap web pages and **glue** to make tidy paste. 


```r
library(tidyverse)
library(rvest)
library(glue)
```

Then, [find a web page with the scripts of the series](http://lmgtfy.com/?q=script+umbrella+academy), and put the url in `url`.

```r
url <- 'https://www.springfieldspringfield.co.uk/episode_scripts.php?tv-show=the-umbrella-academy-2019&season=1'
```

<p align="center">
![](https://media.giphy.com/media/3fibASpOsR4s94M1v4/giphy.gif)
</p>

I played a little with [SelectorGadget](https://selectorgadget.com/) to find the class of what I wanted, `.season-episode-title` seemed a good one, so let's see what it contains :


```r
url %>%
  read_html() %>%
  html_nodes('.season-episode-title')
```

```
## {xml_nodeset (10)}
##  [1] <a href="view_episode_scripts.php?tv-show=the-umbrella-academy-2019&amp; ...
##  [2] <a href="view_episode_scripts.php?tv-show=the-umbrella-academy-2019&amp; ...
##  [3] <a href="view_episode_scripts.php?tv-show=the-umbrella-academy-2019&amp; ...
##  [4] <a href="view_episode_scripts.php?tv-show=the-umbrella-academy-2019&amp; ...
##  [5] <a href="view_episode_scripts.php?tv-show=the-umbrella-academy-2019&amp; ...
##  [6] <a href="view_episode_scripts.php?tv-show=the-umbrella-academy-2019&amp; ...
##  [7] <a href="view_episode_scripts.php?tv-show=the-umbrella-academy-2019&amp; ...
##  [8] <a href="view_episode_scripts.php?tv-show=the-umbrella-academy-2019&amp; ...
##  [9] <a href="view_episode_scripts.php?tv-show=the-umbrella-academy-2019&amp; ...
## [10] <a href="view_episode_scripts.php?tv-show=the-umbrella-academy-2019&amp; ...
```

Good, we can get episodes titles and `href` attribute gives the end the url of each episode, we just have to paste it to "https://www.springfieldspringfield.co.uk/". 


```r
#titles of the episodes
episodes_titles <- url %>%
  read_html() %>%
  html_nodes('.season-episode-title') %>%
  html_text()

#url of the episodes
episodes_urls <- url %>%
  read_html() %>%
  html_nodes('.season-episode-title') %>%
  html_attr("href") %>%
  map(~glue("https://www.springfieldspringfield.co.uk/{.}")) 
```

If you go on [the web page of the first episode for example](https://www.springfieldspringfield.co.uk/view_episode_scripts.php?tv-show=the-umbrella-academy-2019&episode=s01e01), you'll note that the script is in the class `.scrolling-script-container`. So I made a little function to get the script of an episode, then I applied it to the episodes urls list with `map`.


```r
#function to get the script of an episode
get_script <- function(url){
  url %>%
    read_html() %>%
    html_nodes(".scrolling-script-container") %>%
    html_text()
}

episodes_scripts <- episodes_urls %>%
  map(~get_script(.)) %>%
  unlist()
```

Then I put titles and scripts in a tibble.


```r
df <- tibble(episodes_titles, episodes_scripts)

saveRDS(df, "df.RDS")
```

Now we have a tidy data frame with all the scripts... 

<p align="center">
![](https://media.giphy.com/media/28FpALDPHljpalhdRa/giphy.gif)
</p>

Yes, that's all for today, tomorrow I'll analyze them, if 👶 wants it 😀
