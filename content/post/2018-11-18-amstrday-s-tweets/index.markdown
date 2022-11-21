---
title: AmstRday's tweets
author: Cécile Sauder
date: '2018-11-18'
topics:
  - Data Visualization
  - Twitter API
  - SatRdays
tags:
  - rtweet
  - tidytext
  - ggplot2
  - magick
  - tidyverse
slug: amstrdays-s-tweets
header: "post/2018-11-18-amstrday-s-tweets_files/figure-html/unnamed-chunk-9-1.png"
---

<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/plotly-binding/plotly.js"></script>
<script src="{{< blogdown/postref >}}index_files/typedarray/typedarray.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/jquery/jquery.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/crosstalk/css/crosstalk.min.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/crosstalk/js/crosstalk.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/plotly-htmlwidgets-css/plotly-htmlwidgets.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/plotly-main/plotly-latest.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>

<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />

These lines of code have been lying around in a file for more than 2 months. I wrote them after [**SatRdays Amsterdam**](https://amsterdam2018.satrdays.org/) in September.

## Packages installation

``` r
library(tidyverse)
library(rtweet)
library(knitr)
library(kableExtra)
library(ggiraph)
library(magick)
library(tidytext)
library(wordcloud)
library(widyr)
library(igraph)
library(ggraph)
library(ggmap)
library(maps)
library(plotly)
```

## Scraping the tweets

``` r
# rt_AmsteRday <- search_tweets(
#   "#AmsteRday", n = 2, include_rts = FALSE
# )
# rt <- rt_AmsteRday
# 
# vect <- c("#AmstRday", "#satRday", "#satRdays", "#satRdayAMS", "#satRdaysAMS")
# 
# for( vec in vect){
#   
#   rt_vec <- search_tweets(
#     vec, n = 18000, include_rts = FALSE
#   )
#   rt <- bind_rows(rt, rt_vec)
# }
# 
# 
# rt <- rt %>% 
#   unique()
# 
# saveRDS(rt, "conttweets.RDS")

rt <- readRDS(file = "tweets.RDS")

#problem  geocode for "nederland", find it in USA
#solution : replace all Nederland by Nederlands in the column location from rt tibble

rt$location <- str_replace_all(rt$location, "Nederland", "Nederlands")

kable(rt) %>%
  kable_styling() %>%
  scroll_box(width = "100%", height = "200px")
```

<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:200px; overflow-x: scroll; width:100%; ">

<table class="table" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
user_id
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
status_id
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
created_at
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
screen_name
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
text
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
source
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
display_text_width
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
reply_to_status_id
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
reply_to_user_id
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
reply_to_screen_name
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
is_quote
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
is_retweet
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
favorite_count
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
retweet_count
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
hashtags
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
symbols
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
urls_url
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
urls_t.co
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
urls_expanded_url
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
media_url
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
media_t.co
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
media_expanded_url
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
media_type
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
ext_media_url
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
ext_media_t.co
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
ext_media_expanded_url
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
ext_media_type
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
mentions_user_id
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
mentions_screen_name
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
lang
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
quoted_status_id
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
quoted_text
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
quoted_created_at
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
quoted_source
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
quoted_favorite_count
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
quoted_retweet_count
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
quoted_user_id
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
quoted_screen_name
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
quoted_name
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
quoted_followers_count
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
quoted_friends_count
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
quoted_statuses_count
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
quoted_location
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
quoted_description
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
quoted_verified
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
retweet_status_id
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
retweet_text
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
retweet_created_at
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
retweet_source
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
retweet_favorite_count
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
retweet_retweet_count
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
retweet_user_id
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
retweet_screen_name
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
retweet_name
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
retweet_followers_count
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
retweet_friends_count
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
retweet_statuses_count
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
retweet_location
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
retweet_description
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
retweet_verified
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
place_url
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
place_name
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
place_full_name
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
place_type
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
country
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
country_code
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
geo_coords
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
coords_coords
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
bbox_coords
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
status_url
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
name
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
location
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
description
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
url
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
protected
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
followers_count
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
friends_count
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
listed_count
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
statuses_count
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
favourites_count
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
account_created_at
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
verified
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
profile_url
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
profile_expanded_url
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
account_lang
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
profile_banner_url
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
profile_background_url
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
profile_image_url
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
1570032288
</td>
<td style="text-align:left;">
1035897619476828161
</td>
<td style="text-align:left;">
2018-09-01 14:30:13
</td>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:left;">
Guess who I finally got to meet today at \#amsteRday! https://t.co/CC5iDghizR
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
52
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amsteRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA_Y6NW4AE7AQy.jpg
</td>
<td style="text-align:left;">
https://t.co/CC5iDghizR
</td>
<td style="text-align:left;">
https://twitter.com/edwin_thoen/status/1035897619476828161/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA_Y6NW4AE7AQy.jpg
</td>
<td style="text-align:left;">
https://t.co/CC5iDghizR
</td>
<td style="text-align:left;">
https://twitter.com/edwin_thoen/status/1035897619476828161/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/edwin_thoen/status/1035897619476828161
</td>
<td style="text-align:left;">
Edwin Thoen
</td>
<td style="text-align:left;">
Leiden, The Netherlands
</td>
<td style="text-align:left;">
Data scientist \| R lover \| Mead maker \| World traveller \| Amateur cook \| Tennis player \| Coffee junkie \| Julian’s dad
</td>
<td style="text-align:left;">
https://t.co/kYJ8q5Dt8d
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
423
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
445
</td>
<td style="text-align:right;">
871
</td>
<td style="text-align:left;">
2013-07-05 08:42:33
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/kYJ8q5Dt8d
</td>
<td style="text-align:left;">
http://thats-so-random.com
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1570032288/1480363331
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1011173218433077248/RIQypB5J_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
1035801172131676162
</td>
<td style="text-align:left;">
2018-09-01 08:06:58
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
.@krlmlr talking DBI (**satRdays_org?**) \#amsteRday \#rstats https://t.co/JFbQALSQjd
</td>
<td style="text-align:left;">
Buffer
</td>
<td style="text-align:right;">
53
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
amsteRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_nrR1VsAAQSfg.jpg
</td>
<td style="text-align:left;">
https://t.co/JFbQALSQjd
</td>
<td style="text-align:left;">
https://twitter.com/dataandme/status/1035801172131676162/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_nrR1VsAAQSfg.jpg, http://pbs.twimg.com/media/Dl_nrQxUwAA7zTR.jpg, http://pbs.twimg.com/media/Dl_nrSjU8AAQ8gb.jpg, http://pbs.twimg.com/media/Dl_nrR3UcAAgfAb.jpg
</td>
<td style="text-align:left;">
https://t.co/JFbQALSQjd, https://t.co/JFbQALSQjd, https://t.co/JFbQALSQjd, https://t.co/JFbQALSQjd
</td>
<td style="text-align:left;">
https://twitter.com/dataandme/status/1035801172131676162/photo/1, https://twitter.com/dataandme/status/1035801172131676162/photo/1, https://twitter.com/dataandme/status/1035801172131676162/photo/1, https://twitter.com/dataandme/status/1035801172131676162/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3354999513 , 737390070252998656
</td>
<td style="text-align:left;">
krlmlr , satRdays_org
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/dataandme/status/1035801172131676162
</td>
<td style="text-align:left;">
Mara Averick
</td>
<td style="text-align:left;">
Massachusetts
</td>
<td style="text-align:left;">
tidyverse dev advocate (**rstudio?**) \#rstats, \#datanerd, \#civictech 💖er, 🏀 stats junkie, using \#data4good (&or 🥇 fantasy sports), lesser ½ of (**batpigandme?**) 🦇🐽
</td>
<td style="text-align:left;">
https://t.co/ZANWJjC3FT
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
28620
</td>
<td style="text-align:right;">
2916
</td>
<td style="text-align:right;">
1392
</td>
<td style="text-align:right;">
29901
</td>
<td style="text-align:right;">
76778
</td>
<td style="text-align:left;">
2015-05-03 11:44:15
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/ZANWJjC3FT
</td>
<td style="text-align:left;">
https://maraaverick.rbind.io
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3230388598/1482490217
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/812016485069680640/tKpsducS_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
68772329
</td>
<td style="text-align:left;">
1037567025189715968
</td>
<td style="text-align:left;">
2018-09-06 05:03:50
</td>
<td style="text-align:left;">
PaulFeitsma
</td>
<td style="text-align:left;">
(**cecilesauder?**) Will next \#amstRday be there daycaRe? Then I will also bring my kids and can they play together!
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
96
</td>
<td style="text-align:left;">
1037325506318925824
</td>
<td style="text-align:left;">
964088911
</td>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
964088911
</td>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/PaulFeitsma/status/1037567025189715968
</td>
<td style="text-align:left;">
Paul Feitsma
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Data Scientist
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
91
</td>
<td style="text-align:right;">
427
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
105
</td>
<td style="text-align:right;">
116
</td>
<td style="text-align:left;">
2009-08-25 18:48:32
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/705824513087270912/jrpSCU_T\_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
68772329
</td>
<td style="text-align:left;">
1036863701591240706
</td>
<td style="text-align:left;">
2018-09-04 06:29:05
</td>
<td style="text-align:left;">
PaulFeitsma
</td>
<td style="text-align:left;">
Really enjoyed the talks last weekend at \#satRDays in \#AmstRday with (**dataandme?**) (**SuzanBaert?**) (**rgiordano79?**) (**GoDataDriven?**) and more \#satRdayAMS
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
139
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
satRDays , AmstRday , satRdayAMS
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3230388598 , 931042575158513664, 120816884 , 1253544996
</td>
<td style="text-align:left;">
dataandme , SuzanBaert , rgiordano79 , GoDataDriven
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/PaulFeitsma/status/1036863701591240706
</td>
<td style="text-align:left;">
Paul Feitsma
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Data Scientist
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
91
</td>
<td style="text-align:right;">
427
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
105
</td>
<td style="text-align:right;">
116
</td>
<td style="text-align:left;">
2009-08-25 18:48:32
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/705824513087270912/jrpSCU_T\_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
964088911
</td>
<td style="text-align:left;">
1035792850607370240
</td>
<td style="text-align:left;">
2018-09-01 07:33:54
</td>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:left;">
\#amstRday \#rstats (**dataandme?**) keynote https://t.co/hu45Wkb8qk
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
36
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_gFXMWwAAl8Hu.jpg
</td>
<td style="text-align:left;">
https://t.co/hu45Wkb8qk
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035792850607370240/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_gFXMWwAAl8Hu.jpg, http://pbs.twimg.com/media/Dl_gGc_X0AADqMw.jpg
</td>
<td style="text-align:left;">
https://t.co/hu45Wkb8qk, https://t.co/hu45Wkb8qk
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035792850607370240/photo/1, https://twitter.com/cecilesauder/status/1035792850607370240/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035792850607370240
</td>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:left;">
Montpellier, France
</td>
<td style="text-align:left;">
\#rstats data scientist
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
163
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
117
</td>
<td style="text-align:right;">
383
</td>
<td style="text-align:left;">
2012-11-22 11:17:21
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
fr
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/964088911/1470756731
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/2881158206/bb964afd6af2d7beea05a5a2b9fec6af_normal.png
</td>
</tr>
<tr>
<td style="text-align:left;">
964088911
</td>
<td style="text-align:left;">
1035858851655036928
</td>
<td style="text-align:left;">
2018-09-01 11:56:10
</td>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:left;">
Thomas Hütter shows us
50 ways to show our data 💹📈📉📊 at \#AmstRday \#satRday \#rstats https://t.co/OXB6trV6EW
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
82
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
AmstRday, satRday , rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAcIPmWsAEEroD.jpg
</td>
<td style="text-align:left;">
https://t.co/OXB6trV6EW
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035858851655036928/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAcIPmWsAEEroD.jpg
</td>
<td style="text-align:left;">
https://t.co/OXB6trV6EW
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035858851655036928/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035858851655036928
</td>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:left;">
Montpellier, France
</td>
<td style="text-align:left;">
\#rstats data scientist
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
163
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
117
</td>
<td style="text-align:right;">
383
</td>
<td style="text-align:left;">
2012-11-22 11:17:21
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
fr
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/964088911/1470756731
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/2881158206/bb964afd6af2d7beea05a5a2b9fec6af_normal.png
</td>
</tr>
<tr>
<td style="text-align:left;">
964088911
</td>
<td style="text-align:left;">
1035798141315018752
</td>
<td style="text-align:left;">
2018-09-01 07:54:55
</td>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:left;">
(**krlmlr?**) talk at \#amstRday \#rstats https://t.co/L8ZPe3Ou5o
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
33
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3354999513
</td>
<td style="text-align:left;">
krlmlr
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_k6W5X4AACEEB.jpg
</td>
<td style="text-align:left;">
https://t.co/L8ZPe3Ou5o
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035798141315018752/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_k6W5X4AACEEB.jpg
</td>
<td style="text-align:left;">
https://t.co/L8ZPe3Ou5o
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035798141315018752/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3354999513
</td>
<td style="text-align:left;">
krlmlr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035798141315018752
</td>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:left;">
Montpellier, France
</td>
<td style="text-align:left;">
\#rstats data scientist
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
163
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
117
</td>
<td style="text-align:right;">
383
</td>
<td style="text-align:left;">
2012-11-22 11:17:21
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
fr
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/964088911/1470756731
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/2881158206/bb964afd6af2d7beea05a5a2b9fec6af_normal.png
</td>
</tr>
<tr>
<td style="text-align:left;">
964088911
</td>
<td style="text-align:left;">
1037325506318925824
</td>
<td style="text-align:left;">
2018-09-05 13:04:07
</td>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:left;">
Come back from \#AmstRday, \#Rbaby 👶 Lexie put her new \#RLadies sticker on her 💻 to work with mummy. https://t.co/18vuAuSRTG
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
99
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
51
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
AmstRday, Rbaby , RLadies
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmVR2sUXoAAdZnW.jpg
</td>
<td style="text-align:left;">
https://t.co/18vuAuSRTG
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1037325506318925824/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmVR2sUXoAAdZnW.jpg, http://pbs.twimg.com/media/DmVR-pCWsAA-Kqk.jpg
</td>
<td style="text-align:left;">
https://t.co/18vuAuSRTG, https://t.co/18vuAuSRTG
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1037325506318925824/photo/1, https://twitter.com/cecilesauder/status/1037325506318925824/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1037325506318925824
</td>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:left;">
Montpellier, France
</td>
<td style="text-align:left;">
\#rstats data scientist
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
163
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
117
</td>
<td style="text-align:right;">
383
</td>
<td style="text-align:left;">
2012-11-22 11:17:21
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
fr
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/964088911/1470756731
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/2881158206/bb964afd6af2d7beea05a5a2b9fec6af_normal.png
</td>
</tr>
<tr>
<td style="text-align:left;">
964088911
</td>
<td style="text-align:left;">
1035812665891930113
</td>
<td style="text-align:left;">
2018-09-01 08:52:38
</td>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:left;">
(**SuzanBaert?**) talk about
“Getting more out of \#dplyr” at \#amstRday
\#rstats https://t.co/cGdqWwTjvb
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
73
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
dplyr , amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_yH0EWsAAyfC1.jpg
</td>
<td style="text-align:left;">
https://t.co/cGdqWwTjvb
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035812665891930113/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_yH0EWsAAyfC1.jpg
</td>
<td style="text-align:left;">
https://t.co/cGdqWwTjvb
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035812665891930113/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035812665891930113
</td>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:left;">
Montpellier, France
</td>
<td style="text-align:left;">
\#rstats data scientist
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
163
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
117
</td>
<td style="text-align:right;">
383
</td>
<td style="text-align:left;">
2012-11-22 11:17:21
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
fr
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/964088911/1470756731
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/2881158206/bb964afd6af2d7beea05a5a2b9fec6af_normal.png
</td>
</tr>
<tr>
<td style="text-align:left;">
964088911
</td>
<td style="text-align:left;">
1035902940828127233
</td>
<td style="text-align:left;">
2018-09-01 14:51:21
</td>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:left;">
And last but not least… Bob Jansen 
tells us how to solve sudoku with Rcpp at \#AmstRday
\#SatRday
\#rstats https://t.co/UatXYQBcpn
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
106
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
AmstRday, SatRday , rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBEOo0W0AAv6E9.jpg
</td>
<td style="text-align:left;">
https://t.co/UatXYQBcpn
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035902940828127233/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBEOo0W0AAv6E9.jpg
</td>
<td style="text-align:left;">
https://t.co/UatXYQBcpn
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035902940828127233/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035902940828127233
</td>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:left;">
Montpellier, France
</td>
<td style="text-align:left;">
\#rstats data scientist
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
163
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
117
</td>
<td style="text-align:right;">
383
</td>
<td style="text-align:left;">
2012-11-22 11:17:21
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
fr
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/964088911/1470756731
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/2881158206/bb964afd6af2d7beea05a5a2b9fec6af_normal.png
</td>
</tr>
<tr>
<td style="text-align:left;">
964088911
</td>
<td style="text-align:left;">
1035794809913520130
</td>
<td style="text-align:left;">
2018-09-01 07:41:41
</td>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:left;">
Data science-ing by (**dataandme?**) at \#amstRday 😁 https://t.co/sN9pnMSeS1
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
46
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_h4JuXgAQDaU-.jpg
</td>
<td style="text-align:left;">
https://t.co/sN9pnMSeS1
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035794809913520130/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_h4JuXgAQDaU-.jpg
</td>
<td style="text-align:left;">
https://t.co/sN9pnMSeS1
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035794809913520130/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035794809913520130
</td>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:left;">
Montpellier, France
</td>
<td style="text-align:left;">
\#rstats data scientist
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
163
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
117
</td>
<td style="text-align:right;">
383
</td>
<td style="text-align:left;">
2012-11-22 11:17:21
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
fr
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/964088911/1470756731
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/2881158206/bb964afd6af2d7beea05a5a2b9fec6af_normal.png
</td>
</tr>
<tr>
<td style="text-align:left;">
964088911
</td>
<td style="text-align:left;">
1035884122793824256
</td>
<td style="text-align:left;">
2018-09-01 13:36:35
</td>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:left;">
(**sholderer?**) Olga talks about
Using R/ R Markdown to create individual reports at \#amstRday
\#SatRday
\#rstats
Hey (**DavidGohel?**) , it’s about your work 😁 https://t.co/ydLHzcm8xU
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
148
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
179263176
</td>
<td style="text-align:left;">
sholderer
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday, SatRday , rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAzHEFX0AAbDhz.jpg
</td>
<td style="text-align:left;">
https://t.co/ydLHzcm8xU
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035884122793824256/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAzHEFX0AAbDhz.jpg
</td>
<td style="text-align:left;">
https://t.co/ydLHzcm8xU
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035884122793824256/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
179263176, 393334207
</td>
<td style="text-align:left;">
sholderer , DavidGohel
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035884122793824256
</td>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:left;">
Montpellier, France
</td>
<td style="text-align:left;">
\#rstats data scientist
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
163
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
117
</td>
<td style="text-align:right;">
383
</td>
<td style="text-align:left;">
2012-11-22 11:17:21
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
fr
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/964088911/1470756731
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/2881158206/bb964afd6af2d7beea05a5a2b9fec6af_normal.png
</td>
</tr>
<tr>
<td style="text-align:left;">
964088911
</td>
<td style="text-align:left;">
1035825255682588672
</td>
<td style="text-align:left;">
2018-09-01 09:42:40
</td>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:left;">
Now, Dominik Krzemiński with
“Making Shiny shine even brighter” 😎☀️☀️☀️☀️ at \#amstRday \#satRday \#rstats https://t.co/FYOMsEsh05
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
103
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday, satRday , rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_9krJW0AALbs4.jpg
</td>
<td style="text-align:left;">
https://t.co/FYOMsEsh05
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035825255682588672/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_9krJW0AALbs4.jpg
</td>
<td style="text-align:left;">
https://t.co/FYOMsEsh05
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035825255682588672/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
pl
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035825255682588672
</td>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:left;">
Montpellier, France
</td>
<td style="text-align:left;">
\#rstats data scientist
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
163
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
117
</td>
<td style="text-align:right;">
383
</td>
<td style="text-align:left;">
2012-11-22 11:17:21
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
fr
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/964088911/1470756731
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/2881158206/bb964afd6af2d7beea05a5a2b9fec6af_normal.png
</td>
</tr>
<tr>
<td style="text-align:left;">
964088911
</td>
<td style="text-align:left;">
1035876718156963840
</td>
<td style="text-align:left;">
2018-09-01 13:07:09
</td>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:left;">
Rita Giordano talks about
Regulars Expressions in \#rstats 👍 at \#AmstRday
\#satRday https://t.co/N8Hb2rfJ1M
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
81
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
15
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
rstats , AmstRday, satRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAsYNKXoAE9q3z.jpg
</td>
<td style="text-align:left;">
https://t.co/N8Hb2rfJ1M
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035876718156963840/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAsYNKXoAE9q3z.jpg
</td>
<td style="text-align:left;">
https://t.co/N8Hb2rfJ1M
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035876718156963840/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035876718156963840
</td>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:left;">
Montpellier, France
</td>
<td style="text-align:left;">
\#rstats data scientist
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
163
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
117
</td>
<td style="text-align:right;">
383
</td>
<td style="text-align:left;">
2012-11-22 11:17:21
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
fr
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/964088911/1470756731
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/2881158206/bb964afd6af2d7beea05a5a2b9fec6af_normal.png
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035788707016728577
</td>
<td style="text-align:left;">
2018-09-01 07:17:26
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Our keynote (**dataandme?**) . Starting the day with ‘That’s not \[data\] science.’ \#amstRday \#rstats https://t.co/BBN8T5piKu
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
94
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_cVWCXsAA5Tw-.jpg
</td>
<td style="text-align:left;">
https://t.co/BBN8T5piKu
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035788707016728577/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_cVWCXsAA5Tw-.jpg, http://pbs.twimg.com/media/Dl_cVWEXsAAEsi5.jpg
</td>
<td style="text-align:left;">
https://t.co/BBN8T5piKu, https://t.co/BBN8T5piKu
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035788707016728577/photo/1, https://twitter.com/Janinekhuc/status/1035788707016728577/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035788707016728577
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1037089134379196416
</td>
<td style="text-align:left;">
2018-09-04 21:24:52
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Could you not join \#amstRday or would like to look up your fav speakers slides? We will soon link the slides on our website. In the meantime, some of our speakers already made their fantastic slides available. More will be added as slides are made available \#rstats
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
265
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
17
</td>
<td style="text-align:right;">
9
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1037089134379196416
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035960403694690304
</td>
<td style="text-align:left;">
2018-09-01 18:39:42
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
\#amstRday beautiful view, networking &amp; drinks https://t.co/1Z2jBrSTRd
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
49
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmB4fe-WsAAfvSt.jpg
</td>
<td style="text-align:left;">
https://t.co/1Z2jBrSTRd
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035960403694690304/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmB4fe-WsAAfvSt.jpg, http://pbs.twimg.com/media/DmB4fe-XoAE0SUy.jpg
</td>
<td style="text-align:left;">
https://t.co/1Z2jBrSTRd, https://t.co/1Z2jBrSTRd
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035960403694690304/photo/1, https://twitter.com/Janinekhuc/status/1035960403694690304/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035960403694690304
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035786194335014912
</td>
<td style="text-align:left;">
2018-09-01 07:07:27
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Kick-off to the first \#satRdays in Amsterdam! Let’s get it started! \#amstRday \#rstats (**Tesskorthout?**) https://t.co/tzc7siIi8l
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
99
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
satRdays, amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_aDD2W0AEP_1D.jpg
</td>
<td style="text-align:left;">
https://t.co/tzc7siIi8l
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035786194335014912/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_aDD2W0AEP_1D.jpg
</td>
<td style="text-align:left;">
https://t.co/tzc7siIi8l
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035786194335014912/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
106091106
</td>
<td style="text-align:left;">
Tesskorthout
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035786194335014912
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035812463793582080
</td>
<td style="text-align:left;">
2018-09-01 08:51:50
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
(**SuzanBaert?**) starting off with sharing her excitement about \#amstRday ! Get ready, she’s sharing all her \#dplyr secrets with us! ’Getting more out of dplyr‘ \#rstats https://t.co/XJGATsQqlU
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
164
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
27
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
amstRday, dplyr , rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_x71EX4AEGntb.jpg
</td>
<td style="text-align:left;">
https://t.co/XJGATsQqlU
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035812463793582080/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_x71EX4AEGntb.jpg
</td>
<td style="text-align:left;">
https://t.co/XJGATsQqlU
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035812463793582080/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035812463793582080
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035479480230440960
</td>
<td style="text-align:left;">
2018-08-31 10:48:41
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Excited to kick off the first \#satRdays in Amsterdam. Follow \#amstRday for updates over the weekend- brilliant minds coming together to learn, teach and discuss \#rstats https://t.co/19lOvaxhD9
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
169
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
12
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
satRdays, amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/tweet_video_thumb/Dl7DF95XcAERu3X.jpg
</td>
<td style="text-align:left;">
https://t.co/19lOvaxhD9
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035479480230440960/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/tweet_video_thumb/Dl7DF95XcAERu3X.jpg
</td>
<td style="text-align:left;">
https://t.co/19lOvaxhD9
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035479480230440960/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035479480230440960
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035798618249289729
</td>
<td style="text-align:left;">
2018-09-01 07:56:49
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
(**dataandme?**) finishing off with the need for all R-users of every skill level to contribute to open source to move the \#rstats community ahead! \#amstRday \#satRdays https://t.co/6ILTDPg37T
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
161
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
rstats , amstRday, satRdays
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_lWNZX0AE-ip-.jpg
</td>
<td style="text-align:left;">
https://t.co/6ILTDPg37T
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035798618249289729/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_lWNZX0AE-ip-.jpg, http://pbs.twimg.com/media/Dl_lWNaX4AAiKo5.jpg
</td>
<td style="text-align:left;">
https://t.co/6ILTDPg37T, https://t.co/6ILTDPg37T
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035798618249289729/photo/1, https://twitter.com/Janinekhuc/status/1035798618249289729/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035798618249289729
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035509267850317826
</td>
<td style="text-align:left;">
2018-08-31 12:47:02
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Nick Jones from (**Uber?**) starting off the weekend with a \#tidyverse workshop. \#amstRday \#rstats \#satRdays https://t.co/XnHG6ouvhI
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
103
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
tidyverse, amstRday , rstats , satRdays
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl7eLz0XsAABmZ-.jpg
</td>
<td style="text-align:left;">
https://t.co/XnHG6ouvhI
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035509267850317826/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl7eLz0XsAABmZ-.jpg
</td>
<td style="text-align:left;">
https://t.co/XnHG6ouvhI
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035509267850317826/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
19103481
</td>
<td style="text-align:left;">
Uber
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035509267850317826
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035881495263674374
</td>
<td style="text-align:left;">
2018-09-01 13:26:08
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
And next up, is (**sholderer?**) showing us how to create pretty reproducible reports with \#rmarkdown in \#rstats \#amstRday https://t.co/mEQUMOpFxd
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
116
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
rmarkdown, rstats , amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAwuJLXcAAI4VM.jpg
</td>
<td style="text-align:left;">
https://t.co/mEQUMOpFxd
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035881495263674374/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAwuJLXcAAI4VM.jpg
</td>
<td style="text-align:left;">
https://t.co/mEQUMOpFxd
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035881495263674374/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
179263176
</td>
<td style="text-align:left;">
sholderer
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035881495263674374
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035863168910872576
</td>
<td style="text-align:left;">
2018-09-01 12:13:19
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Welcome (back) to Twitter! \#amstRday https://t.co/xDcOuvDUy3
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
36
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
TRUE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
twitter.com/StevenNooijen/…
</td>
<td style="text-align:left;">
https://t.co/xDcOuvDUy3
</td>
<td style="text-align:left;">
https://twitter.com/StevenNooijen/status/1035854045255294977
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
1035854045255294977
</td>
<td style="text-align:left;">
Dusted off my account especially to Tweet about \#amstRday today! Great to have about a 100 R lovers here, of which 14 awesome speakers 🎉 https://t.co/c6JXcRZWB5
</td>
<td style="text-align:left;">
2018-09-01 11:37:04
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
9
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
1354498236
</td>
<td style="text-align:left;">
StevenNooijen
</td>
<td style="text-align:left;">
Steven Nooijen
</td>
<td style="text-align:right;">
20
</td>
<td style="text-align:right;">
96
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Data and Travel enthousiast
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035863168910872576
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035813115571699713
</td>
<td style="text-align:left;">
2018-09-01 08:54:25
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Check out the full emoji featured programme for \#amstRday \#rstats https://t.co/wMFjC8GoN4
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
65
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
TRUE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
twitter.com/RMHoge/status/…
</td>
<td style="text-align:left;">
https://t.co/wMFjC8GoN4
</td>
<td style="text-align:left;">
https://twitter.com/RMHoge/status/1035550831964246022
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
1035550831964246022
</td>
<td style="text-align:left;">

Did I just tweet the entire Saturday program for \#amstRday ? 🙀

Yes! https://t.co/BfP60hVWyp
</td>
<td style="text-align:left;">
2018-08-31 15:32:12
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
220099608
</td>
<td style="text-align:left;">
RMHoge
</td>
<td style="text-align:left;">
Roel
</td>
<td style="text-align:right;">
187
</td>
<td style="text-align:right;">
812
</td>
<td style="text-align:right;">
1157
</td>
<td style="text-align:left;">
Leiden
</td>
<td style="text-align:left;">

I build silly rstats packages, data-science, https://t.co/sAKycT5zyA

Friend of DeSoto
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035813115571699713
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035868228449447937
</td>
<td style="text-align:left;">
2018-09-01 12:33:25
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Coffee time ☕️, before we continue with our ✨⚡️ lightning talks! \#amstRday \#rstats https://t.co/Ch1fgOLuqJ
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
82
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/tweet_video_thumb/DmAkponWwAEH29J.jpg
</td>
<td style="text-align:left;">
https://t.co/Ch1fgOLuqJ
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035868228449447937/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/tweet_video_thumb/DmAkponWwAEH29J.jpg
</td>
<td style="text-align:left;">
https://t.co/Ch1fgOLuqJ
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035868228449447937/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035868228449447937
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035900589136400389
</td>
<td style="text-align:left;">
2018-09-01 14:42:01
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Joe-Fai Chow (**matlabulous?**) introduces the moneyball app developed using R, Shiny and H2O AutoML \#rstats \#amstRday \#h2oai \#rshiny \#lime (**h2oai?**) https://t.co/7A7oSNfScz
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
140
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
rstats , amstRday, h2oai , rshiny , lime
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBCFeOX0AAeTFv.jpg
</td>
<td style="text-align:left;">
https://t.co/7A7oSNfScz
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035900589136400389/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBCFeOX0AAeTFv.jpg
</td>
<td style="text-align:left;">
https://t.co/7A7oSNfScz
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035900589136400389/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
296664658, 481867656
</td>
<td style="text-align:left;">
matlabulous, h2oai
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035900589136400389
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1036532028316037120
</td>
<td style="text-align:left;">
2018-09-03 08:31:08
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Thanks for joining us for a fantastic kick-off of the first \#amstRday conference! It was truly awe inspiring! https://t.co/7RYE80Gte5
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
109
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
TRUE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
twitter.com/dataandme/stat…
</td>
<td style="text-align:left;">
https://t.co/7RYE80Gte5
</td>
<td style="text-align:left;">
https://twitter.com/dataandme/status/1036526517881380864
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
1036526517881380864
</td>
<td style="text-align:left;">
💘🙏🌷 to everyone who made (**satRdays_org?**) \#AmstRday such a 💥! (**GoDataDriven?**) (**fishnets88?**) (**Janinekhuc?**) (**Tesskorthout?**) (**RConsortium?**) &amp;co 👋🇳🇱 https://t.co/zBBPZMYkpi
</td>
<td style="text-align:left;">
2018-09-03 08:09:14
</td>
<td style="text-align:left;">
Buffer
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
Mara Averick
</td>
<td style="text-align:right;">
28620
</td>
<td style="text-align:right;">
2916
</td>
<td style="text-align:right;">
29901
</td>
<td style="text-align:left;">
Massachusetts
</td>
<td style="text-align:left;">
tidyverse dev advocate (**rstudio?**) \#rstats, \#datanerd, \#civictech 💖er, 🏀 stats junkie, using \#data4good (&or 🥇 fantasy sports), lesser ½ of (**batpigandme?**) 🦇🐽
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1036532028316037120
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035518141063880704
</td>
<td style="text-align:left;">
2018-08-31 13:22:18
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Lexie, our youngest and most motivated workshop attendee \#rstats \#amstRday \#satRday https://t.co/cB9ByN03Um
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
83
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
TRUE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
rstats , amstRday, satRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
twitter.com/romain_francoi…
</td>
<td style="text-align:left;">
https://t.co/cB9ByN03Um
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1035500746974945283
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
1035500746974945283
</td>
<td style="text-align:left;">
Never too early to attend a \#satRdays \#rstats conference. \#rbaby 👶 https://t.co/gx7U8k3CVU
</td>
<td style="text-align:left;">
2018-08-31 12:13:11
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
35
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
377578645
</td>
<td style="text-align:left;">
romain_francois
</td>
<td style="text-align:left;">
Romain François 🦄
</td>
<td style="text-align:right;">
5113
</td>
<td style="text-align:right;">
336
</td>
<td style="text-align:right;">
5837
</td>
<td style="text-align:left;">
France
</td>
<td style="text-align:left;">
👨‍💻 \#rstats 📦 with the \#tidyverse team.
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035518141063880704
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035885179921940481
</td>
<td style="text-align:left;">
2018-09-01 13:40:47
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Jeroen Groot tells us about analysis of data to get insights about smart charging of electric cars. \#AmstRday \#rstats https://t.co/DLVbmWdsJO
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
117
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA0EhTWsAEMpKl.jpg
</td>
<td style="text-align:left;">
https://t.co/DLVbmWdsJO
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035885179921940481/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA0EhTWsAEMpKl.jpg
</td>
<td style="text-align:left;">
https://t.co/DLVbmWdsJO
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035885179921940481/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035885179921940481
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035896579327242241
</td>
<td style="text-align:left;">
2018-09-01 14:26:05
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Pieter Marcus discussing ‘Why you shouldn’t use ROC curves to assess the business value of your model!’ - an r package that makes it easier to communicate your ML results to non-tech people \#modelplotR \#rstats \#amstRday https://t.co/oI5oO0fAca
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
219
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
modelplotR, rstats , amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA-cKUXsAAqhzf.jpg
</td>
<td style="text-align:left;">
https://t.co/oI5oO0fAca
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035896579327242241/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA-cKUXsAAqhzf.jpg
</td>
<td style="text-align:left;">
https://t.co/oI5oO0fAca
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035896579327242241/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035896579327242241
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035825695115698176
</td>
<td style="text-align:left;">
2018-09-01 09:44:25
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Dominik Krzemiński sharing with us how to make your shiny apps shine even brighter ! \#rstats \#amstRday \#rshiny https://t.co/HCzzystHVy
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
110
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
9
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
rstats , amstRday, rshiny
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_9-NnX0AESooN.jpg
</td>
<td style="text-align:left;">
https://t.co/HCzzystHVy
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035825695115698176/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_9-NnX0AESooN.jpg, http://pbs.twimg.com/media/Dl_9-NmWsAALRCy.jpg
</td>
<td style="text-align:left;">
https://t.co/HCzzystHVy, https://t.co/HCzzystHVy
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035825695115698176/photo/1, https://twitter.com/Janinekhuc/status/1035825695115698176/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
pl
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035825695115698176
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035877994345185280
</td>
<td style="text-align:left;">
2018-09-01 13:12:14
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
2nd ⚡️-talk (**longhowlam?**) showing us how to use text2vec for fun projects \#rstats \#amstRday https://t.co/aLL9FkWMG3
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
89
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
rstats , amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAtiP3XsAAnaFO.jpg
</td>
<td style="text-align:left;">
https://t.co/aLL9FkWMG3
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035877994345185280/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAtiP3XsAAnaFO.jpg
</td>
<td style="text-align:left;">
https://t.co/aLL9FkWMG3
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035877994345185280/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
166540104
</td>
<td style="text-align:left;">
longhowlam
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035877994345185280
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035803940246441984
</td>
<td style="text-align:left;">
2018-09-01 08:17:58
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Don’t miss your chance to get some awesome stickers sponsored by (**rstudio?**) and (**LockeData?**) \#amstRday \#rstats https://t.co/E1M9ZvPKLB
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
106
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
13
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_qL_5WwAAg4-O.jpg
</td>
<td style="text-align:left;">
https://t.co/E1M9ZvPKLB
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035803940246441984/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_qL_5WwAAg4-O.jpg
</td>
<td style="text-align:left;">
https://t.co/E1M9ZvPKLB
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035803940246441984/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
235261861 , 839804970614538240
</td>
<td style="text-align:left;">
rstudio , LockeData
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035803940246441984
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035847238692597760
</td>
<td style="text-align:left;">
2018-09-01 11:10:01
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
After a great lunch, let’s continue with (**edwin_thoen?**) ‘An exploration of NSE and tidyeval’ \#rstats \#amstRday https://t.co/UuTbmgJkwS
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
108
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
rstats , amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmARkETXgAALhTA.jpg
</td>
<td style="text-align:left;">
https://t.co/UuTbmgJkwS
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035847238692597760/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmARkETXgAALhTA.jpg
</td>
<td style="text-align:left;">
https://t.co/UuTbmgJkwS
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035847238692597760/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
1570032288
</td>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035847238692597760
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035860468919881729
</td>
<td style="text-align:left;">
2018-09-01 12:02:35
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
(**DerFredo?**) showing us how to visualise data in just about 50 different ways. \#amstRday \#rstats \#ggplot https://t.co/LZhiWvYoi3
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
101
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
amstRday, rstats , ggplot
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAdl6rW0AE7JO2.jpg
</td>
<td style="text-align:left;">
https://t.co/LZhiWvYoi3
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035860468919881729/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAdl6rW0AE7JO2.jpg
</td>
<td style="text-align:left;">
https://t.co/LZhiWvYoi3
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035860468919881729/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035860468919881729
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1037078251234123776
</td>
<td style="text-align:left;">
2018-09-04 20:41:37
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Couldn’t make it to \#amstRday? Don’t worry, (**rgiordano79?**) regex slides are online! Thanks for sharing! https://t.co/qw97jfycbB
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
101
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
TRUE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
twitter.com/rgiordano79/st…
</td>
<td style="text-align:left;">
https://t.co/qw97jfycbB
</td>
<td style="text-align:left;">
https://twitter.com/rgiordano79/status/1037076620161572865
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
120816884
</td>
<td style="text-align:left;">
rgiordano79
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
1037076620161572865
</td>
<td style="text-align:left;">
The slides from my presentation about \#regex in \#rstats (**satRdays_org?**) \#amstRday are available on github: https://t.co/Lnonk4p1TA
</td>
<td style="text-align:left;">
2018-09-04 20:35:08
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
38
</td>
<td style="text-align:right;">
13
</td>
<td style="text-align:left;">
120816884
</td>
<td style="text-align:left;">
rgiordano79
</td>
<td style="text-align:left;">
Rita
</td>
<td style="text-align:right;">
121
</td>
<td style="text-align:right;">
231
</td>
<td style="text-align:right;">
211
</td>
<td style="text-align:left;">
France
</td>
<td style="text-align:left;">
Data analyst, researcher and passionate for data. Founder (**RLadiesStras?**).
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1037078251234123776
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035901881221111810
</td>
<td style="text-align:left;">
2018-09-01 14:47:09
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
The final fun⚡️talk, solving sudokus with \#rcpp by Bob Jansen! \#amstRday \#rstats https://t.co/NFR1lB2jez
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
81
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
rcpp , amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBDQpoXgAAEvQB.jpg
</td>
<td style="text-align:left;">
https://t.co/NFR1lB2jez
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035901881221111810/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBDQpoXgAAEvQB.jpg
</td>
<td style="text-align:left;">
https://t.co/NFR1lB2jez
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035901881221111810/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035901881221111810
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035861822593802240
</td>
<td style="text-align:left;">
2018-09-01 12:07:58
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Our dearly loved mtcars dataset. (**DerFredo?**) so, who actually thinks lollipop charts are cute? \#amstRday \#ggplot \#rstats https://t.co/7TrGbWcgVY
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
118
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
amstRday, ggplot , rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAe1CqW0AEHo2K.jpg
</td>
<td style="text-align:left;">
https://t.co/7TrGbWcgVY
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035861822593802240/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAe1CqW0AEHo2K.jpg
</td>
<td style="text-align:left;">
https://t.co/7TrGbWcgVY
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035861822593802240/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035861822593802240
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035798992377049090
</td>
<td style="text-align:left;">
2018-09-01 07:58:18
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Next up, (**krlmlr?**) on the most ‘Recent development in R’s database interface’ \#amstRday \#rstats https://t.co/V3TjS0Rm4o
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
94
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_lr8YXgAEa9wp.jpg
</td>
<td style="text-align:left;">
https://t.co/V3TjS0Rm4o
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035798992377049090/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_lr8YXgAEa9wp.jpg, http://pbs.twimg.com/media/Dl_lr8XXgAEsAL4.jpg
</td>
<td style="text-align:left;">
https://t.co/V3TjS0Rm4o, https://t.co/V3TjS0Rm4o
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035798992377049090/photo/1, https://twitter.com/Janinekhuc/status/1035798992377049090/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3354999513
</td>
<td style="text-align:left;">
krlmlr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035798992377049090
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
120816884
</td>
<td style="text-align:left;">
1037076620161572865
</td>
<td style="text-align:left;">
2018-09-04 20:35:08
</td>
<td style="text-align:left;">
rgiordano79
</td>
<td style="text-align:left;">
The slides from my presentation about \#regex in \#rstats (**satRdays_org?**) \#amstRday are available on github: https://t.co/Lnonk4p1TA
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
128
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
38
</td>
<td style="text-align:right;">
13
</td>
<td style="text-align:left;">
regex , rstats , amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
github.com/ritagior/Regul…
</td>
<td style="text-align:left;">
https://t.co/Lnonk4p1TA
</td>
<td style="text-align:left;">
https://github.com/ritagior/Regular-Expression-in-R/blob/master/Regular_expression_R.pdf
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
737390070252998656
</td>
<td style="text-align:left;">
satRdays_org
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/rgiordano79/status/1037076620161572865
</td>
<td style="text-align:left;">
Rita
</td>
<td style="text-align:left;">
France
</td>
<td style="text-align:left;">
Data analyst, researcher and passionate for data. Founder (**RLadiesStras?**).
</td>
<td style="text-align:left;">
https://t.co/alQHCeD7q1
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
121
</td>
<td style="text-align:right;">
231
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
211
</td>
<td style="text-align:right;">
93
</td>
<td style="text-align:left;">
2010-03-07 17:02:00
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/alQHCeD7q1
</td>
<td style="text-align:left;">
https://rasrita.wordpress.com
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme13/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/816934985806606336/EmxKWSKm_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
120816884
</td>
<td style="text-align:left;">
1036315197395357696
</td>
<td style="text-align:left;">
2018-09-02 18:09:31
</td>
<td style="text-align:left;">
rgiordano79
</td>
<td style="text-align:left;">
Going back to Strasbourg. Thanks the organiser of (**satRdays_org?**) \#amstRday (**GoDataDriven?**) and (**LockeData?**) for sponsoring the event. Very well organised! I really enjoyed!
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
9
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
737390070252998656, 1253544996 , 839804970614538240
</td>
<td style="text-align:left;">
satRdays_org, GoDataDriven, LockeData
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/rgiordano79/status/1036315197395357696
</td>
<td style="text-align:left;">
Rita
</td>
<td style="text-align:left;">
France
</td>
<td style="text-align:left;">
Data analyst, researcher and passionate for data. Founder (**RLadiesStras?**).
</td>
<td style="text-align:left;">
https://t.co/alQHCeD7q1
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
121
</td>
<td style="text-align:right;">
231
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
211
</td>
<td style="text-align:right;">
93
</td>
<td style="text-align:left;">
2010-03-07 17:02:00
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/alQHCeD7q1
</td>
<td style="text-align:left;">
https://rasrita.wordpress.com
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme13/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/816934985806606336/EmxKWSKm_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
1600995199
</td>
<td style="text-align:left;">
1037071172045824001
</td>
<td style="text-align:left;">
2018-09-04 20:13:29
</td>
<td style="text-align:left;">
paulusj8
</td>
<td style="text-align:left;">
Running (**DerFredo?**)’s code with those great hand-made lollipop-charts from last weekend’s \#AmstRday. It was fun and I learned a lot! \#rstats https://t.co/q904gpcBBY
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
138
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
AmstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmRquUiXcAUfqXf.jpg
</td>
<td style="text-align:left;">
https://t.co/q904gpcBBY
</td>
<td style="text-align:left;">
https://twitter.com/paulusj8/status/1037071172045824001/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmRquUiXcAUfqXf.jpg
</td>
<td style="text-align:left;">
https://t.co/q904gpcBBY
</td>
<td style="text-align:left;">
https://twitter.com/paulusj8/status/1037071172045824001/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/paulusj8/status/1037071172045824001
</td>
<td style="text-align:left;">
Paul van Leeuwen
</td>
<td style="text-align:left;">
Nederlands
</td>
<td style="text-align:left;">
\#rstats, bass guitar, table tennis
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
158
</td>
<td style="text-align:right;">
1360
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:right;">
665
</td>
<td style="text-align:left;">
2013-07-17 13:33:47
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1600995199/1535662992
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1035477074570407937/G2zosk99_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
1600995199
</td>
<td style="text-align:left;">
1035879384488587265
</td>
<td style="text-align:left;">
2018-09-01 13:17:45
</td>
<td style="text-align:left;">
paulusj8
</td>
<td style="text-align:left;">
.@longhowlam explaining how to predict house prices with the text2vec package. \#AmstRday https://t.co/YAErIzwsym
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
88
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAuzVWXoAAFimF.jpg
</td>
<td style="text-align:left;">
https://t.co/YAErIzwsym
</td>
<td style="text-align:left;">
https://twitter.com/paulusj8/status/1035879384488587265/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAuzVWXoAAFimF.jpg
</td>
<td style="text-align:left;">
https://t.co/YAErIzwsym
</td>
<td style="text-align:left;">
https://twitter.com/paulusj8/status/1035879384488587265/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
166540104
</td>
<td style="text-align:left;">
longhowlam
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/paulusj8/status/1035879384488587265
</td>
<td style="text-align:left;">
Paul van Leeuwen
</td>
<td style="text-align:left;">
Nederlands
</td>
<td style="text-align:left;">
\#rstats, bass guitar, table tennis
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
158
</td>
<td style="text-align:right;">
1360
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:right;">
665
</td>
<td style="text-align:left;">
2013-07-17 13:33:47
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1600995199/1535662992
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1035477074570407937/G2zosk99_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
2876078391
</td>
<td style="text-align:left;">
1036609828645490688
</td>
<td style="text-align:left;">
2018-09-03 13:40:17
</td>
<td style="text-align:left;">
S_Owla
</td>
<td style="text-align:left;">
Huge thanks to everyone involved in organising \#amstRday! I learned so much, met so many awesome \#rstats people (including many (**RLadiesAMS?**)) and had so much fun!! My first but definitely not my last (**satRdays_org?**) event!! :D
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
223
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
9
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
964839447798910976, 737390070252998656
</td>
<td style="text-align:left;">
RLadiesAMS , satRdays_org
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/S_Owla/status/1036609828645490688
</td>
<td style="text-align:left;">
Suthira Owlarn
</td>
<td style="text-align:left;">
Germany/Thailand
</td>
<td style="text-align:left;">
Hi! I’m a developmental biologist/postdoc at (**MPI_Muenster?**) and a \#bioinformatics/#rstats \#codenewbie :D
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
550
</td>
<td style="text-align:right;">
804
</td>
<td style="text-align:right;">
34
</td>
<td style="text-align:right;">
1761
</td>
<td style="text-align:right;">
13059
</td>
<td style="text-align:left;">
2014-11-14 06:58:18
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/535734330622885888/Mmp0HQqH_normal.jpeg
</td>
</tr>
<tr>
<td style="text-align:left;">
2876078391
</td>
<td style="text-align:left;">
1037009888029929473
</td>
<td style="text-align:left;">
2018-09-04 16:09:58
</td>
<td style="text-align:left;">
S_Owla
</td>
<td style="text-align:left;">
(**WeAreRLadies?**) (**JennyBryan?**) (**g3rv4?**) (**DesiNavadeh?**) (**romain_francois?**)’ and (**cecilesauder?**)’s \#rbaby was a delightful part of \#amstRday over the weekend! :D
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
100
</td>
<td style="text-align:left;">
1037006589377445888
</td>
<td style="text-align:left;">
1001511262545592320
</td>
<td style="text-align:left;">
WeAreRLadies
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
rbaby , amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
1001511262545592320, 2167059661 , 77212546 , 51159588 , 377578645 , 964088911
</td>
<td style="text-align:left;">
WeAreRLadies , JennyBryan , g3rv4 , DesiNavadeh , romain_francois, cecilesauder
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/S_Owla/status/1037009888029929473
</td>
<td style="text-align:left;">
Suthira Owlarn
</td>
<td style="text-align:left;">
Germany/Thailand
</td>
<td style="text-align:left;">
Hi! I’m a developmental biologist/postdoc at (**MPI_Muenster?**) and a \#bioinformatics/#rstats \#codenewbie :D
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
550
</td>
<td style="text-align:right;">
804
</td>
<td style="text-align:right;">
34
</td>
<td style="text-align:right;">
1761
</td>
<td style="text-align:right;">
13059
</td>
<td style="text-align:left;">
2014-11-14 06:58:18
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/535734330622885888/Mmp0HQqH_normal.jpeg
</td>
</tr>
<tr>
<td style="text-align:left;">
2876078391
</td>
<td style="text-align:left;">
1036608172365160450
</td>
<td style="text-align:left;">
2018-09-03 13:33:42
</td>
<td style="text-align:left;">
S_Owla
</td>
<td style="text-align:left;">
(**StevenNooijen?**) I hope you’ll continue to tweet between now and the next \#amstRday! :)
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
85
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
1354498236
</td>
<td style="text-align:left;">
StevenNooijen
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
1354498236
</td>
<td style="text-align:left;">
StevenNooijen
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/S_Owla/status/1036608172365160450
</td>
<td style="text-align:left;">
Suthira Owlarn
</td>
<td style="text-align:left;">
Germany/Thailand
</td>
<td style="text-align:left;">
Hi! I’m a developmental biologist/postdoc at (**MPI_Muenster?**) and a \#bioinformatics/#rstats \#codenewbie :D
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
550
</td>
<td style="text-align:right;">
804
</td>
<td style="text-align:right;">
34
</td>
<td style="text-align:right;">
1761
</td>
<td style="text-align:right;">
13059
</td>
<td style="text-align:left;">
2014-11-14 06:58:18
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/535734330622885888/Mmp0HQqH_normal.jpeg
</td>
</tr>
<tr>
<td style="text-align:left;">
296664658
</td>
<td style="text-align:left;">
1036940233235984390
</td>
<td style="text-align:left;">
2018-09-04 11:33:11
</td>
<td style="text-align:left;">
matlabulous
</td>
<td style="text-align:left;">

After \#amstRday, I am bringing the (**h2oai?**) (**IBMDataScience?**) (**Aginity?**) \#Moneyball to \#Oslo. Come and join us tomorrow ⚾️🇳🇴

\#AroundTheWorldWithH2Oai
\#AutoML \#XAI \#Shiny \#rstats https://t.co/MwcafHE6SP
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
174
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
TRUE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
amstRday , Moneyball , Oslo , AroundTheWorldWithH2Oai, AutoML , XAI , Shiny , rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
twitter.com/dmi3k/status/1…
</td>
<td style="text-align:left;">
https://t.co/MwcafHE6SP
</td>
<td style="text-align:left;">
https://twitter.com/dmi3k/status/1032527899277107201
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
481867656 , 722214536460173312, 829965721
</td>
<td style="text-align:left;">
h2oai , IBMDataScience, Aginity
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
1032527899277107201
</td>
<td style="text-align:left;">
Come and join is at \#H2Oslo with (**matlabulous?**) \#AutoML \#lime and \#shiny. Meetup on Sept 5. Few spots left!
https://t.co/r64TtzdmuG https://t.co/KHmbpTzOLT
</td>
<td style="text-align:left;">
2018-08-23 07:20:09
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
107048264
</td>
<td style="text-align:left;">
dmi3k
</td>
<td style="text-align:left;">
Deemah 🇺🇦 🇳🇴
</td>
<td style="text-align:right;">
547
</td>
<td style="text-align:right;">
411
</td>
<td style="text-align:right;">
5651
</td>
<td style="text-align:left;">
Oslo, Norway
</td>
<td style="text-align:left;">
Data Scientist in Oil & Gas, DQ coach, \#rstats-aficionado, Kaggle-addict, teacher, learner. Father of many, husband to one. “Problem well put is half-solved”
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/matlabulous/status/1036940233235984390
</td>
<td style="text-align:left;">
Jo-fai (Joe) Chow
</td>
<td style="text-align:left;">
🇬🇧🇺🇸🇭🇰
</td>
<td style="text-align:left;">
Civil Engineer turned Data Science Evangelist & Community Manager (**h2oai?**) \| GitHub: woobe \| Formerly (**DominoDataLab?**) (**virginmedia?**) \| \#AroundTheWorldWithH2Oai
</td>
<td style="text-align:left;">
https://t.co/No9aXP6IEL
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1330
</td>
<td style="text-align:right;">
693
</td>
<td style="text-align:right;">
199
</td>
<td style="text-align:right;">
1847
</td>
<td style="text-align:right;">
2552
</td>
<td style="text-align:left;">
2011-05-11 05:55:44
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/No9aXP6IEL
</td>
<td style="text-align:left;">
http://www.jofaichow.co.uk
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/296664658/1524180604
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1021046533360406528/19NnYn60_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
296664658
</td>
<td style="text-align:left;">
1036131024185511936
</td>
<td style="text-align:left;">
2018-09-02 05:57:41
</td>
<td style="text-align:left;">
matlabulous
</td>
<td style="text-align:left;">
(**RLadiesAMS?**) (**RladiesBrussels?**) (**RLadiesStras?**) (**RLadiesGlobal?**) (**Tesskorthout?**) (**TheSarahStolle?**) (**rgiordano79?**) (**cecilesauder?**) (**SuzanBaert?**) (**dataandme?**) (**Janinekhuc?**) (**IlsePit?**) \#rladies \#amstRday \#360selfie 🤳🏻😎 https://t.co/zR5hhnzuYn
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
33
</td>
<td style="text-align:left;">
1035917734100561920
</td>
<td style="text-align:left;">
964839447798910976
</td>
<td style="text-align:left;">
RLadiesAMS
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
24
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
rladies , amstRday , 360selfie
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmETqy8XsAANo6W.jpg
</td>
<td style="text-align:left;">
https://t.co/zR5hhnzuYn
</td>
<td style="text-align:left;">
https://twitter.com/matlabulous/status/1036131024185511936/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmETqy8XsAANo6W.jpg
</td>
<td style="text-align:left;">
https://t.co/zR5hhnzuYn
</td>
<td style="text-align:left;">
https://twitter.com/matlabulous/status/1036131024185511936/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
964839447798910976, 929302435876753408, 912221092500197377, 770490229769789440, 106091106 , 935995440792784900, 120816884 , 964088911 , 931042575158513664, 3230388598 , 3808635677 , 976069167295197184
</td>
<td style="text-align:left;">
RLadiesAMS , RladiesBrussels, RLadiesStras , RLadiesGlobal , Tesskorthout , TheSarahStolle , rgiordano79 , cecilesauder , SuzanBaert , dataandme , Janinekhuc , IlsePit
</td>
<td style="text-align:left;">
und
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/matlabulous/status/1036131024185511936
</td>
<td style="text-align:left;">
Jo-fai (Joe) Chow
</td>
<td style="text-align:left;">
🇬🇧🇺🇸🇭🇰
</td>
<td style="text-align:left;">
Civil Engineer turned Data Science Evangelist & Community Manager (**h2oai?**) \| GitHub: woobe \| Formerly (**DominoDataLab?**) (**virginmedia?**) \| \#AroundTheWorldWithH2Oai
</td>
<td style="text-align:left;">
https://t.co/No9aXP6IEL
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1330
</td>
<td style="text-align:right;">
693
</td>
<td style="text-align:right;">
199
</td>
<td style="text-align:right;">
1847
</td>
<td style="text-align:right;">
2552
</td>
<td style="text-align:left;">
2011-05-11 05:55:44
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/No9aXP6IEL
</td>
<td style="text-align:left;">
http://www.jofaichow.co.uk
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/296664658/1524180604
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1021046533360406528/19NnYn60_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
296664658
</td>
<td style="text-align:left;">
1035946768842862592
</td>
<td style="text-align:left;">
2018-09-01 17:45:31
</td>
<td style="text-align:left;">
matlabulous
</td>
<td style="text-align:left;">

I forgot to say a big thank you to (**satRdays_org?**) \#rstats \#amstRday especially (**fishnets88?**) &amp; (**GoDataDriven?**) for having me again. I hope you all enjoyed a short version of \#Moneyball. See you next time :)

It was also great to meet (**dataandme?**) 🎉

\#AroundTheWorldWithH2Oai
\#360Selfie https://t.co/oYb0sVATcE
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
283
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
24
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
rstats , amstRday , Moneyball , AroundTheWorldWithH2Oai, 360Selfie
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBsEadWsAElT0f.jpg
</td>
<td style="text-align:left;">
https://t.co/oYb0sVATcE
</td>
<td style="text-align:left;">
https://twitter.com/matlabulous/status/1035946768842862592/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBsEadWsAElT0f.jpg
</td>
<td style="text-align:left;">
https://t.co/oYb0sVATcE
</td>
<td style="text-align:left;">
https://twitter.com/matlabulous/status/1035946768842862592/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
737390070252998656, 326295039 , 1253544996 , 3230388598
</td>
<td style="text-align:left;">
satRdays_org, fishnets88 , GoDataDriven, dataandme
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
https://api.twitter.com/1.1/geo/id/99cdab25eddd6bce.json
</td>
<td style="text-align:left;">
Amsterdam
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
city
</td>
<td style="text-align:left;">
The Netherlands
</td>
<td style="text-align:left;">
NL
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
4.728900, 5.079207, 5.079207, 4.728900, 52.278227, 52.278227, 52.431229, 52.431229
</td>
<td style="text-align:left;">
https://twitter.com/matlabulous/status/1035946768842862592
</td>
<td style="text-align:left;">
Jo-fai (Joe) Chow
</td>
<td style="text-align:left;">
🇬🇧🇺🇸🇭🇰
</td>
<td style="text-align:left;">
Civil Engineer turned Data Science Evangelist & Community Manager (**h2oai?**) \| GitHub: woobe \| Formerly (**DominoDataLab?**) (**virginmedia?**) \| \#AroundTheWorldWithH2Oai
</td>
<td style="text-align:left;">
https://t.co/No9aXP6IEL
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1330
</td>
<td style="text-align:right;">
693
</td>
<td style="text-align:right;">
199
</td>
<td style="text-align:right;">
1847
</td>
<td style="text-align:right;">
2552
</td>
<td style="text-align:left;">
2011-05-11 05:55:44
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/No9aXP6IEL
</td>
<td style="text-align:left;">
http://www.jofaichow.co.uk
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/296664658/1524180604
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1021046533360406528/19NnYn60_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
1570032288
</td>
<td style="text-align:left;">
1035552924963885056
</td>
<td style="text-align:left;">
2018-08-31 15:40:31
</td>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:left;">
🤬😡🤬, hit by de flu right before \#amstRday. Would be so gutted to miss it. Hope I can make it by drugging-up tomorrow. Pfff… \#rstats \#fyouflu
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
142
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday, rstats , fyouflu
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/edwin_thoen/status/1035552924963885056
</td>
<td style="text-align:left;">
Edwin Thoen
</td>
<td style="text-align:left;">
Leiden, The Netherlands
</td>
<td style="text-align:left;">
Data scientist \| R lover \| Mead maker \| World traveller \| Amateur cook \| Tennis player \| Coffee junkie \| Julian’s dad
</td>
<td style="text-align:left;">
https://t.co/kYJ8q5Dt8d
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
423
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
445
</td>
<td style="text-align:right;">
871
</td>
<td style="text-align:left;">
2013-07-05 08:42:33
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/kYJ8q5Dt8d
</td>
<td style="text-align:left;">
http://thats-so-random.com
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1570032288/1480363331
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1011173218433077248/RIQypB5J_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
1570032288
</td>
<td style="text-align:left;">
1036325560434282498
</td>
<td style="text-align:left;">
2018-09-02 18:50:42
</td>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:left;">
My slides of \#amstRday are here https://t.co/Iv5OhFV0nv. Also there is a, rather lengthy, blog post on NSE here https://t.co/dat9Uc0QR7. Questions and remarks are very welcome. \#rstats
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
184
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
46
</td>
<td style="text-align:right;">
22
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
github.com/EdwinTh/satRday , edwinth.github.io/blog/nse/
</td>
<td style="text-align:left;">
https://t.co/Iv5OhFV0nv, https://t.co/dat9Uc0QR7
</td>
<td style="text-align:left;">
https://github.com/EdwinTh/satRday , https://edwinth.github.io/blog/nse/
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/edwin_thoen/status/1036325560434282498
</td>
<td style="text-align:left;">
Edwin Thoen
</td>
<td style="text-align:left;">
Leiden, The Netherlands
</td>
<td style="text-align:left;">
Data scientist \| R lover \| Mead maker \| World traveller \| Amateur cook \| Tennis player \| Coffee junkie \| Julian’s dad
</td>
<td style="text-align:left;">
https://t.co/kYJ8q5Dt8d
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
423
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
445
</td>
<td style="text-align:right;">
871
</td>
<td style="text-align:left;">
2013-07-05 08:42:33
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/kYJ8q5Dt8d
</td>
<td style="text-align:left;">
http://thats-so-random.com
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1570032288/1480363331
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1011173218433077248/RIQypB5J_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
1570032288
</td>
<td style="text-align:left;">
1036324632884850690
</td>
<td style="text-align:left;">
2018-09-02 18:47:01
</td>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:left;">
Had a fabulous day yesterday at the very first \#amstRday! Would be delighted if this became a regular thing. Many thanks to the organising committee and (**GoDataDriven?**) for the venue.
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
181
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
12
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
1253544996
</td>
<td style="text-align:left;">
GoDataDriven
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/edwin_thoen/status/1036324632884850690
</td>
<td style="text-align:left;">
Edwin Thoen
</td>
<td style="text-align:left;">
Leiden, The Netherlands
</td>
<td style="text-align:left;">
Data scientist \| R lover \| Mead maker \| World traveller \| Amateur cook \| Tennis player \| Coffee junkie \| Julian’s dad
</td>
<td style="text-align:left;">
https://t.co/kYJ8q5Dt8d
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
423
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
445
</td>
<td style="text-align:right;">
871
</td>
<td style="text-align:left;">
2013-07-05 08:42:33
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/kYJ8q5Dt8d
</td>
<td style="text-align:left;">
http://thats-so-random.com
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1570032288/1480363331
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1011173218433077248/RIQypB5J_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
1570032288
</td>
<td style="text-align:left;">
1036918880369876992
</td>
<td style="text-align:left;">
2018-09-04 10:08:20
</td>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:left;">
I thought the 10-minute lightening talks at \#amstRday were so much more informative and entertaining than the usual 5-minute versions. Just saying (**UseR2019_Conf?**) \#rstats
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
169
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
880766885544902656
</td>
<td style="text-align:left;">
UseR2019_Conf
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/edwin_thoen/status/1036918880369876992
</td>
<td style="text-align:left;">
Edwin Thoen
</td>
<td style="text-align:left;">
Leiden, The Netherlands
</td>
<td style="text-align:left;">
Data scientist \| R lover \| Mead maker \| World traveller \| Amateur cook \| Tennis player \| Coffee junkie \| Julian’s dad
</td>
<td style="text-align:left;">
https://t.co/kYJ8q5Dt8d
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
423
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
445
</td>
<td style="text-align:right;">
871
</td>
<td style="text-align:left;">
2013-07-05 08:42:33
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/kYJ8q5Dt8d
</td>
<td style="text-align:left;">
http://thats-so-random.com
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1570032288/1480363331
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1011173218433077248/RIQypB5J_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
1035805380499136512
</td>
<td style="text-align:left;">
2018-09-01 08:23:41
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
Make life easier w/ dplyr/dbplyr syntax, other 📦s … \#amstRday \#amstRday \#rstats \#dplyr \#rquery 💪 (**krlmlr?**) https://t.co/NMBCWyZJo9
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
106
</td>
<td style="text-align:left;">
1035801172131676162
</td>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:left;">
amstRday, amstRday, rstats , dplyr , rquery
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_rf_0X0AEtZQ9.jpg
</td>
<td style="text-align:left;">
https://t.co/NMBCWyZJo9
</td>
<td style="text-align:left;">
https://twitter.com/dataandme/status/1035805380499136512/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_rf_0X0AEtZQ9.jpg, http://pbs.twimg.com/media/Dl_rf_zXoAQMM9X.jpg, http://pbs.twimg.com/media/Dl_rf_yX0AE0jge.jpg, http://pbs.twimg.com/media/Dl_rf_2XgAIg16N.jpg
</td>
<td style="text-align:left;">
https://t.co/NMBCWyZJo9, https://t.co/NMBCWyZJo9, https://t.co/NMBCWyZJo9, https://t.co/NMBCWyZJo9
</td>
<td style="text-align:left;">
https://twitter.com/dataandme/status/1035805380499136512/photo/1, https://twitter.com/dataandme/status/1035805380499136512/photo/1, https://twitter.com/dataandme/status/1035805380499136512/photo/1, https://twitter.com/dataandme/status/1035805380499136512/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3354999513
</td>
<td style="text-align:left;">
krlmlr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/dataandme/status/1035805380499136512
</td>
<td style="text-align:left;">
Mara Averick
</td>
<td style="text-align:left;">
Massachusetts
</td>
<td style="text-align:left;">
tidyverse dev advocate (**rstudio?**) \#rstats, \#datanerd, \#civictech 💖er, 🏀 stats junkie, using \#data4good (&or 🥇 fantasy sports), lesser ½ of (**batpigandme?**) 🦇🐽
</td>
<td style="text-align:left;">
https://t.co/ZANWJjC3FT
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
28620
</td>
<td style="text-align:right;">
2916
</td>
<td style="text-align:right;">
1392
</td>
<td style="text-align:right;">
29901
</td>
<td style="text-align:right;">
76778
</td>
<td style="text-align:left;">
2015-05-03 11:44:15
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/ZANWJjC3FT
</td>
<td style="text-align:left;">
https://maraaverick.rbind.io
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3230388598/1482490217
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/812016485069680640/tKpsducS_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
1035823353817444352
</td>
<td style="text-align:left;">
2018-09-01 09:35:06
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
So. Much. Useful. Stuffs. (**SuzanBaert?**) on scoped dplyr verbs! \#rstats \#AmstRday \#satRday (**satRdays_org?**)
📽 https://t.co/mLrNvjBaYG https://t.co/EIVqre9Gmj
</td>
<td style="text-align:left;">
Buffer
</td>
<td style="text-align:right;">
127
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
190
</td>
<td style="text-align:right;">
45
</td>
<td style="text-align:left;">
rstats , AmstRday, satRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
bit.ly/dplyr_slides
</td>
<td style="text-align:left;">
https://t.co/mLrNvjBaYG
</td>
<td style="text-align:left;">
http://bit.ly/dplyr_slides
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_72cvUYAAEX9h.jpg
</td>
<td style="text-align:left;">
https://t.co/EIVqre9Gmj
</td>
<td style="text-align:left;">
https://twitter.com/dataandme/status/1035823353817444352/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_72cvUYAAEX9h.jpg, http://pbs.twimg.com/media/Dl_72VAU8AEKPlH.jpg, http://pbs.twimg.com/media/Dl_72XIUUAAF8Cb.jpg, http://pbs.twimg.com/media/Dl_72CQVAAE-2jF.jpg
</td>
<td style="text-align:left;">
https://t.co/EIVqre9Gmj, https://t.co/EIVqre9Gmj, https://t.co/EIVqre9Gmj, https://t.co/EIVqre9Gmj
</td>
<td style="text-align:left;">
https://twitter.com/dataandme/status/1035823353817444352/photo/1, https://twitter.com/dataandme/status/1035823353817444352/photo/1, https://twitter.com/dataandme/status/1035823353817444352/photo/1, https://twitter.com/dataandme/status/1035823353817444352/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
931042575158513664, 737390070252998656
</td>
<td style="text-align:left;">
SuzanBaert , satRdays_org
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/dataandme/status/1035823353817444352
</td>
<td style="text-align:left;">
Mara Averick
</td>
<td style="text-align:left;">
Massachusetts
</td>
<td style="text-align:left;">
tidyverse dev advocate (**rstudio?**) \#rstats, \#datanerd, \#civictech 💖er, 🏀 stats junkie, using \#data4good (&or 🥇 fantasy sports), lesser ½ of (**batpigandme?**) 🦇🐽
</td>
<td style="text-align:left;">
https://t.co/ZANWJjC3FT
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
28620
</td>
<td style="text-align:right;">
2916
</td>
<td style="text-align:right;">
1392
</td>
<td style="text-align:right;">
29901
</td>
<td style="text-align:right;">
76778
</td>
<td style="text-align:left;">
2015-05-03 11:44:15
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/ZANWJjC3FT
</td>
<td style="text-align:left;">
https://maraaverick.rbind.io
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3230388598/1482490217
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/812016485069680640/tKpsducS_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
1036526517881380864
</td>
<td style="text-align:left;">
2018-09-03 08:09:14
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
💘🙏🌷 to everyone who made (**satRdays_org?**) \#AmstRday such a 💥! (**GoDataDriven?**) (**fishnets88?**) (**Janinekhuc?**) (**Tesskorthout?**) (**RConsortium?**) &amp;co 👋🇳🇱 https://t.co/zBBPZMYkpi
</td>
<td style="text-align:left;">
Buffer
</td>
<td style="text-align:right;">
136
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
AmstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmJ7X9xXcAEpX8E.jpg
</td>
<td style="text-align:left;">
https://t.co/zBBPZMYkpi
</td>
<td style="text-align:left;">
https://twitter.com/dataandme/status/1036526517881380864/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmJ7X9xXcAEpX8E.jpg, http://pbs.twimg.com/media/DmJ7X-\_XcAExrhB.jpg, http://pbs.twimg.com/media/DmJ7X-EWwAAGCRx.jpg, http://pbs.twimg.com/media/DmJ7X-jXoAAvYsV.jpg
</td>
<td style="text-align:left;">
https://t.co/zBBPZMYkpi, https://t.co/zBBPZMYkpi, https://t.co/zBBPZMYkpi, https://t.co/zBBPZMYkpi
</td>
<td style="text-align:left;">
https://twitter.com/dataandme/status/1036526517881380864/photo/1, https://twitter.com/dataandme/status/1036526517881380864/photo/1, https://twitter.com/dataandme/status/1036526517881380864/photo/1, https://twitter.com/dataandme/status/1036526517881380864/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
737390070252998656, 1253544996 , 326295039 , 3808635677 , 106091106 , 3318844765
</td>
<td style="text-align:left;">
satRdays_org, GoDataDriven, fishnets88 , Janinekhuc , Tesskorthout, RConsortium
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/dataandme/status/1036526517881380864
</td>
<td style="text-align:left;">
Mara Averick
</td>
<td style="text-align:left;">
Massachusetts
</td>
<td style="text-align:left;">
tidyverse dev advocate (**rstudio?**) \#rstats, \#datanerd, \#civictech 💖er, 🏀 stats junkie, using \#data4good (&or 🥇 fantasy sports), lesser ½ of (**batpigandme?**) 🦇🐽
</td>
<td style="text-align:left;">
https://t.co/ZANWJjC3FT
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
28620
</td>
<td style="text-align:right;">
2916
</td>
<td style="text-align:right;">
1392
</td>
<td style="text-align:right;">
29901
</td>
<td style="text-align:right;">
76778
</td>
<td style="text-align:left;">
2015-05-03 11:44:15
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/ZANWJjC3FT
</td>
<td style="text-align:left;">
https://maraaverick.rbind.io
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3230388598/1482490217
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/812016485069680640/tKpsducS_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
1035787492337876992
</td>
<td style="text-align:left;">
2018-09-01 07:12:36
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
It’s (**dataandme?**) taking the stage for the opening keynote of \#amstRday \#rstats https://t.co/aRjyltgXZ3
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
77
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_bOcgXsAMbRho.jpg
</td>
<td style="text-align:left;">
https://t.co/aRjyltgXZ3
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035787492337876992/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_bOcgXsAMbRho.jpg
</td>
<td style="text-align:left;">
https://t.co/aRjyltgXZ3
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035787492337876992/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035787492337876992
</td>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:left;">
Germany, Europe, Earth
</td>
<td style="text-align:left;">
Husband, Dad & Opa • Seasoned Data dude, author, speaker: https://t.co/AYWTmUeDYb - \#SQLPASS, \#sqlfamily, R, \#DataViz, \#SQLServer, Docker, Mac, big & small data
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
890
</td>
<td style="text-align:right;">
806
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
21768
</td>
<td style="text-align:right;">
361
</td>
<td style="text-align:left;">
2008-12-19 09:55:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
https://sqlfredo.wordpress.com
</td>
<td style="text-align:left;">
de
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/18238982/1524944979
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1020786409622433792/dTcna0WF_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
1035893418902401025
</td>
<td style="text-align:left;">
2018-09-01 14:13:31
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
Last round of lightning tasks at \#amstRday started by Rianne Schouten \#rstats https://t.co/jVOFxvs3E4
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
78
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA7kGWXsAAflW\_.jpg
</td>
<td style="text-align:left;">
https://t.co/jVOFxvs3E4
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035893418902401025/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA7kGWXsAAflW\_.jpg
</td>
<td style="text-align:left;">
https://t.co/jVOFxvs3E4
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035893418902401025/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035893418902401025
</td>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:left;">
Germany, Europe, Earth
</td>
<td style="text-align:left;">
Husband, Dad & Opa • Seasoned Data dude, author, speaker: https://t.co/AYWTmUeDYb - \#SQLPASS, \#sqlfamily, R, \#DataViz, \#SQLServer, Docker, Mac, big & small data
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
890
</td>
<td style="text-align:right;">
806
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
21768
</td>
<td style="text-align:right;">
361
</td>
<td style="text-align:left;">
2008-12-19 09:55:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
https://sqlfredo.wordpress.com
</td>
<td style="text-align:left;">
de
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/18238982/1524944979
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1020786409622433792/dTcna0WF_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
1035798764970287104
</td>
<td style="text-align:left;">
2018-09-01 07:57:24
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
Next up for his \#amstRday session on recent DBI development is (**krlmlr?**) \#rstats https://t.co/Owpj8kz3iS
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
78
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_leewW0AAI-uF.jpg
</td>
<td style="text-align:left;">
https://t.co/Owpj8kz3iS
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035798764970287104/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_leewW0AAI-uF.jpg
</td>
<td style="text-align:left;">
https://t.co/Owpj8kz3iS
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035798764970287104/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3354999513
</td>
<td style="text-align:left;">
krlmlr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035798764970287104
</td>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:left;">
Germany, Europe, Earth
</td>
<td style="text-align:left;">
Husband, Dad & Opa • Seasoned Data dude, author, speaker: https://t.co/AYWTmUeDYb - \#SQLPASS, \#sqlfamily, R, \#DataViz, \#SQLServer, Docker, Mac, big & small data
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
890
</td>
<td style="text-align:right;">
806
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
21768
</td>
<td style="text-align:right;">
361
</td>
<td style="text-align:left;">
2008-12-19 09:55:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
https://sqlfredo.wordpress.com
</td>
<td style="text-align:left;">
de
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/18238982/1524944979
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1020786409622433792/dTcna0WF_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
1035847371735883776
</td>
<td style="text-align:left;">
2018-09-01 11:10:33
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
After lunch: (**edwin_thoen?**) about NSE and tidyeval. \#amstRday \#rstats https://t.co/9cEToYsbIA
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
67
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmARsKBXcAAnG9L.jpg
</td>
<td style="text-align:left;">
https://t.co/9cEToYsbIA
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035847371735883776/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmARsKBXcAAnG9L.jpg
</td>
<td style="text-align:left;">
https://t.co/9cEToYsbIA
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035847371735883776/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
1570032288
</td>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035847371735883776
</td>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:left;">
Germany, Europe, Earth
</td>
<td style="text-align:left;">
Husband, Dad & Opa • Seasoned Data dude, author, speaker: https://t.co/AYWTmUeDYb - \#SQLPASS, \#sqlfamily, R, \#DataViz, \#SQLServer, Docker, Mac, big & small data
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
890
</td>
<td style="text-align:right;">
806
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
21768
</td>
<td style="text-align:right;">
361
</td>
<td style="text-align:left;">
2008-12-19 09:55:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
https://sqlfredo.wordpress.com
</td>
<td style="text-align:left;">
de
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/18238982/1524944979
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1020786409622433792/dTcna0WF_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
1035778405508239360
</td>
<td style="text-align:left;">
2018-09-01 06:36:30
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
Starting off for my first ever \#SatRday \#amstRday /(**satRdays_org?**) https://t.co/WR2zrJmQQe
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
64
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
SatRday , amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_S9ZtXcAAe5OM.jpg
</td>
<td style="text-align:left;">
https://t.co/WR2zrJmQQe
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035778405508239360/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_S9ZtXcAAe5OM.jpg
</td>
<td style="text-align:left;">
https://t.co/WR2zrJmQQe
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035778405508239360/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
737390070252998656
</td>
<td style="text-align:left;">
satRdays_org
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035778405508239360
</td>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:left;">
Germany, Europe, Earth
</td>
<td style="text-align:left;">
Husband, Dad & Opa • Seasoned Data dude, author, speaker: https://t.co/AYWTmUeDYb - \#SQLPASS, \#sqlfamily, R, \#DataViz, \#SQLServer, Docker, Mac, big & small data
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
890
</td>
<td style="text-align:right;">
806
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
21768
</td>
<td style="text-align:right;">
361
</td>
<td style="text-align:left;">
2008-12-19 09:55:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
https://sqlfredo.wordpress.com
</td>
<td style="text-align:left;">
de
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/18238982/1524944979
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1020786409622433792/dTcna0WF_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
1035885385249943553
</td>
<td style="text-align:left;">
2018-09-01 13:41:36
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
Dank u wel &amp; thank you to the attendees of my session „50 ways to show your data“ at \#amstRday. Slides and script are now available at https://t.co/ZlD26fpiZJ \#rstats /(**satRdays_org?**)
</td>
<td style="text-align:left;">
TweetDeck
</td>
<td style="text-align:right;">
185
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
github.com/SQLThomas/Conf…
</td>
<td style="text-align:left;">
https://t.co/ZlD26fpiZJ
</td>
<td style="text-align:left;">
https://github.com/SQLThomas/Conferences/tree/master/SatRdayAms2018
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
737390070252998656
</td>
<td style="text-align:left;">
satRdays_org
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035885385249943553
</td>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:left;">
Germany, Europe, Earth
</td>
<td style="text-align:left;">
Husband, Dad & Opa • Seasoned Data dude, author, speaker: https://t.co/AYWTmUeDYb - \#SQLPASS, \#sqlfamily, R, \#DataViz, \#SQLServer, Docker, Mac, big & small data
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
890
</td>
<td style="text-align:right;">
806
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
21768
</td>
<td style="text-align:right;">
361
</td>
<td style="text-align:left;">
2008-12-19 09:55:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
https://sqlfredo.wordpress.com
</td>
<td style="text-align:left;">
de
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/18238982/1524944979
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1020786409622433792/dTcna0WF_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
1036340205119320064
</td>
<td style="text-align:left;">
2018-09-02 19:48:53
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
Back home from a pleasant weekend in Amsterdam, big thanks go to the \#amstRday team for organizing a fantastic event and for having me as a speaker! I had a great time mingling with all of you R community members! \#rstats /(**satRdays_org?**)
</td>
<td style="text-align:left;">
TweetDeck
</td>
<td style="text-align:right;">
236
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
737390070252998656
</td>
<td style="text-align:left;">
satRdays_org
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1036340205119320064
</td>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:left;">
Germany, Europe, Earth
</td>
<td style="text-align:left;">
Husband, Dad & Opa • Seasoned Data dude, author, speaker: https://t.co/AYWTmUeDYb - \#SQLPASS, \#sqlfamily, R, \#DataViz, \#SQLServer, Docker, Mac, big & small data
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
890
</td>
<td style="text-align:right;">
806
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
21768
</td>
<td style="text-align:right;">
361
</td>
<td style="text-align:left;">
2008-12-19 09:55:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
https://sqlfredo.wordpress.com
</td>
<td style="text-align:left;">
de
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/18238982/1524944979
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1020786409622433792/dTcna0WF_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
1035807140685012992
</td>
<td style="text-align:left;">
2018-09-01 08:30:41
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
Hmm, so (**TheStephLocke?**) is almost around the corner 😀 or at least (**LockeData?**) is \#amstRday https://t.co/LTCyHKaicV
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
88
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_tF86XgAAg0-M.jpg
</td>
<td style="text-align:left;">
https://t.co/LTCyHKaicV
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035807140685012992/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_tF86XgAAg0-M.jpg
</td>
<td style="text-align:left;">
https://t.co/LTCyHKaicV
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035807140685012992/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
1420994827 , 839804970614538240
</td>
<td style="text-align:left;">
TheStephLocke, LockeData
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035807140685012992
</td>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:left;">
Germany, Europe, Earth
</td>
<td style="text-align:left;">
Husband, Dad & Opa • Seasoned Data dude, author, speaker: https://t.co/AYWTmUeDYb - \#SQLPASS, \#sqlfamily, R, \#DataViz, \#SQLServer, Docker, Mac, big & small data
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
890
</td>
<td style="text-align:right;">
806
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
21768
</td>
<td style="text-align:right;">
361
</td>
<td style="text-align:left;">
2008-12-19 09:55:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
https://sqlfredo.wordpress.com
</td>
<td style="text-align:left;">
de
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/18238982/1524944979
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1020786409622433792/dTcna0WF_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
1035812153616465927
</td>
<td style="text-align:left;">
2018-09-01 08:50:36
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
Taking \#amstRday to the next round: (**SuzanBaert?**) getting more out of dplyr. \#rstats https://t.co/msg8FTnGzv
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
82
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_xqDIXcAA3yH4.jpg
</td>
<td style="text-align:left;">
https://t.co/msg8FTnGzv
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035812153616465927/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_xqDIXcAA3yH4.jpg
</td>
<td style="text-align:left;">
https://t.co/msg8FTnGzv
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035812153616465927/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035812153616465927
</td>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:left;">
Germany, Europe, Earth
</td>
<td style="text-align:left;">
Husband, Dad & Opa • Seasoned Data dude, author, speaker: https://t.co/AYWTmUeDYb - \#SQLPASS, \#sqlfamily, R, \#DataViz, \#SQLServer, Docker, Mac, big & small data
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
890
</td>
<td style="text-align:right;">
806
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
21768
</td>
<td style="text-align:right;">
361
</td>
<td style="text-align:left;">
2008-12-19 09:55:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
https://sqlfredo.wordpress.com
</td>
<td style="text-align:left;">
de
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/18238982/1524944979
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1020786409622433792/dTcna0WF_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
1035876870204604416
</td>
<td style="text-align:left;">
2018-09-01 13:07:46
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
Full room also for (**rgiordano79?**) kicking off the lightning talks at \#amstRday \#rstats https://t.co/KXltjX68Er
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
84
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAshNpW4AEyXbm.jpg
</td>
<td style="text-align:left;">
https://t.co/KXltjX68Er
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035876870204604416/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAshNpW4AEyXbm.jpg
</td>
<td style="text-align:left;">
https://t.co/KXltjX68Er
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035876870204604416/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
120816884
</td>
<td style="text-align:left;">
rgiordano79
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035876870204604416
</td>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:left;">
Germany, Europe, Earth
</td>
<td style="text-align:left;">
Husband, Dad & Opa • Seasoned Data dude, author, speaker: https://t.co/AYWTmUeDYb - \#SQLPASS, \#sqlfamily, R, \#DataViz, \#SQLServer, Docker, Mac, big & small data
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
890
</td>
<td style="text-align:right;">
806
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
21768
</td>
<td style="text-align:right;">
361
</td>
<td style="text-align:left;">
2008-12-19 09:55:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
https://sqlfredo.wordpress.com
</td>
<td style="text-align:left;">
de
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/18238982/1524944979
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1020786409622433792/dTcna0WF_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
1035825293079060481
</td>
<td style="text-align:left;">
2018-09-01 09:42:49
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
Dominik (not on Twitter - yet) came all the way from Cardiff (not Poland 😉) to \#amstRday to make Shiny shine even more. \#rstats https://t.co/g07YOFZUB5
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
127
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_9mrGXoAAWeKh.jpg
</td>
<td style="text-align:left;">
https://t.co/g07YOFZUB5
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035825293079060481/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_9mrGXoAAWeKh.jpg
</td>
<td style="text-align:left;">
https://t.co/g07YOFZUB5
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035825293079060481/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DerFredo/status/1035825293079060481
</td>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:left;">
Germany, Europe, Earth
</td>
<td style="text-align:left;">
Husband, Dad & Opa • Seasoned Data dude, author, speaker: https://t.co/AYWTmUeDYb - \#SQLPASS, \#sqlfamily, R, \#DataViz, \#SQLServer, Docker, Mac, big & small data
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
890
</td>
<td style="text-align:right;">
806
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
21768
</td>
<td style="text-align:right;">
361
</td>
<td style="text-align:left;">
2008-12-19 09:55:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/9kCEGkQWqg
</td>
<td style="text-align:left;">
https://sqlfredo.wordpress.com
</td>
<td style="text-align:left;">
de
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/18238982/1524944979
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1020786409622433792/dTcna0WF_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
614549020
</td>
<td style="text-align:left;">
1036254285561044992
</td>
<td style="text-align:left;">
2018-09-02 14:07:29
</td>
<td style="text-align:left;">
veerlevanson
</td>
<td style="text-align:left;">
I received my first hex sticker yesterday! \#amstRday \#rladies https://t.co/tDrfI6CXBI
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
61
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
22
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
amstRday, rladies
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmGDw6-X4AA7w-k.jpg
</td>
<td style="text-align:left;">
https://t.co/tDrfI6CXBI
</td>
<td style="text-align:left;">
https://twitter.com/veerlevanson/status/1036254285561044992/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmGDw6-X4AA7w-k.jpg
</td>
<td style="text-align:left;">
https://t.co/tDrfI6CXBI
</td>
<td style="text-align:left;">
https://twitter.com/veerlevanson/status/1036254285561044992/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/veerlevanson/status/1036254285561044992
</td>
<td style="text-align:left;">
Veerle van Son
</td>
<td style="text-align:left;">
’s-Hertogenbosch, Nederlands
</td>
<td style="text-align:left;">
I ❤️ Data Science
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
82
</td>
<td style="text-align:right;">
139
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
62
</td>
<td style="text-align:right;">
563
</td>
<td style="text-align:left;">
2012-06-21 20:20:16
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/998990196669493250/pc6hKizY_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
119444092
</td>
<td style="text-align:left;">
1036228035765317632
</td>
<td style="text-align:left;">
2018-09-02 12:23:10
</td>
<td style="text-align:left;">
HoogvlietsR
</td>
<td style="text-align:left;">

(**matlabulous?**) (**dataandme?**) (**satRdays_org?**) (**fishnets88?**) (**GoDataDriven?**) Oh no, can’t believe I missed this, right in my own city 😑.

Looks really great! Where do I sign up for the next one? \#AmstRday
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
128
</td>
<td style="text-align:left;">
1035946768842862592
</td>
<td style="text-align:left;">
296664658
</td>
<td style="text-align:left;">
matlabulous
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
296664658 , 3230388598 , 737390070252998656, 326295039 , 1253544996
</td>
<td style="text-align:left;">
matlabulous , dataandme , satRdays_org, fishnets88 , GoDataDriven
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/HoogvlietsR/status/1036228035765317632
</td>
<td style="text-align:left;">
Raphaël Hoogvliets
</td>
<td style="text-align:left;">
Nederlands
</td>
<td style="text-align:left;">
Data Scientist • Agrifood Expert • (**KPNconsulting?**) • NBA fan
</td>
<td style="text-align:left;">
https://t.co/T3lfxzMM0M
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1028
</td>
<td style="text-align:right;">
376
</td>
<td style="text-align:right;">
55
</td>
<td style="text-align:right;">
4754
</td>
<td style="text-align:right;">
1682
</td>
<td style="text-align:left;">
2010-03-03 17:32:31
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/T3lfxzMM0M
</td>
<td style="text-align:left;">
http://www.raphaelhoogvliets.nl
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/119444092/1393421645
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme14/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/792312375407968256/1BXInKJf_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
377578645
</td>
<td style="text-align:left;">
1036176209959366657
</td>
<td style="text-align:left;">
2018-09-02 08:57:14
</td>
<td style="text-align:left;">
romain_francois
</td>
<td style="text-align:left;">
Open source day after \#amstRday. regex and cheatsheets. https://t.co/kmXpuPnhfa
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
55
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
27
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmE8xA-WwAAO3T8.jpg
</td>
<td style="text-align:left;">
https://t.co/kmXpuPnhfa
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1036176209959366657/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmE8xA-WwAAO3T8.jpg, http://pbs.twimg.com/media/DmE8xA_X4AApFsU.jpg
</td>
<td style="text-align:left;">
https://t.co/kmXpuPnhfa, https://t.co/kmXpuPnhfa
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1036176209959366657/photo/1, https://twitter.com/romain_francois/status/1036176209959366657/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
https://api.twitter.com/1.1/geo/id/08a67dc7d1141000.json
</td>
<td style="text-align:left;">
GoDataDriven / Xebia Education
</td>
<td style="text-align:left;">
GoDataDriven / Xebia Education
</td>
<td style="text-align:left;">
poi
</td>
<td style="text-align:left;">
The Netherlands
</td>
<td style="text-align:left;">
NL
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
4.912941, 4.912941, 4.912941, 4.912941, 52.352090, 52.352090, 52.352090, 52.352090
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1036176209959366657
</td>
<td style="text-align:left;">
Romain François 🦄
</td>
<td style="text-align:left;">
France
</td>
<td style="text-align:left;">
👨‍💻 \#rstats 📦 with the \#tidyverse team.
</td>
<td style="text-align:left;">
https://t.co/8WIUhd0bJc
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5113
</td>
<td style="text-align:right;">
336
</td>
<td style="text-align:right;">
211
</td>
<td style="text-align:right;">
5837
</td>
<td style="text-align:right;">
5440
</td>
<td style="text-align:left;">
2011-09-21 20:02:22
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/8WIUhd0bJc
</td>
<td style="text-align:left;">
https://purrple.cat
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/377578645/1519142290
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/991018500591378432/U_9\_9qU-\_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
377578645
</td>
<td style="text-align:left;">
1035812809819521024
</td>
<td style="text-align:left;">
2018-09-01 08:53:12
</td>
<td style="text-align:left;">
romain_francois
</td>
<td style="text-align:left;">
Getting more out of \#dplyr, (**SuzanBaert?**) \#amstRday \#satrdays \#rstats \#tidyverse https://t.co/zLDLuXPnM9
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
78
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
dplyr , amstRday , satrdays , rstats , tidyverse
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_yQgFWsAACbUT.jpg
</td>
<td style="text-align:left;">
https://t.co/zLDLuXPnM9
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1035812809819521024/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_yQgFWsAACbUT.jpg
</td>
<td style="text-align:left;">
https://t.co/zLDLuXPnM9
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1035812809819521024/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1035812809819521024
</td>
<td style="text-align:left;">
Romain François 🦄
</td>
<td style="text-align:left;">
France
</td>
<td style="text-align:left;">
👨‍💻 \#rstats 📦 with the \#tidyverse team.
</td>
<td style="text-align:left;">
https://t.co/8WIUhd0bJc
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5113
</td>
<td style="text-align:right;">
336
</td>
<td style="text-align:right;">
211
</td>
<td style="text-align:right;">
5837
</td>
<td style="text-align:right;">
5440
</td>
<td style="text-align:left;">
2011-09-21 20:02:22
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/8WIUhd0bJc
</td>
<td style="text-align:left;">
https://purrple.cat
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/377578645/1519142290
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/991018500591378432/U_9\_9qU-\_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
202543976
</td>
<td style="text-align:left;">
1035976515870179328
</td>
<td style="text-align:left;">
2018-09-01 19:43:43
</td>
<td style="text-align:left;">
g_inberg
</td>
<td style="text-align:left;">
Interesting talks at the first \#satRday Amsterdam! \#AmstRday. Got some of the famous stickers as well:-) \#rstats https://t.co/dUQDAu8Iwn
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
112
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
satRday , AmstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmCGPAlXsAA7Avz.jpg
</td>
<td style="text-align:left;">
https://t.co/dUQDAu8Iwn
</td>
<td style="text-align:left;">
https://twitter.com/g_inberg/status/1035976515870179328/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmCGPAlXsAA7Avz.jpg, http://pbs.twimg.com/media/DmCGPCSXsAAywxz.jpg
</td>
<td style="text-align:left;">
https://t.co/dUQDAu8Iwn, https://t.co/dUQDAu8Iwn
</td>
<td style="text-align:left;">
https://twitter.com/g_inberg/status/1035976515870179328/photo/1, https://twitter.com/g_inberg/status/1035976515870179328/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/g_inberg/status/1035976515870179328
</td>
<td style="text-align:left;">
Ger
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Freelance data scientist, R, python, data viz, travelling, cycling, running
</td>
<td style="text-align:left;">
https://t.co/anNALdOGpO
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
64
</td>
<td style="text-align:right;">
87
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:right;">
68
</td>
<td style="text-align:right;">
73
</td>
<td style="text-align:left;">
2010-10-14 08:26:35
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/anNALdOGpO
</td>
<td style="text-align:left;">
http://gerinberg.com
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/670311083182309380/tvityZ62_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
36220799
</td>
<td style="text-align:left;">
1035967256801497088
</td>
<td style="text-align:left;">
2018-09-01 19:06:56
</td>
<td style="text-align:left;">
infotroph
</td>
<td style="text-align:left;">
Highlight of the afternoon for me at \#AmstRday: Rianne Schouten showing mice::ampute, which generates missing data from a specified multivariate pattern. this looks VERY handy for testing model assumptions. https://t.co/aDs2hkahEe
</td>
<td style="text-align:left;">
Tweetbot for Mac
</td>
<td style="text-align:right;">
230
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
AmstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
rianneschouten.github.io/mice_ampute/vi…
</td>
<td style="text-align:left;">
https://t.co/aDs2hkahEe
</td>
<td style="text-align:left;">
https://rianneschouten.github.io/mice_ampute/vignette/ampute.html
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/infotroph/status/1035967256801497088
</td>
<td style="text-align:left;">
Chris Black
</td>
<td style="text-align:left;">
Nijmegen, NL
</td>
<td style="text-align:left;">
Data janitor building models of root-soil interaction. He/him. Likes human rights, R, sed, transit, error bars, veggies, cats. Attempting less spleen-venting.
</td>
<td style="text-align:left;">
https://t.co/N8i3X4Y7uW
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
475
</td>
<td style="text-align:right;">
454
</td>
<td style="text-align:right;">
39
</td>
<td style="text-align:right;">
8729
</td>
<td style="text-align:right;">
7777
</td>
<td style="text-align:left;">
2009-04-29 00:03:00
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/N8i3X4Y7uW
</td>
<td style="text-align:left;">
http://ckblack.org
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/36220799/1514970161
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/654666018296467456/9m3ijJ_Z\_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
36220799
</td>
<td style="text-align:left;">
1035843502670848000
</td>
<td style="text-align:left;">
2018-09-01 10:55:10
</td>
<td style="text-align:left;">
infotroph
</td>
<td style="text-align:left;">
My highlight of the morning at \#amstRday: (**SuzanBaert?**) with a exceptionally clear walk-through of the scoped dplyr verbs. Slides at https://t.co/I4fc2ySWtl, but look for video — her explanations are outstanding.
</td>
<td style="text-align:left;">
Tweetbot for Mac
</td>
<td style="text-align:right;">
210
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
27
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
github.com/suzanbaert/Sat…
</td>
<td style="text-align:left;">
https://t.co/I4fc2ySWtl
</td>
<td style="text-align:left;">
https://github.com/suzanbaert/SatRdaysAmsterdam18_dplyr
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/infotroph/status/1035843502670848000
</td>
<td style="text-align:left;">
Chris Black
</td>
<td style="text-align:left;">
Nijmegen, NL
</td>
<td style="text-align:left;">
Data janitor building models of root-soil interaction. He/him. Likes human rights, R, sed, transit, error bars, veggies, cats. Attempting less spleen-venting.
</td>
<td style="text-align:left;">
https://t.co/N8i3X4Y7uW
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
475
</td>
<td style="text-align:right;">
454
</td>
<td style="text-align:right;">
39
</td>
<td style="text-align:right;">
8729
</td>
<td style="text-align:right;">
7777
</td>
<td style="text-align:left;">
2009-04-29 00:03:00
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/N8i3X4Y7uW
</td>
<td style="text-align:left;">
http://ckblack.org
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/36220799/1514970161
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/654666018296467456/9m3ijJ_Z\_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
957220441323646978
</td>
<td style="text-align:left;">
1035949359723110400
</td>
<td style="text-align:left;">
2018-09-01 17:55:49
</td>
<td style="text-align:left;">
MadelijnBazen
</td>
<td style="text-align:left;">
Excellent \#satRday conference, with excellent \#rstats takeaways :) Thank you \#AmstRday and \#RLadies! https://t.co/hXC2c2gkMn
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
100
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
satRday , rstats , AmstRday, RLadies
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBsXAOWsAIol3X.jpg
</td>
<td style="text-align:left;">
https://t.co/hXC2c2gkMn
</td>
<td style="text-align:left;">
https://twitter.com/MadelijnBazen/status/1035949359723110400/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBsXAOWsAIol3X.jpg
</td>
<td style="text-align:left;">
https://t.co/hXC2c2gkMn
</td>
<td style="text-align:left;">
https://twitter.com/MadelijnBazen/status/1035949359723110400/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/MadelijnBazen/status/1035949359723110400
</td>
<td style="text-align:left;">
Madelijn Bazen
</td>
<td style="text-align:left;">
Nederlands
</td>
<td style="text-align:left;">
Into Data Visualization \| R \| GIS (**zuid_holland?**) Background in Statistics & Psychology
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
41
</td>
<td style="text-align:right;">
188
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:right;">
65
</td>
<td style="text-align:left;">
2018-01-27 11:55:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/957220441323646978/1518360275
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/957267685171253248/reG5qYm7_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
957220441323646978
</td>
<td style="text-align:left;">
1035930403721367553
</td>
<td style="text-align:left;">
2018-09-01 16:40:29
</td>
<td style="text-align:left;">
MadelijnBazen
</td>
<td style="text-align:left;">
Great \#amstRday keynote talk ‘That’s not \[data\] science!’ by (**dataandme?**)! Learning new words like ex•o•ter•ic and Rgossip..Definitely worth taking the 7:30 train on a \#satRday! https://t.co/ixPUJL7z4A
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
175
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday, satRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBdMWbXsAEhLJc.jpg
</td>
<td style="text-align:left;">
https://t.co/ixPUJL7z4A
</td>
<td style="text-align:left;">
https://twitter.com/MadelijnBazen/status/1035930403721367553/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBdMWbXsAEhLJc.jpg
</td>
<td style="text-align:left;">
https://t.co/ixPUJL7z4A
</td>
<td style="text-align:left;">
https://twitter.com/MadelijnBazen/status/1035930403721367553/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/MadelijnBazen/status/1035930403721367553
</td>
<td style="text-align:left;">
Madelijn Bazen
</td>
<td style="text-align:left;">
Nederlands
</td>
<td style="text-align:left;">
Into Data Visualization \| R \| GIS (**zuid_holland?**) Background in Statistics & Psychology
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
41
</td>
<td style="text-align:right;">
188
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:right;">
65
</td>
<td style="text-align:left;">
2018-01-27 11:55:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/957220441323646978/1518360275
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/957267685171253248/reG5qYm7_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
891904584
</td>
<td style="text-align:left;">
1035850995614527488
</td>
<td style="text-align:left;">
2018-09-01 11:24:57
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
(**edwin_thoen?**) setting up a great punchline for an extended coding joke in \#amstRday about non-standard eval https://t.co/2f1TpFKqgm
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
106
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
1570032288
</td>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAU_BJW4AA2tsh.jpg
</td>
<td style="text-align:left;">
https://t.co/2f1TpFKqgm
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035850995614527488/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAU_BJW4AA2tsh.jpg
</td>
<td style="text-align:left;">
https://t.co/2f1TpFKqgm
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035850995614527488/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
1570032288
</td>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035850995614527488
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
UK
</td>
<td style="text-align:left;">
Make, Do and Mend. \#rstats with (**lockedata?**) and (**satrdays_org?**)
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
306
</td>
<td style="text-align:right;">
612
</td>
<td style="text-align:right;">
17
</td>
<td style="text-align:right;">
1218
</td>
<td style="text-align:right;">
439
</td>
<td style="text-align:left;">
2012-10-19 21:48:48
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
https://github.com/DaveParr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/891904584/1530362945
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1007683337132093440/cujXW7UY_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
891904584
</td>
<td style="text-align:left;">
1035932368404733953
</td>
<td style="text-align:left;">
2018-09-01 16:48:17
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
(**matlabulous?**) knocked it out of the park with his \#mlb moneyball talk at \#amstRday using h2o, lime and shiny to make a winning team! ⚾ https://t.co/TMuObVnGi8 (retweet to fix horrible typo)
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
188
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
296664658
</td>
<td style="text-align:left;">
matlabulous
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
mlb , amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
pic.twitter.com/TMuObVnGi8
</td>
<td style="text-align:left;">
https://t.co/TMuObVnGi8
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035901890217889792/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
296664658
</td>
<td style="text-align:left;">
matlabulous
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035932368404733953
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
UK
</td>
<td style="text-align:left;">
Make, Do and Mend. \#rstats with (**lockedata?**) and (**satrdays_org?**)
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
306
</td>
<td style="text-align:right;">
612
</td>
<td style="text-align:right;">
17
</td>
<td style="text-align:right;">
1218
</td>
<td style="text-align:right;">
439
</td>
<td style="text-align:left;">
2012-10-19 21:48:48
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
https://github.com/DaveParr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/891904584/1530362945
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1007683337132093440/cujXW7UY_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
891904584
</td>
<td style="text-align:left;">
1035882309797531649
</td>
<td style="text-align:left;">
2018-09-01 13:29:23
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
“Three weeks of reporting by hand for 30 reports reduced to three days of r coding and .rmd documents with parameters” \#amstRday \#rstats \#Winning
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
145
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday, rstats , Winning
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035882309797531649
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
UK
</td>
<td style="text-align:left;">
Make, Do and Mend. \#rstats with (**lockedata?**) and (**satrdays_org?**)
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
306
</td>
<td style="text-align:right;">
612
</td>
<td style="text-align:right;">
17
</td>
<td style="text-align:right;">
1218
</td>
<td style="text-align:right;">
439
</td>
<td style="text-align:left;">
2012-10-19 21:48:48
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
https://github.com/DaveParr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/891904584/1530362945
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1007683337132093440/cujXW7UY_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
891904584
</td>
<td style="text-align:left;">
1035872989932396545
</td>
<td style="text-align:left;">
2018-09-01 12:52:21
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
Or come find me at \#amstRday . I’m wearing the same shirt as Oz in this picture, but I have more hair and am in Amsterdam. https://t.co/wjiAyUc0F9
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
122
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
TRUE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
twitter.com/LockeData/stat…
</td>
<td style="text-align:left;">
https://t.co/wjiAyUc0F9
</td>
<td style="text-align:left;">
https://twitter.com/LockeData/status/1035801488675753985
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
1035801488675753985
</td>
<td style="text-align:left;">

Say hi to us at (**Sqlsatoslo?**) and talk to us about how to start doing \#datascience in your org!

Or just get a selfie with the chibi or enter the competition for the start of your data science library 🙋‍♀️ https://t.co/NwXMdI5dgQ
</td>
<td style="text-align:left;">
2018-09-01 08:08:13
</td>
<td style="text-align:left;">
TweetDeck
</td>
<td style="text-align:right;">
19
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
839804970614538240
</td>
<td style="text-align:left;">
LockeData
</td>
<td style="text-align:left;">
Locke Data
</td>
<td style="text-align:right;">
1538
</td>
<td style="text-align:right;">
344
</td>
<td style="text-align:right;">
1515
</td>
<td style="text-align:left;">
United Kingdom
</td>
<td style="text-align:left;">
Founded by (**theStephLocke?**), Locke Data helps organisations start their data science journey. Psst … on the 1st of each month, a random follower wins a book!
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035872989932396545
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
UK
</td>
<td style="text-align:left;">
Make, Do and Mend. \#rstats with (**lockedata?**) and (**satrdays_org?**)
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
306
</td>
<td style="text-align:right;">
612
</td>
<td style="text-align:right;">
17
</td>
<td style="text-align:right;">
1218
</td>
<td style="text-align:right;">
439
</td>
<td style="text-align:left;">
2012-10-19 21:48:48
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
https://github.com/DaveParr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/891904584/1530362945
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1007683337132093440/cujXW7UY_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
891904584
</td>
<td style="text-align:left;">
1035881253667577858
</td>
<td style="text-align:left;">
2018-09-01 13:25:11
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
Great examples of performant natural language processing at \#amstRday https://t.co/QHNhBCzDjv
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
69
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAwgF5X0AA860g.jpg
</td>
<td style="text-align:left;">
https://t.co/QHNhBCzDjv
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035881253667577858/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAwgF5X0AA860g.jpg
</td>
<td style="text-align:left;">
https://t.co/QHNhBCzDjv
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035881253667577858/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035881253667577858
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
UK
</td>
<td style="text-align:left;">
Make, Do and Mend. \#rstats with (**lockedata?**) and (**satrdays_org?**)
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
306
</td>
<td style="text-align:right;">
612
</td>
<td style="text-align:right;">
17
</td>
<td style="text-align:right;">
1218
</td>
<td style="text-align:right;">
439
</td>
<td style="text-align:left;">
2012-10-19 21:48:48
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
https://github.com/DaveParr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/891904584/1530362945
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1007683337132093440/cujXW7UY_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
891904584
</td>
<td style="text-align:left;">
1035902237715910656
</td>
<td style="text-align:left;">
2018-09-01 14:48:34
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
“it’s hard to read a Sudoku problem into R wrong. It’s a perfect language for that”
\#amstRday
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
93
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035902237715910656
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
UK
</td>
<td style="text-align:left;">
Make, Do and Mend. \#rstats with (**lockedata?**) and (**satrdays_org?**)
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
306
</td>
<td style="text-align:right;">
612
</td>
<td style="text-align:right;">
17
</td>
<td style="text-align:right;">
1218
</td>
<td style="text-align:right;">
439
</td>
<td style="text-align:left;">
2012-10-19 21:48:48
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
https://github.com/DaveParr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/891904584/1530362945
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1007683337132093440/cujXW7UY_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
891904584
</td>
<td style="text-align:left;">
1035865575245983744
</td>
<td style="text-align:left;">
2018-09-01 12:22:53
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
(**DerFredo?**) thanks for the ‘sweet’ live coding session \#amstRday https://t.co/yRYxN13VFv
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
62
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAiPbMX0AEqzPU.jpg
</td>
<td style="text-align:left;">
https://t.co/yRYxN13VFv
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035865575245983744/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAiPbMX0AEqzPU.jpg
</td>
<td style="text-align:left;">
https://t.co/yRYxN13VFv
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035865575245983744/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035865575245983744
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
UK
</td>
<td style="text-align:left;">
Make, Do and Mend. \#rstats with (**lockedata?**) and (**satrdays_org?**)
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
306
</td>
<td style="text-align:right;">
612
</td>
<td style="text-align:right;">
17
</td>
<td style="text-align:right;">
1218
</td>
<td style="text-align:right;">
439
</td>
<td style="text-align:left;">
2012-10-19 21:48:48
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
https://github.com/DaveParr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/891904584/1530362945
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1007683337132093440/cujXW7UY_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
891904584
</td>
<td style="text-align:left;">
1035876236659187712
</td>
<td style="text-align:left;">
2018-09-01 13:05:15
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
(**rgiordano79?**) helping regular people express themselves using \#regex at \#amstRday https://t.co/UYtthIh2kz
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
80
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
120816884
</td>
<td style="text-align:left;">
rgiordano79
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
regex , amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAr8N1WsAAJ8_U.jpg
</td>
<td style="text-align:left;">
https://t.co/UYtthIh2kz
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035876236659187712/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAr8N1WsAAJ8_U.jpg
</td>
<td style="text-align:left;">
https://t.co/UYtthIh2kz
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035876236659187712/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
120816884
</td>
<td style="text-align:left;">
rgiordano79
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035876236659187712
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
UK
</td>
<td style="text-align:left;">
Make, Do and Mend. \#rstats with (**lockedata?**) and (**satrdays_org?**)
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
306
</td>
<td style="text-align:right;">
612
</td>
<td style="text-align:right;">
17
</td>
<td style="text-align:right;">
1218
</td>
<td style="text-align:right;">
439
</td>
<td style="text-align:left;">
2012-10-19 21:48:48
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
https://github.com/DaveParr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/891904584/1530362945
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1007683337132093440/cujXW7UY_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
494325889
</td>
<td style="text-align:left;">
1035932212938657792
</td>
<td style="text-align:left;">
2018-09-01 16:47:40
</td>
<td style="text-align:left;">
FlorisPadt
</td>
<td style="text-align:left;">
(**edwin_thoen?**) Thanks (**EdwinThoen?**) for coming despite of flu and giving a talk on steroids \#amstRday about tidyeval interesting, mind boggling and entertaining,
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
145
</td>
<td style="text-align:left;">
1035552924963885056
</td>
<td style="text-align:left;">
1570032288
</td>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
1570032288, 71872299
</td>
<td style="text-align:left;">
edwin_thoen, EdwinThoen
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/FlorisPadt/status/1035932212938657792
</td>
<td style="text-align:left;">
Floris Padt
</td>
<td style="text-align:left;">
Hilversum
</td>
<td style="text-align:left;">
SAP BI & Analytics, Operational Excellence & SCM optimization in Retail. Dad of 3
</td>
<td style="text-align:left;">
http://t.co/duosMoVqCY
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
92
</td>
<td style="text-align:right;">
126
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:right;">
229
</td>
<td style="text-align:right;">
58
</td>
<td style="text-align:left;">
2012-02-16 19:41:06
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
http://t.co/duosMoVqCY
</td>
<td style="text-align:left;">
http://www.linkedin.com/in/florispadt
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/2235592355/ad6Twit_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
1291259790
</td>
<td style="text-align:left;">
1035895583951802369
</td>
<td style="text-align:left;">
2018-09-01 14:22:07
</td>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:left;">
‘Why ROC curves are unfit for business modelling’ with Pieter Marcus @ \#AmstRday. Check out the modelplotR package. \#SatRdays https://t.co/kn7u8Rkoid
</td>
<td style="text-align:left;">
Twitter Lite
</td>
<td style="text-align:right;">
125
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRday, SatRdays
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA9h-QWsAUwI4w.jpg
</td>
<td style="text-align:left;">
https://t.co/kn7u8Rkoid
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035895583951802369/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA9h-QWsAUwI4w.jpg, http://pbs.twimg.com/media/DmA9h-fWwAEaH6O.jpg, http://pbs.twimg.com/media/DmA9h-YW4AIjIdY.jpg, http://pbs.twimg.com/media/DmA9h-aXcAEJGY7.jpg
</td>
<td style="text-align:left;">
https://t.co/kn7u8Rkoid, https://t.co/kn7u8Rkoid, https://t.co/kn7u8Rkoid, https://t.co/kn7u8Rkoid
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035895583951802369/photo/1, https://twitter.com/dragonflystats/status/1035895583951802369/photo/1, https://twitter.com/dragonflystats/status/1035895583951802369/photo/1, https://twitter.com/dragonflystats/status/1035895583951802369/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035895583951802369
</td>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:left;">
Dublin, Ireland
</td>
<td style="text-align:left;">
Statistician and Coder - Data Sciences, Rstats, Python, Julia, MatLab, etc. (many tweets intended for my students)
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2844
</td>
<td style="text-align:right;">
2360
</td>
<td style="text-align:right;">
220
</td>
<td style="text-align:right;">
3547
</td>
<td style="text-align:right;">
4043
</td>
<td style="text-align:left;">
2013-03-23 12:10:36
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
https://www.linkedin.com/profile/view?id=14325915&trk=nav_responsive_tab_profile
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1291259790/1420153011
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/3427713318/840e4aa0a6dca9263a0507fbfe4c4074_normal.jpeg
</td>
</tr>
<tr>
<td style="text-align:left;">
1291259790
</td>
<td style="text-align:left;">
1035908429355855874
</td>
<td style="text-align:left;">
2018-09-01 15:13:10
</td>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:left;">
That’s a wrap for \#AmstRday 2018. Great conference. https://t.co/JqrPHgZMc8
</td>
<td style="text-align:left;">
Twitter Lite
</td>
<td style="text-align:right;">
51
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
AmstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBJOBcX0AUcBat.jpg
</td>
<td style="text-align:left;">
https://t.co/JqrPHgZMc8
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035908429355855874/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBJOBcX0AUcBat.jpg, http://pbs.twimg.com/media/DmBJOBfXsAA1tYU.jpg, http://pbs.twimg.com/media/DmBJOBeXcAAhKW1.jpg
</td>
<td style="text-align:left;">
https://t.co/JqrPHgZMc8, https://t.co/JqrPHgZMc8, https://t.co/JqrPHgZMc8
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035908429355855874/photo/1, https://twitter.com/dragonflystats/status/1035908429355855874/photo/1, https://twitter.com/dragonflystats/status/1035908429355855874/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035908429355855874
</td>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:left;">
Dublin, Ireland
</td>
<td style="text-align:left;">
Statistician and Coder - Data Sciences, Rstats, Python, Julia, MatLab, etc. (many tweets intended for my students)
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2844
</td>
<td style="text-align:right;">
2360
</td>
<td style="text-align:right;">
220
</td>
<td style="text-align:right;">
3547
</td>
<td style="text-align:right;">
4043
</td>
<td style="text-align:left;">
2013-03-23 12:10:36
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
https://www.linkedin.com/profile/view?id=14325915&trk=nav_responsive_tab_profile
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1291259790/1420153011
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/3427713318/840e4aa0a6dca9263a0507fbfe4c4074_normal.jpeg
</td>
</tr>
<tr>
<td style="text-align:left;">
1291259790
</td>
<td style="text-align:left;">
1035885555534495744
</td>
<td style="text-align:left;">
2018-09-01 13:42:16
</td>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:left;">
How to avoid electric vehicles charge-ups overloading the Electricity Grid With Jeroen Groot - Lightning Talk @ \#AmstRday \#rstats https://t.co/LxznG1Eptr
</td>
<td style="text-align:left;">
Twitter Lite
</td>
<td style="text-align:right;">
129
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
AmstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA0aF3XsAIsIQd.jpg
</td>
<td style="text-align:left;">
https://t.co/LxznG1Eptr
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035885555534495744/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA0aF3XsAIsIQd.jpg, http://pbs.twimg.com/media/DmA0aGDXcAArTB5.jpg, http://pbs.twimg.com/media/DmA0aF5XcAU0Y9B.jpg, http://pbs.twimg.com/media/DmA0aGFWsAIFUhj.jpg
</td>
<td style="text-align:left;">
https://t.co/LxznG1Eptr, https://t.co/LxznG1Eptr, https://t.co/LxznG1Eptr, https://t.co/LxznG1Eptr
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035885555534495744/photo/1, https://twitter.com/dragonflystats/status/1035885555534495744/photo/1, https://twitter.com/dragonflystats/status/1035885555534495744/photo/1, https://twitter.com/dragonflystats/status/1035885555534495744/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035885555534495744
</td>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:left;">
Dublin, Ireland
</td>
<td style="text-align:left;">
Statistician and Coder - Data Sciences, Rstats, Python, Julia, MatLab, etc. (many tweets intended for my students)
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2844
</td>
<td style="text-align:right;">
2360
</td>
<td style="text-align:right;">
220
</td>
<td style="text-align:right;">
3547
</td>
<td style="text-align:right;">
4043
</td>
<td style="text-align:left;">
2013-03-23 12:10:36
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
https://www.linkedin.com/profile/view?id=14325915&trk=nav_responsive_tab_profile
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1291259790/1420153011
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/3427713318/840e4aa0a6dca9263a0507fbfe4c4074_normal.jpeg
</td>
</tr>
<tr>
<td style="text-align:left;">
1291259790
</td>
<td style="text-align:left;">
1035881932108771329
</td>
<td style="text-align:left;">
2018-09-01 13:27:53
</td>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:left;">
‘Using \#rstats and R markdown for Individual Reports’ with Olga Sholderer - lightning talk @ \#AmstRday \#SatRdays https://t.co/j8smV5BLDA
</td>
<td style="text-align:left;">
Twitter Lite
</td>
<td style="text-align:right;">
112
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
rstats , AmstRday, SatRdays
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAxHhdXsAAEFI4.jpg
</td>
<td style="text-align:left;">
https://t.co/j8smV5BLDA
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035881932108771329/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAxHhdXsAAEFI4.jpg, http://pbs.twimg.com/media/DmAxHhdX0AANgwE.jpg, http://pbs.twimg.com/media/DmAxHhgWwAA4TDS.jpg
</td>
<td style="text-align:left;">
https://t.co/j8smV5BLDA, https://t.co/j8smV5BLDA, https://t.co/j8smV5BLDA
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035881932108771329/photo/1, https://twitter.com/dragonflystats/status/1035881932108771329/photo/1, https://twitter.com/dragonflystats/status/1035881932108771329/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035881932108771329
</td>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:left;">
Dublin, Ireland
</td>
<td style="text-align:left;">
Statistician and Coder - Data Sciences, Rstats, Python, Julia, MatLab, etc. (many tweets intended for my students)
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2844
</td>
<td style="text-align:right;">
2360
</td>
<td style="text-align:right;">
220
</td>
<td style="text-align:right;">
3547
</td>
<td style="text-align:right;">
4043
</td>
<td style="text-align:left;">
2013-03-23 12:10:36
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
https://www.linkedin.com/profile/view?id=14325915&trk=nav_responsive_tab_profile
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1291259790/1420153011
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/3427713318/840e4aa0a6dca9263a0507fbfe4c4074_normal.jpeg
</td>
</tr>
<tr>
<td style="text-align:left;">
1291259790
</td>
<td style="text-align:left;">
1035902942396727296
</td>
<td style="text-align:left;">
2018-09-01 14:51:22
</td>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:left;">
‘Solving Sudokus with R and C++’ With Bob Jansen at \#AmstRday \#satrdays https://t.co/VC3wx0GLWi
</td>
<td style="text-align:left;">
Twitter Lite
</td>
<td style="text-align:right;">
71
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
AmstRday, satrdays
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBEN-rX0AAwTaM.jpg
</td>
<td style="text-align:left;">
https://t.co/VC3wx0GLWi
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035902942396727296/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBEN-rX0AAwTaM.jpg, http://pbs.twimg.com/media/DmBEN-qX4AAf6SN.jpg, http://pbs.twimg.com/media/DmBEN-sXoAEjN87.jpg, http://pbs.twimg.com/media/DmBEN-sWwAAfRkM.jpg
</td>
<td style="text-align:left;">
https://t.co/VC3wx0GLWi, https://t.co/VC3wx0GLWi, https://t.co/VC3wx0GLWi, https://t.co/VC3wx0GLWi
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035902942396727296/photo/1, https://twitter.com/dragonflystats/status/1035902942396727296/photo/1, https://twitter.com/dragonflystats/status/1035902942396727296/photo/1, https://twitter.com/dragonflystats/status/1035902942396727296/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035902942396727296
</td>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:left;">
Dublin, Ireland
</td>
<td style="text-align:left;">
Statistician and Coder - Data Sciences, Rstats, Python, Julia, MatLab, etc. (many tweets intended for my students)
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2844
</td>
<td style="text-align:right;">
2360
</td>
<td style="text-align:right;">
220
</td>
<td style="text-align:right;">
3547
</td>
<td style="text-align:right;">
4043
</td>
<td style="text-align:left;">
2013-03-23 12:10:36
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
https://www.linkedin.com/profile/view?id=14325915&trk=nav_responsive_tab_profile
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1291259790/1420153011
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/3427713318/840e4aa0a6dca9263a0507fbfe4c4074_normal.jpeg
</td>
</tr>
<tr>
<td style="text-align:left;">
1291259790
</td>
<td style="text-align:left;">
1035878319047299074
</td>
<td style="text-align:left;">
2018-09-01 13:13:31
</td>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:left;">
Longhow Lam giving a lightning talk on text2vec with \#rstats : predicting house prices \#AmstRday https://t.co/8de0ibGpqa
</td>
<td style="text-align:left;">
Twitter Lite
</td>
<td style="text-align:right;">
96
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
rstats , AmstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAt1eFXcAA3kiI.jpg
</td>
<td style="text-align:left;">
https://t.co/8de0ibGpqa
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035878319047299074/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAt1eFXcAA3kiI.jpg, http://pbs.twimg.com/media/DmAt1eGX0AYQBiZ.jpg, http://pbs.twimg.com/media/DmAt1eHXsAgFPVi.jpg, http://pbs.twimg.com/media/DmAt1eJW0AApKWr.jpg
</td>
<td style="text-align:left;">
https://t.co/8de0ibGpqa, https://t.co/8de0ibGpqa, https://t.co/8de0ibGpqa, https://t.co/8de0ibGpqa
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035878319047299074/photo/1, https://twitter.com/dragonflystats/status/1035878319047299074/photo/1, https://twitter.com/dragonflystats/status/1035878319047299074/photo/1, https://twitter.com/dragonflystats/status/1035878319047299074/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035878319047299074
</td>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:left;">
Dublin, Ireland
</td>
<td style="text-align:left;">
Statistician and Coder - Data Sciences, Rstats, Python, Julia, MatLab, etc. (many tweets intended for my students)
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2844
</td>
<td style="text-align:right;">
2360
</td>
<td style="text-align:right;">
220
</td>
<td style="text-align:right;">
3547
</td>
<td style="text-align:right;">
4043
</td>
<td style="text-align:left;">
2013-03-23 12:10:36
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
https://www.linkedin.com/profile/view?id=14325915&trk=nav_responsive_tab_profile
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1291259790/1420153011
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/3427713318/840e4aa0a6dca9263a0507fbfe4c4074_normal.jpeg
</td>
</tr>
<tr>
<td style="text-align:left;">
1291259790
</td>
<td style="text-align:left;">
1035926032870723584
</td>
<td style="text-align:left;">
2018-09-01 16:23:07
</td>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:left;">
Very impressed with the \#AmstRday venue. Fair play to (**GoDataDriven?**) for providing a great venue. \#AmstRday \#RStats https://t.co/qiAyoYaGUx
</td>
<td style="text-align:left;">
Twitter Lite
</td>
<td style="text-align:right;">
114
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRday, AmstRday, RStats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBZOVeWsAAowAs.jpg
</td>
<td style="text-align:left;">
https://t.co/qiAyoYaGUx
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035926032870723584/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBZOVeWsAAowAs.jpg
</td>
<td style="text-align:left;">
https://t.co/qiAyoYaGUx
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035926032870723584/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
1253544996
</td>
<td style="text-align:left;">
GoDataDriven
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035926032870723584
</td>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:left;">
Dublin, Ireland
</td>
<td style="text-align:left;">
Statistician and Coder - Data Sciences, Rstats, Python, Julia, MatLab, etc. (many tweets intended for my students)
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2844
</td>
<td style="text-align:right;">
2360
</td>
<td style="text-align:right;">
220
</td>
<td style="text-align:right;">
3547
</td>
<td style="text-align:right;">
4043
</td>
<td style="text-align:left;">
2013-03-23 12:10:36
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
https://www.linkedin.com/profile/view?id=14325915&trk=nav_responsive_tab_profile
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1291259790/1420153011
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/3427713318/840e4aa0a6dca9263a0507fbfe4c4074_normal.jpeg
</td>
</tr>
<tr>
<td style="text-align:left;">
1291259790
</td>
<td style="text-align:left;">
1035892887760908289
</td>
<td style="text-align:left;">
2018-09-01 14:11:25
</td>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:left;">
“Generating Missing Values with Ampute” with Rianne Schouten @ \#AmstRday \#rstats https://t.co/83eJX3p6k5
</td>
<td style="text-align:left;">
Twitter Lite
</td>
<td style="text-align:right;">
80
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
AmstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA7FLAWsAAgUQF.jpg
</td>
<td style="text-align:left;">
https://t.co/83eJX3p6k5
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035892887760908289/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA7FLAWsAAgUQF.jpg, http://pbs.twimg.com/media/DmA7FKyXsAAT-YA.jpg, http://pbs.twimg.com/media/DmA7FKyX0AEEzWG.jpg, http://pbs.twimg.com/media/DmA7FK3W0AAYtZn.jpg
</td>
<td style="text-align:left;">
https://t.co/83eJX3p6k5, https://t.co/83eJX3p6k5, https://t.co/83eJX3p6k5, https://t.co/83eJX3p6k5
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035892887760908289/photo/1, https://twitter.com/dragonflystats/status/1035892887760908289/photo/1, https://twitter.com/dragonflystats/status/1035892887760908289/photo/1, https://twitter.com/dragonflystats/status/1035892887760908289/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035892887760908289
</td>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:left;">
Dublin, Ireland
</td>
<td style="text-align:left;">
Statistician and Coder - Data Sciences, Rstats, Python, Julia, MatLab, etc. (many tweets intended for my students)
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2844
</td>
<td style="text-align:right;">
2360
</td>
<td style="text-align:right;">
220
</td>
<td style="text-align:right;">
3547
</td>
<td style="text-align:right;">
4043
</td>
<td style="text-align:left;">
2013-03-23 12:10:36
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
https://www.linkedin.com/profile/view?id=14325915&trk=nav_responsive_tab_profile
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1291259790/1420153011
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/3427713318/840e4aa0a6dca9263a0507fbfe4c4074_normal.jpeg
</td>
</tr>
<tr>
<td style="text-align:left;">
1291259790
</td>
<td style="text-align:left;">
1035899207264202752
</td>
<td style="text-align:left;">
2018-09-01 14:36:31
</td>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:left;">
Jo Fai Chow from (**h2oai?**) talks Baseball and Moneyball @ \#AmstRday \#satrdays https://t.co/s8CJAKl02o
</td>
<td style="text-align:left;">
Twitter Lite
</td>
<td style="text-align:right;">
74
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
AmstRday, satrdays
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBA0hfXsAAnVtk.jpg
</td>
<td style="text-align:left;">
https://t.co/s8CJAKl02o
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035899207264202752/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBA0hfXsAAnVtk.jpg, http://pbs.twimg.com/media/DmBA0hgX4AAlcDQ.jpg, http://pbs.twimg.com/media/DmBA0hiX4AAQe-G.jpg, http://pbs.twimg.com/media/DmBA0hhX0AEDlBh.jpg
</td>
<td style="text-align:left;">
https://t.co/s8CJAKl02o, https://t.co/s8CJAKl02o, https://t.co/s8CJAKl02o, https://t.co/s8CJAKl02o
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035899207264202752/photo/1, https://twitter.com/dragonflystats/status/1035899207264202752/photo/1, https://twitter.com/dragonflystats/status/1035899207264202752/photo/1, https://twitter.com/dragonflystats/status/1035899207264202752/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
481867656
</td>
<td style="text-align:left;">
h2oai
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035899207264202752
</td>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:left;">
Dublin, Ireland
</td>
<td style="text-align:left;">
Statistician and Coder - Data Sciences, Rstats, Python, Julia, MatLab, etc. (many tweets intended for my students)
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2844
</td>
<td style="text-align:right;">
2360
</td>
<td style="text-align:right;">
220
</td>
<td style="text-align:right;">
3547
</td>
<td style="text-align:right;">
4043
</td>
<td style="text-align:left;">
2013-03-23 12:10:36
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
https://www.linkedin.com/profile/view?id=14325915&trk=nav_responsive_tab_profile
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1291259790/1420153011
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/3427713318/840e4aa0a6dca9263a0507fbfe4c4074_normal.jpeg
</td>
</tr>
<tr>
<td style="text-align:left;">
1253544996
</td>
<td style="text-align:left;">
1035923415608295424
</td>
<td style="text-align:left;">
2018-09-01 16:12:43
</td>
<td style="text-align:left;">
GoDataDriven
</td>
<td style="text-align:left;">
The magic of data at \#AmstRday! Yesterday started with great workshops at (**Uber_NL?**). Today is full of \#R talks at the conference. It is lovely to contribute to more \#Rstats \#datascience awesomeness with (**satRdays_org?**), (**rstudio?**), (**RLadiesAMS?**), and thanks to all inspiring speakers! https://t.co/tj7GmwjQ5G
</td>
<td style="text-align:left;">
HubSpot
</td>
<td style="text-align:right;">
277
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
AmstRday , R , Rstats , datascience
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBW2y0XoAE8HCk.jpg
</td>
<td style="text-align:left;">
https://t.co/tj7GmwjQ5G
</td>
<td style="text-align:left;">
https://twitter.com/GoDataDriven/status/1035923415608295424/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBW2y0XoAE8HCk.jpg
</td>
<td style="text-align:left;">
https://t.co/tj7GmwjQ5G
</td>
<td style="text-align:left;">
https://twitter.com/GoDataDriven/status/1035923415608295424/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
791919660 , 737390070252998656, 235261861 , 964839447798910976
</td>
<td style="text-align:left;">
Uber_NL , satRdays_org, rstudio , RLadiesAMS
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/GoDataDriven/status/1035923415608295424
</td>
<td style="text-align:left;">
GoDataDriven
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
We’re all about the DataDriven Enterprise. \#BigData Platform Implementations, \#Data Engineering and applied \#DataScience.
</td>
<td style="text-align:left;">
http://t.co/cXyUP5yZYX
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1670
</td>
<td style="text-align:right;">
901
</td>
<td style="text-align:right;">
137
</td>
<td style="text-align:right;">
1032
</td>
<td style="text-align:right;">
408
</td>
<td style="text-align:left;">
2013-03-09 06:14:18
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
http://t.co/cXyUP5yZYX
</td>
<td style="text-align:left;">
http://www.godatadriven.com/
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1253544996/1536304024
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1037959579185938432/BMCn_z6X_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
964839447798910976
</td>
<td style="text-align:left;">
1035917734100561920
</td>
<td style="text-align:left;">
2018-09-01 15:50:08
</td>
<td style="text-align:left;">
RLadiesAMS
</td>
<td style="text-align:left;">

\#rladies awesomeness at \#amstRday

(**RladiesBrussels?**) (**RLadiesStras?**) (**RLadiesGlobal?**) (**Tesskorthout?**) (**TheSarahStolle?**) (**rgiordano79?**) (**cecilesauder?**) https://t.co/5V9hPRWG6j
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
138
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
58
</td>
<td style="text-align:right;">
15
</td>
<td style="text-align:left;">
rladies , amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBRri2XoAATkJw.jpg
</td>
<td style="text-align:left;">
https://t.co/5V9hPRWG6j
</td>
<td style="text-align:left;">
https://twitter.com/RLadiesAMS/status/1035917734100561920/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBRri2XoAATkJw.jpg
</td>
<td style="text-align:left;">
https://t.co/5V9hPRWG6j
</td>
<td style="text-align:left;">
https://twitter.com/RLadiesAMS/status/1035917734100561920/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
929302435876753408, 912221092500197377, 770490229769789440, 106091106 , 935995440792784900, 120816884 , 964088911
</td>
<td style="text-align:left;">
RladiesBrussels, RLadiesStras , RLadiesGlobal , Tesskorthout , TheSarahStolle , rgiordano79 , cecilesauder
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/RLadiesAMS/status/1035917734100561920
</td>
<td style="text-align:left;">
R- Ladies Amsterdam
</td>
<td style="text-align:left;">
Amsterdam, Nederlands
</td>
<td style="text-align:left;">
Amsterdam’s local \#RLadies chapter, aiming to increase gender diversity in the \#rstats, \#tech, and \#datascience community.
</td>
<td style="text-align:left;">
https://t.co/hDfN2XRoIG
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
176
</td>
<td style="text-align:right;">
83
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
149
</td>
<td style="text-align:right;">
107
</td>
<td style="text-align:left;">
2018-02-17 12:30:25
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/hDfN2XRoIG
</td>
<td style="text-align:left;">
https://www.meetup.com/rladies-amsterdam/
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/964839447798910976/1518871950
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/964843467150102528/ScQ2RYdF_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
964839447798910976
</td>
<td style="text-align:left;">
1035479879482056706
</td>
<td style="text-align:left;">
2018-08-31 10:50:16
</td>
<td style="text-align:left;">
RLadiesAMS
</td>
<td style="text-align:left;">
Excited to see \#Rladies at \#amstRday ! https://t.co/0FOgCTXuxu
</td>
<td style="text-align:left;">
TweetDeck
</td>
<td style="text-align:right;">
38
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
TRUE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Rladies , amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
twitter.com/Janinekhuc/sta…
</td>
<td style="text-align:left;">
https://t.co/0FOgCTXuxu
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035479480230440960
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
1035479480230440960
</td>
<td style="text-align:left;">
Excited to kick off the first \#satRdays in Amsterdam. Follow \#amstRday for updates over the weekend- brilliant minds coming together to learn, teach and discuss \#rstats https://t.co/19lOvaxhD9
</td>
<td style="text-align:left;">
2018-08-31 10:48:41
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
12
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/RLadiesAMS/status/1035479879482056706
</td>
<td style="text-align:left;">
R- Ladies Amsterdam
</td>
<td style="text-align:left;">
Amsterdam, Nederlands
</td>
<td style="text-align:left;">
Amsterdam’s local \#RLadies chapter, aiming to increase gender diversity in the \#rstats, \#tech, and \#datascience community.
</td>
<td style="text-align:left;">
https://t.co/hDfN2XRoIG
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
176
</td>
<td style="text-align:right;">
83
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
149
</td>
<td style="text-align:right;">
107
</td>
<td style="text-align:left;">
2018-02-17 12:30:25
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/hDfN2XRoIG
</td>
<td style="text-align:left;">
https://www.meetup.com/rladies-amsterdam/
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/964839447798910976/1518871950
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/964843467150102528/ScQ2RYdF_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
964839447798910976
</td>
<td style="text-align:left;">
1035818326667264001
</td>
<td style="text-align:left;">
2018-09-01 09:15:08
</td>
<td style="text-align:left;">
RLadiesAMS
</td>
<td style="text-align:left;">
(**RladiesBrussels?**) power at \#amstRday ! Great talk by (**SuzanBaert?**) on how to get more out of dplyr. \#rstats \#rladies https://t.co/yOHq8wCyWO
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
113
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
929302435876753408
</td>
<td style="text-align:left;">
RladiesBrussels
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
amstRday, rstats , rladies
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_3RNNWsAAsB5m.jpg
</td>
<td style="text-align:left;">
https://t.co/yOHq8wCyWO
</td>
<td style="text-align:left;">
https://twitter.com/RLadiesAMS/status/1035818326667264001/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_3RNNWsAAsB5m.jpg
</td>
<td style="text-align:left;">
https://t.co/yOHq8wCyWO
</td>
<td style="text-align:left;">
https://twitter.com/RLadiesAMS/status/1035818326667264001/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
929302435876753408, 931042575158513664
</td>
<td style="text-align:left;">
RladiesBrussels, SuzanBaert
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/RLadiesAMS/status/1035818326667264001
</td>
<td style="text-align:left;">
R- Ladies Amsterdam
</td>
<td style="text-align:left;">
Amsterdam, Nederlands
</td>
<td style="text-align:left;">
Amsterdam’s local \#RLadies chapter, aiming to increase gender diversity in the \#rstats, \#tech, and \#datascience community.
</td>
<td style="text-align:left;">
https://t.co/hDfN2XRoIG
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
176
</td>
<td style="text-align:right;">
83
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
149
</td>
<td style="text-align:right;">
107
</td>
<td style="text-align:left;">
2018-02-17 12:30:25
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/hDfN2XRoIG
</td>
<td style="text-align:left;">
https://www.meetup.com/rladies-amsterdam/
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/964839447798910976/1518871950
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/964843467150102528/ScQ2RYdF_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
964839447798910976
</td>
<td style="text-align:left;">
1035877452420206592
</td>
<td style="text-align:left;">
2018-09-01 13:10:04
</td>
<td style="text-align:left;">
RLadiesAMS
</td>
<td style="text-align:left;">
More \#rladies power! (**rgiordano79?**) from (**RLadiesStras?**) telling us about the awesomeness of \#regex in \#rstats! \#amstRday https://t.co/rpxEAboBaG
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
117
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
rladies , regex , rstats , amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAtCuhXsAEOUQy.jpg
</td>
<td style="text-align:left;">
https://t.co/rpxEAboBaG
</td>
<td style="text-align:left;">
https://twitter.com/RLadiesAMS/status/1035877452420206592/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAtCuhXsAEOUQy.jpg
</td>
<td style="text-align:left;">
https://t.co/rpxEAboBaG
</td>
<td style="text-align:left;">
https://twitter.com/RLadiesAMS/status/1035877452420206592/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
120816884 , 912221092500197377
</td>
<td style="text-align:left;">
rgiordano79 , RLadiesStras
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/RLadiesAMS/status/1035877452420206592
</td>
<td style="text-align:left;">
R- Ladies Amsterdam
</td>
<td style="text-align:left;">
Amsterdam, Nederlands
</td>
<td style="text-align:left;">
Amsterdam’s local \#RLadies chapter, aiming to increase gender diversity in the \#rstats, \#tech, and \#datascience community.
</td>
<td style="text-align:left;">
https://t.co/hDfN2XRoIG
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
176
</td>
<td style="text-align:right;">
83
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
149
</td>
<td style="text-align:right;">
107
</td>
<td style="text-align:left;">
2018-02-17 12:30:25
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/hDfN2XRoIG
</td>
<td style="text-align:left;">
https://www.meetup.com/rladies-amsterdam/
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/964839447798910976/1518871950
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/964843467150102528/ScQ2RYdF_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
24228154
</td>
<td style="text-align:left;">
1035914037991624704
</td>
<td style="text-align:left;">
2018-09-01 15:35:27
</td>
<td style="text-align:left;">
hspter
</td>
<td style="text-align:left;">
(**Tesskorthout?**) (**dataandme?**) (**NSSDeviations?**) (**rdpeng?**) aww yay!! that makes my morning!! =) (uh and would LOVE to come to Amsterdam!) \#amstRday
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
88
</td>
<td style="text-align:left;">
1035799538462806016
</td>
<td style="text-align:left;">
106091106
</td>
<td style="text-align:left;">
Tesskorthout
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
106091106 , 3230388598, 3827302049, 9308212
</td>
<td style="text-align:left;">
Tesskorthout , dataandme , NSSDeviations, rdpeng
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/hspter/status/1035914037991624704
</td>
<td style="text-align:left;">
Hilary Parker
</td>
<td style="text-align:left;">
San Francisco
</td>
<td style="text-align:left;">
Data Scientist (**StitchFix?**), co-host of (**NSSDeviations?**), \#1 fan of (**TheSquidofTruth?**) \#rstats \#rcatladies
</td>
<td style="text-align:left;">
https://t.co/tjICmkA2EF
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
20784
</td>
<td style="text-align:right;">
1892
</td>
<td style="text-align:right;">
809
</td>
<td style="text-align:right;">
23007
</td>
<td style="text-align:right;">
28603
</td>
<td style="text-align:left;">
2009-03-13 18:59:32
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/tjICmkA2EF
</td>
<td style="text-align:left;">
http://hilaryparker.com
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/24228154/1468982290
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/611535712710729728/ZrqMrN21_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
923984409837162496
</td>
<td style="text-align:left;">
1035829373016915973
</td>
<td style="text-align:left;">
2018-09-01 09:59:01
</td>
<td style="text-align:left;">
smartR101
</td>
<td style="text-align:left;">
Thanks (**Dominik?**) Krzemiński #amstRday very useful:
Making Shiny shine even brighter
https://t.co/UeqNRR2TYj https://t.co/GiO71d7Z00 https://t.co/qhYvcSweK3 all from https://t.co/PaH9chdk3k https://t.co/tsX1bwx1b2
</td>
<td style="text-align:left;">
TweetDeck
</td>
<td style="text-align:right;">
188
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
appsilon.github.io/shiny.semantic/ , demo.appsilondatascience.com/shiny-semantic…, github.com/Appsilon/seman… , github.com/appsilon
</td>
<td style="text-align:left;">
https://t.co/UeqNRR2TYj, https://t.co/GiO71d7Z00, https://t.co/qhYvcSweK3, https://t.co/PaH9chdk3k
</td>
<td style="text-align:left;">
https://appsilon.github.io/shiny.semantic/ , https://demo.appsilondatascience.com/shiny-semantic-components/, https://github.com/Appsilon/semantic.dashboard , https://github.com/appsilon
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmABSN1W4AAK2Ak.jpg
</td>
<td style="text-align:left;">
https://t.co/tsX1bwx1b2
</td>
<td style="text-align:left;">
https://twitter.com/smartR101/status/1035829373016915973/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmABSN1W4AAK2Ak.jpg
</td>
<td style="text-align:left;">
https://t.co/tsX1bwx1b2
</td>
<td style="text-align:left;">
https://twitter.com/smartR101/status/1035829373016915973/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
2623
</td>
<td style="text-align:left;">
dominik
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/smartR101/status/1035829373016915973
</td>
<td style="text-align:left;">
smart-R
</td>
<td style="text-align:left;">
Hilversum, Nederlands
</td>
<td style="text-align:left;">
focused on increasing Roi through better business decisions directed by the Art of business & data Modeling, Statistics & open source Tools like R.
</td>
<td style="text-align:left;">
https://t.co/XZstNiHoZD
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:right;">
40
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
13
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
2017-10-27 18:47:04
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/XZstNiHoZD
</td>
<td style="text-align:left;">
http://www.smart-r.net
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/923984409837162496/1509133757
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/923998501398351877/EXEH4wAz_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
923984409837162496
</td>
<td style="text-align:left;">
1035856509031407617
</td>
<td style="text-align:left;">
2018-09-01 11:46:51
</td>
<td style="text-align:left;">
smartR101
</td>
<td style="text-align:left;">
An exploration of NSE and tidyeval by Edwin Thoen https://t.co/TAHYEKPXGp, \#amstRday https://t.co/7xsYGW9w65, nice to be a Koala and get it all explained https://t.co/lXxYXCTpoO
</td>
<td style="text-align:left;">
TweetDeck
</td>
<td style="text-align:right;">
154
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
github.com/EdwinTh/satRday , edwinth.github.io/blog/dplyr-rec…
</td>
<td style="text-align:left;">
https://t.co/TAHYEKPXGp, https://t.co/7xsYGW9w65
</td>
<td style="text-align:left;">
https://github.com/EdwinTh/satRday , https://edwinth.github.io/blog/dplyr-recipes/
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAZ6ulXsAAapP7.jpg
</td>
<td style="text-align:left;">
https://t.co/lXxYXCTpoO
</td>
<td style="text-align:left;">
https://twitter.com/smartR101/status/1035856509031407617/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAZ6ulXsAAapP7.jpg
</td>
<td style="text-align:left;">
https://t.co/lXxYXCTpoO
</td>
<td style="text-align:left;">
https://twitter.com/smartR101/status/1035856509031407617/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/smartR101/status/1035856509031407617
</td>
<td style="text-align:left;">
smart-R
</td>
<td style="text-align:left;">
Hilversum, Nederlands
</td>
<td style="text-align:left;">
focused on increasing Roi through better business decisions directed by the Art of business & data Modeling, Statistics & open source Tools like R.
</td>
<td style="text-align:left;">
https://t.co/XZstNiHoZD
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:right;">
40
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
13
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
2017-10-27 18:47:04
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/XZstNiHoZD
</td>
<td style="text-align:left;">
http://www.smart-r.net
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/923984409837162496/1509133757
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/923998501398351877/EXEH4wAz_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
923984409837162496
</td>
<td style="text-align:left;">
1035905864589303808
</td>
<td style="text-align:left;">
2018-09-01 15:02:58
</td>
<td style="text-align:left;">
smartR101
</td>
<td style="text-align:left;">
BIG thanks to Bob Jansen and \#amstRday for solving the hardest puzzles this \#satRday https://t.co/8Gaw4Sio9c, a lot to digest https://t.co/yIIWveIwKy
</td>
<td style="text-align:left;">
TweetDeck
</td>
<td style="text-align:right;">
125
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
amstRday, satRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
amsterdam2018.satrdays.org
</td>
<td style="text-align:left;">
https://t.co/8Gaw4Sio9c
</td>
<td style="text-align:left;">
https://amsterdam2018.satrdays.org/
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBGnLNW0AIB_U4.jpg
</td>
<td style="text-align:left;">
https://t.co/yIIWveIwKy
</td>
<td style="text-align:left;">
https://twitter.com/smartR101/status/1035905864589303808/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmBGnLNW0AIB_U4.jpg
</td>
<td style="text-align:left;">
https://t.co/yIIWveIwKy
</td>
<td style="text-align:left;">
https://twitter.com/smartR101/status/1035905864589303808/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/smartR101/status/1035905864589303808
</td>
<td style="text-align:left;">
smart-R
</td>
<td style="text-align:left;">
Hilversum, Nederlands
</td>
<td style="text-align:left;">
focused on increasing Roi through better business decisions directed by the Art of business & data Modeling, Statistics & open source Tools like R.
</td>
<td style="text-align:left;">
https://t.co/XZstNiHoZD
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:right;">
40
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
13
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
2017-10-27 18:47:04
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/XZstNiHoZD
</td>
<td style="text-align:left;">
http://www.smart-r.net
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/923984409837162496/1509133757
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/923998501398351877/EXEH4wAz_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
923984409837162496
</td>
<td style="text-align:left;">
1035898448359370758
</td>
<td style="text-align:left;">
2018-09-01 14:33:30
</td>
<td style="text-align:left;">
smartR101
</td>
<td style="text-align:left;">
Nice - mice::ampute now they also eat your data next to your cheese (at random and not at random) \#amstRday thanks to https://t.co/zRShbLhCJs https://t.co/iAMKjU6IUJ
</td>
<td style="text-align:left;">
TweetDeck
</td>
<td style="text-align:right;">
142
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
rianneschouten.github.io/mice_ampute/vi…
</td>
<td style="text-align:left;">
https://t.co/zRShbLhCJs
</td>
<td style="text-align:left;">
http://rianneschouten.github.io/mice_ampute/vignette/ampute.html
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA_o7nXgAEqO49.jpg
</td>
<td style="text-align:left;">
https://t.co/iAMKjU6IUJ
</td>
<td style="text-align:left;">
https://twitter.com/smartR101/status/1035898448359370758/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA_o7nXgAEqO49.jpg
</td>
<td style="text-align:left;">
https://t.co/iAMKjU6IUJ
</td>
<td style="text-align:left;">
https://twitter.com/smartR101/status/1035898448359370758/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/smartR101/status/1035898448359370758
</td>
<td style="text-align:left;">
smart-R
</td>
<td style="text-align:left;">
Hilversum, Nederlands
</td>
<td style="text-align:left;">
focused on increasing Roi through better business decisions directed by the Art of business & data Modeling, Statistics & open source Tools like R.
</td>
<td style="text-align:left;">
https://t.co/XZstNiHoZD
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:right;">
40
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
13
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
2017-10-27 18:47:04
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/XZstNiHoZD
</td>
<td style="text-align:left;">
http://www.smart-r.net
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/923984409837162496/1509133757
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/923998501398351877/EXEH4wAz_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
923984409837162496
</td>
<td style="text-align:left;">
1035870309721759745
</td>
<td style="text-align:left;">
2018-09-01 12:41:42
</td>
<td style="text-align:left;">
smartR101
</td>
<td style="text-align:left;">
50 Beautiful gRaphs by Thomas Hütter using (gg)-packages e.g. waterfall, treemap, ggradar  #amstRday slides to be published on https://t.co/8Gaw4Sio9c \#satRdays https://t.co/7YBuog5Huq
</td>
<td style="text-align:left;">
TweetDeck
</td>
<td style="text-align:right;">
160
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
amstRday, satRdays
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
amsterdam2018.satrdays.org
</td>
<td style="text-align:left;">
https://t.co/8Gaw4Sio9c
</td>
<td style="text-align:left;">
https://amsterdam2018.satrdays.org/
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAmA5pXoAI7C3p.jpg
</td>
<td style="text-align:left;">
https://t.co/7YBuog5Huq
</td>
<td style="text-align:left;">
https://twitter.com/smartR101/status/1035870309721759745/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAmA5pXoAI7C3p.jpg
</td>
<td style="text-align:left;">
https://t.co/7YBuog5Huq
</td>
<td style="text-align:left;">
https://twitter.com/smartR101/status/1035870309721759745/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/smartR101/status/1035870309721759745
</td>
<td style="text-align:left;">
smart-R
</td>
<td style="text-align:left;">
Hilversum, Nederlands
</td>
<td style="text-align:left;">
focused on increasing Roi through better business decisions directed by the Art of business & data Modeling, Statistics & open source Tools like R.
</td>
<td style="text-align:left;">
https://t.co/XZstNiHoZD
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:right;">
40
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
13
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
2017-10-27 18:47:04
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/XZstNiHoZD
</td>
<td style="text-align:left;">
http://www.smart-r.net
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/923984409837162496/1509133757
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/923998501398351877/EXEH4wAz_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
220099608
</td>
<td style="text-align:left;">
1035881665992773633
</td>
<td style="text-align:left;">
2018-09-01 13:26:49
</td>
<td style="text-align:left;">
RMHoge
</td>
<td style="text-align:left;">
After explaining text2vec, (**longhowlam?**) gives us an important lesson: “always check your results with the business, or in this case my wife” \#AmstRday https://t.co/HwQgzhK5Oj
</td>
<td style="text-align:left;">
Twitter Lite
</td>
<td style="text-align:right;">
149
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
AmstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAw4HuXoAIRRP1.jpg
</td>
<td style="text-align:left;">
https://t.co/HwQgzhK5Oj
</td>
<td style="text-align:left;">
https://twitter.com/RMHoge/status/1035881665992773633/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAw4HuXoAIRRP1.jpg
</td>
<td style="text-align:left;">
https://t.co/HwQgzhK5Oj
</td>
<td style="text-align:left;">
https://twitter.com/RMHoge/status/1035881665992773633/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
166540104
</td>
<td style="text-align:left;">
longhowlam
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/RMHoge/status/1035881665992773633
</td>
<td style="text-align:left;">
Roel
</td>
<td style="text-align:left;">
Leiden
</td>
<td style="text-align:left;">

I build silly rstats packages, data-science, https://t.co/sAKycT5zyA

Friend of DeSoto
</td>
<td style="text-align:left;">
https://t.co/SbnUhBcD9L
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
187
</td>
<td style="text-align:right;">
812
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
1157
</td>
<td style="text-align:right;">
2037
</td>
<td style="text-align:left;">
2010-11-26 19:46:55
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/SbnUhBcD9L
</td>
<td style="text-align:left;">
http://rmhogervorst.nl
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/220099608/1487413689
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme3/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/832899187566080000/CyyCNvC7_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
220099608
</td>
<td style="text-align:left;">
1035536200487063554
</td>
<td style="text-align:left;">
2018-08-31 14:34:04
</td>
<td style="text-align:left;">
RMHoge
</td>
<td style="text-align:left;">
The \#amstRday is on its way! Today tutorials, tomorrow speakers and on sunday we can hack together, for instance to create \#rstats 📦.  
(**satRdays_org?**) https://t.co/2aG87Q1Sur https://t.co/TnEVyVvjCE
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
173
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
TRUE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
amsterdam2018.satrdays.org , twitter.com/Janinekhuc/sta…
</td>
<td style="text-align:left;">
https://t.co/2aG87Q1Sur, https://t.co/TnEVyVvjCE
</td>
<td style="text-align:left;">
http://amsterdam2018.satrdays.org/ , https://twitter.com/Janinekhuc/status/1035479480230440960
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
737390070252998656
</td>
<td style="text-align:left;">
satRdays_org
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
1035479480230440960
</td>
<td style="text-align:left;">
Excited to kick off the first \#satRdays in Amsterdam. Follow \#amstRday for updates over the weekend- brilliant minds coming together to learn, teach and discuss \#rstats https://t.co/19lOvaxhD9
</td>
<td style="text-align:left;">
2018-08-31 10:48:41
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
12
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/RMHoge/status/1035536200487063554
</td>
<td style="text-align:left;">
Roel
</td>
<td style="text-align:left;">
Leiden
</td>
<td style="text-align:left;">

I build silly rstats packages, data-science, https://t.co/sAKycT5zyA

Friend of DeSoto
</td>
<td style="text-align:left;">
https://t.co/SbnUhBcD9L
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
187
</td>
<td style="text-align:right;">
812
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
1157
</td>
<td style="text-align:right;">
2037
</td>
<td style="text-align:left;">
2010-11-26 19:46:55
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/SbnUhBcD9L
</td>
<td style="text-align:left;">
http://rmhogervorst.nl
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/220099608/1487413689
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme3/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/832899187566080000/CyyCNvC7_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
220099608
</td>
<td style="text-align:left;">
1035904185785573378
</td>
<td style="text-align:left;">
2018-09-01 14:56:18
</td>
<td style="text-align:left;">
RMHoge
</td>
<td style="text-align:left;">
Bob Jansen: Solved the world’s hardest sudoku within a minute with pure R. And thought: that can be done faster. Let’s use Rcpp! \#AmstRday
</td>
<td style="text-align:left;">
Twitter Lite
</td>
<td style="text-align:right;">
138
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/RMHoge/status/1035904185785573378
</td>
<td style="text-align:left;">
Roel
</td>
<td style="text-align:left;">
Leiden
</td>
<td style="text-align:left;">

I build silly rstats packages, data-science, https://t.co/sAKycT5zyA

Friend of DeSoto
</td>
<td style="text-align:left;">
https://t.co/SbnUhBcD9L
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
187
</td>
<td style="text-align:right;">
812
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
1157
</td>
<td style="text-align:right;">
2037
</td>
<td style="text-align:left;">
2010-11-26 19:46:55
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/SbnUhBcD9L
</td>
<td style="text-align:left;">
http://rmhogervorst.nl
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/220099608/1487413689
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme3/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/832899187566080000/CyyCNvC7_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
220099608
</td>
<td style="text-align:left;">
1035829001225465856
</td>
<td style="text-align:left;">
2018-09-01 09:57:33
</td>
<td style="text-align:left;">
RMHoge
</td>
<td style="text-align:left;">
Dominik Krzemiński assures us that we can now translate your shiny apps to klingon (or other languages if you’d like) \#rstats \#amstRday https://t.co/8yyuwLWEFs
</td>
<td style="text-align:left;">
Twitter Lite
</td>
<td style="text-align:right;">
135
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
rstats , amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAA-sUXgAA5Njp.jpg
</td>
<td style="text-align:left;">
https://t.co/8yyuwLWEFs
</td>
<td style="text-align:left;">
https://twitter.com/RMHoge/status/1035829001225465856/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAA-sUXgAA5Njp.jpg
</td>
<td style="text-align:left;">
https://t.co/8yyuwLWEFs
</td>
<td style="text-align:left;">
https://twitter.com/RMHoge/status/1035829001225465856/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/RMHoge/status/1035829001225465856
</td>
<td style="text-align:left;">
Roel
</td>
<td style="text-align:left;">
Leiden
</td>
<td style="text-align:left;">

I build silly rstats packages, data-science, https://t.co/sAKycT5zyA

Friend of DeSoto
</td>
<td style="text-align:left;">
https://t.co/SbnUhBcD9L
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
187
</td>
<td style="text-align:right;">
812
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
1157
</td>
<td style="text-align:right;">
2037
</td>
<td style="text-align:left;">
2010-11-26 19:46:55
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/SbnUhBcD9L
</td>
<td style="text-align:left;">
http://rmhogervorst.nl
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/220099608/1487413689
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme3/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/832899187566080000/CyyCNvC7_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
220099608
</td>
<td style="text-align:left;">
1035876224730652673
</td>
<td style="text-align:left;">
2018-09-01 13:05:12
</td>
<td style="text-align:left;">
RMHoge
</td>
<td style="text-align:left;">

Rita slashes through shopping lists with R.

Regular expressions made easy by Rita Giordano \#AmstRday
</td>
<td style="text-align:left;">
Twitter Lite
</td>
<td style="text-align:right;">
102
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/RMHoge/status/1035876224730652673
</td>
<td style="text-align:left;">
Roel
</td>
<td style="text-align:left;">
Leiden
</td>
<td style="text-align:left;">

I build silly rstats packages, data-science, https://t.co/sAKycT5zyA

Friend of DeSoto
</td>
<td style="text-align:left;">
https://t.co/SbnUhBcD9L
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
187
</td>
<td style="text-align:right;">
812
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
1157
</td>
<td style="text-align:right;">
2037
</td>
<td style="text-align:left;">
2010-11-26 19:46:55
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/SbnUhBcD9L
</td>
<td style="text-align:left;">
http://rmhogervorst.nl
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/220099608/1487413689
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme3/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/832899187566080000/CyyCNvC7_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
220099608
</td>
<td style="text-align:left;">
1035550831964246022
</td>
<td style="text-align:left;">
2018-08-31 15:32:12
</td>
<td style="text-align:left;">
RMHoge
</td>
<td style="text-align:left;">

Did I just tweet the entire Saturday program for \#amstRday ? 🙀

Yes! https://t.co/BfP60hVWyp
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
68
</td>
<td style="text-align:left;">
1035549784084492290
</td>
<td style="text-align:left;">
220099608
</td>
<td style="text-align:left;">
RMHoge
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/tweet_video_thumb/Dl8Dv2BU8AEH6RQ.jpg
</td>
<td style="text-align:left;">
https://t.co/BfP60hVWyp
</td>
<td style="text-align:left;">
https://twitter.com/RMHoge/status/1035550831964246022/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/tweet_video_thumb/Dl8Dv2BU8AEH6RQ.jpg
</td>
<td style="text-align:left;">
https://t.co/BfP60hVWyp
</td>
<td style="text-align:left;">
https://twitter.com/RMHoge/status/1035550831964246022/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/RMHoge/status/1035550831964246022
</td>
<td style="text-align:left;">
Roel
</td>
<td style="text-align:left;">
Leiden
</td>
<td style="text-align:left;">

I build silly rstats packages, data-science, https://t.co/sAKycT5zyA

Friend of DeSoto
</td>
<td style="text-align:left;">
https://t.co/SbnUhBcD9L
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
187
</td>
<td style="text-align:right;">
812
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
1157
</td>
<td style="text-align:right;">
2037
</td>
<td style="text-align:left;">
2010-11-26 19:46:55
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/SbnUhBcD9L
</td>
<td style="text-align:left;">
http://rmhogervorst.nl
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/220099608/1487413689
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme3/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/832899187566080000/CyyCNvC7_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
978906818591240193
</td>
<td style="text-align:left;">
1035897434268987392
</td>
<td style="text-align:left;">
2018-09-01 14:29:29
</td>
<td style="text-align:left;">
stephanievdpas
</td>
<td style="text-align:left;">
What a great \#amstRday! Featuring Science Gossip (the journal! great find by (**dataandme?**)), the bang bang operator (**suzanbaert?**), and an entertaining talk on Non-Standard Evaluation by (**edwin_thoen?**)! https://t.co/KMWLCyOPNx
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
194
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
20
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA-\_idXsAET-Rr.jpg
</td>
<td style="text-align:left;">
https://t.co/KMWLCyOPNx
</td>
<td style="text-align:left;">
https://twitter.com/stephanievdpas/status/1035897434268987392/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA-\_idXsAET-Rr.jpg, http://pbs.twimg.com/media/DmA_AL8W0AAlwUU.jpg, http://pbs.twimg.com/media/DmA_A1eX0AAEDSl.jpg
</td>
<td style="text-align:left;">
https://t.co/KMWLCyOPNx, https://t.co/KMWLCyOPNx, https://t.co/KMWLCyOPNx
</td>
<td style="text-align:left;">
https://twitter.com/stephanievdpas/status/1035897434268987392/photo/1, https://twitter.com/stephanievdpas/status/1035897434268987392/photo/1, https://twitter.com/stephanievdpas/status/1035897434268987392/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3230388598 , 931042575158513664, 1570032288
</td>
<td style="text-align:left;">
dataandme , SuzanBaert , edwin_thoen
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/stephanievdpas/status/1035897434268987392
</td>
<td style="text-align:left;">
Stéphanie van der Pas
</td>
<td style="text-align:left;">
Leiden, Nederlands
</td>
<td style="text-align:left;">
Assistant professor in Statistics at Leiden University.
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
57
</td>
<td style="text-align:right;">
139
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
78
</td>
<td style="text-align:right;">
114
</td>
<td style="text-align:left;">
2018-03-28 08:09:07
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/990853991084019712/lOBvZvAq_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
1354498236
</td>
<td style="text-align:left;">
1035854045255294977
</td>
<td style="text-align:left;">
2018-09-01 11:37:04
</td>
<td style="text-align:left;">
StevenNooijen
</td>
<td style="text-align:left;">
Dusted off my account especially to Tweet about \#amstRday today! Great to have about a 100 R lovers here, of which 14 awesome speakers 🎉 https://t.co/c6JXcRZWB5
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
136
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
9
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAXwasXsAAgokx.jpg
</td>
<td style="text-align:left;">
https://t.co/c6JXcRZWB5
</td>
<td style="text-align:left;">
https://twitter.com/StevenNooijen/status/1035854045255294977/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAXwasXsAAgokx.jpg
</td>
<td style="text-align:left;">
https://t.co/c6JXcRZWB5
</td>
<td style="text-align:left;">
https://twitter.com/StevenNooijen/status/1035854045255294977/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/StevenNooijen/status/1035854045255294977
</td>
<td style="text-align:left;">
Steven Nooijen
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Data and Travel enthousiast
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
20
</td>
<td style="text-align:right;">
96
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
12
</td>
<td style="text-align:left;">
2013-04-15 14:37:30
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1354498236/1535956008
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1036499367883100160/wv56JPq7_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
1354498236
</td>
<td style="text-align:left;">
1035895164089319424
</td>
<td style="text-align:left;">
2018-09-01 14:20:27
</td>
<td style="text-align:left;">
StevenNooijen
</td>
<td style="text-align:left;">
Always good to think about why data is missing, and what’s the reason for it. Great talk (**RianneSchouten?**) \#amstRday https://t.co/ePZETdGvWB
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
114
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA9KDTX0AEqN3e.jpg
</td>
<td style="text-align:left;">
https://t.co/ePZETdGvWB
</td>
<td style="text-align:left;">
https://twitter.com/StevenNooijen/status/1035895164089319424/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA9KDTX0AEqN3e.jpg
</td>
<td style="text-align:left;">
https://t.co/ePZETdGvWB
</td>
<td style="text-align:left;">
https://twitter.com/StevenNooijen/status/1035895164089319424/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
150661626
</td>
<td style="text-align:left;">
RianneSchouten
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/StevenNooijen/status/1035895164089319424
</td>
<td style="text-align:left;">
Steven Nooijen
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Data and Travel enthousiast
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
20
</td>
<td style="text-align:right;">
96
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
12
</td>
<td style="text-align:left;">
2013-04-15 14:37:30
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1354498236/1535956008
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1036499367883100160/wv56JPq7_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
1035829603846303744
</td>
<td style="text-align:left;">
2018-09-01 09:59:56
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
Shiny apps with multiple languages? 😱😱😱😱. I love it. Great talk by Dominik Krzemiński! \#amstRday https://t.co/blJ3SxKigc
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
96
</td>
<td style="text-align:left;">
1035809288650977281
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmABg9dX0AEzBly.jpg
</td>
<td style="text-align:left;">
https://t.co/blJ3SxKigc
</td>
<td style="text-align:left;">
https://twitter.com/SuzanBaert/status/1035829603846303744/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmABg9dX0AEzBly.jpg, http://pbs.twimg.com/media/DmABhq_W4AEOmsx.jpg
</td>
<td style="text-align:left;">
https://t.co/blJ3SxKigc, https://t.co/blJ3SxKigc
</td>
<td style="text-align:left;">
https://twitter.com/SuzanBaert/status/1035829603846303744/photo/1, https://twitter.com/SuzanBaert/status/1035829603846303744/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
pl
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/SuzanBaert/status/1035829603846303744
</td>
<td style="text-align:left;">
Suzan Baert
</td>
<td style="text-align:left;">
Belgium
</td>
<td style="text-align:left;">
BI and analytics consultant, NASA datanaut, general data and \#rstats enthusiast. Part of \#rladies and \#rweekly.
</td>
<td style="text-align:left;">
https://t.co/byEmdn1bk6
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
988
</td>
<td style="text-align:right;">
406
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:right;">
623
</td>
<td style="text-align:right;">
3349
</td>
<td style="text-align:left;">
2017-11-16 06:13:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/byEmdn1bk6
</td>
<td style="text-align:left;">
http://suzan.rbind.io
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/931042575158513664/1510938661
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/931044588197998592/nL4heSc9_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
1035891790539317249
</td>
<td style="text-align:left;">
2018-09-01 14:07:03
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
Spreading the hex sticker love at \#AmstRday !! 🎉🎉 (**rweekly_org?**) (**RLadiesGlobal?**) https://t.co/QbIcK2sXF4
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
77
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
27
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
AmstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA6FdKWsAEQv_6.jpg
</td>
<td style="text-align:left;">
https://t.co/QbIcK2sXF4
</td>
<td style="text-align:left;">
https://twitter.com/SuzanBaert/status/1035891790539317249/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA6FdKWsAEQv_6.jpg
</td>
<td style="text-align:left;">
https://t.co/QbIcK2sXF4
</td>
<td style="text-align:left;">
https://twitter.com/SuzanBaert/status/1035891790539317249/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
733994123678490625, 770490229769789440
</td>
<td style="text-align:left;">
rweekly_org , RLadiesGlobal
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/SuzanBaert/status/1035891790539317249
</td>
<td style="text-align:left;">
Suzan Baert
</td>
<td style="text-align:left;">
Belgium
</td>
<td style="text-align:left;">
BI and analytics consultant, NASA datanaut, general data and \#rstats enthusiast. Part of \#rladies and \#rweekly.
</td>
<td style="text-align:left;">
https://t.co/byEmdn1bk6
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
988
</td>
<td style="text-align:right;">
406
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:right;">
623
</td>
<td style="text-align:right;">
3349
</td>
<td style="text-align:left;">
2017-11-16 06:13:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/byEmdn1bk6
</td>
<td style="text-align:left;">
http://suzan.rbind.io
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/931042575158513664/1510938661
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/931044588197998592/nL4heSc9_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
1035808540286492672
</td>
<td style="text-align:left;">
2018-09-01 08:36:15
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
Also love the quote (**dataandme?**) shared on being kind to beginners \#amstRday https://t.co/1NACHNncVG
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
74
</td>
<td style="text-align:left;">
1035807913783250944
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
15
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_uXQNX4AAnspG.jpg
</td>
<td style="text-align:left;">
https://t.co/1NACHNncVG
</td>
<td style="text-align:left;">
https://twitter.com/SuzanBaert/status/1035808540286492672/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_uXQNX4AAnspG.jpg
</td>
<td style="text-align:left;">
https://t.co/1NACHNncVG
</td>
<td style="text-align:left;">
https://twitter.com/SuzanBaert/status/1035808540286492672/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/SuzanBaert/status/1035808540286492672
</td>
<td style="text-align:left;">
Suzan Baert
</td>
<td style="text-align:left;">
Belgium
</td>
<td style="text-align:left;">
BI and analytics consultant, NASA datanaut, general data and \#rstats enthusiast. Part of \#rladies and \#rweekly.
</td>
<td style="text-align:left;">
https://t.co/byEmdn1bk6
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
988
</td>
<td style="text-align:right;">
406
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:right;">
623
</td>
<td style="text-align:right;">
3349
</td>
<td style="text-align:left;">
2017-11-16 06:13:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/byEmdn1bk6
</td>
<td style="text-align:left;">
http://suzan.rbind.io
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/931042575158513664/1510938661
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/931044588197998592/nL4heSc9_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
1035868571270873094
</td>
<td style="text-align:left;">
2018-09-01 12:34:47
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
(**edwin_thoen?**) working through a big cold to share something not quite that straightforward. \#hatsoff \#AmstRday https://t.co/TI658PtSze
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
109
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
1570032288
</td>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
hatsoff , AmstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAk-CwX4AASvG7.jpg
</td>
<td style="text-align:left;">
https://t.co/TI658PtSze
</td>
<td style="text-align:left;">
https://twitter.com/SuzanBaert/status/1035868571270873094/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAk-CwX4AASvG7.jpg
</td>
<td style="text-align:left;">
https://t.co/TI658PtSze
</td>
<td style="text-align:left;">
https://twitter.com/SuzanBaert/status/1035868571270873094/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
1570032288
</td>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/SuzanBaert/status/1035868571270873094
</td>
<td style="text-align:left;">
Suzan Baert
</td>
<td style="text-align:left;">
Belgium
</td>
<td style="text-align:left;">
BI and analytics consultant, NASA datanaut, general data and \#rstats enthusiast. Part of \#rladies and \#rweekly.
</td>
<td style="text-align:left;">
https://t.co/byEmdn1bk6
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
988
</td>
<td style="text-align:right;">
406
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:right;">
623
</td>
<td style="text-align:right;">
3349
</td>
<td style="text-align:left;">
2017-11-16 06:13:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/byEmdn1bk6
</td>
<td style="text-align:left;">
http://suzan.rbind.io
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/931042575158513664/1510938661
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/931044588197998592/nL4heSc9_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
1035809288650977281
</td>
<td style="text-align:left;">
2018-09-01 08:39:13
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
For people who don’t know SQL, or are learning it, (**krlmlr?**) shared a nice trick to get a query from R code with dbplyr \#amstRday https://t.co/E9tOZFdjko
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
127
</td>
<td style="text-align:left;">
1035808540286492672
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_vDcPXcAA5XyL.jpg
</td>
<td style="text-align:left;">
https://t.co/E9tOZFdjko
</td>
<td style="text-align:left;">
https://twitter.com/SuzanBaert/status/1035809288650977281/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_vDcPXcAA5XyL.jpg
</td>
<td style="text-align:left;">
https://t.co/E9tOZFdjko
</td>
<td style="text-align:left;">
https://twitter.com/SuzanBaert/status/1035809288650977281/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3354999513
</td>
<td style="text-align:left;">
krlmlr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/SuzanBaert/status/1035809288650977281
</td>
<td style="text-align:left;">
Suzan Baert
</td>
<td style="text-align:left;">
Belgium
</td>
<td style="text-align:left;">
BI and analytics consultant, NASA datanaut, general data and \#rstats enthusiast. Part of \#rladies and \#rweekly.
</td>
<td style="text-align:left;">
https://t.co/byEmdn1bk6
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
988
</td>
<td style="text-align:right;">
406
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:right;">
623
</td>
<td style="text-align:right;">
3349
</td>
<td style="text-align:left;">
2017-11-16 06:13:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/byEmdn1bk6
</td>
<td style="text-align:left;">
http://suzan.rbind.io
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/931042575158513664/1510938661
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/931044588197998592/nL4heSc9_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
1035807913783250944
</td>
<td style="text-align:left;">
2018-09-01 08:33:45
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
Two talks done at \#amstRday! (**dataandme?**) had a terrific talk showing how even the word “scientist” was controversial 🎉
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
117
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
13
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/SuzanBaert/status/1035807913783250944
</td>
<td style="text-align:left;">
Suzan Baert
</td>
<td style="text-align:left;">
Belgium
</td>
<td style="text-align:left;">
BI and analytics consultant, NASA datanaut, general data and \#rstats enthusiast. Part of \#rladies and \#rweekly.
</td>
<td style="text-align:left;">
https://t.co/byEmdn1bk6
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
988
</td>
<td style="text-align:right;">
406
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:right;">
623
</td>
<td style="text-align:right;">
3349
</td>
<td style="text-align:left;">
2017-11-16 06:13:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/byEmdn1bk6
</td>
<td style="text-align:left;">
http://suzan.rbind.io
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/931042575158513664/1510938661
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/931044588197998592/nL4heSc9_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
935995440792784900
</td>
<td style="text-align:left;">
1035821718575693824
</td>
<td style="text-align:left;">
2018-09-01 09:28:37
</td>
<td style="text-align:left;">
TheSarahStolle
</td>
<td style="text-align:left;">
R \#dplyr has bang bang 💥!! functions 💥!! 😄#awesomeR \#rstats \#amstRday (**SuzanBaert?**)
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
81
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
dplyr , awesomeR, rstats , amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/TheSarahStolle/status/1035821718575693824
</td>
<td style="text-align:left;">
Sarah Stolle
</td>
<td style="text-align:left;">
The Netherlands
</td>
<td style="text-align:left;">

Researcher of ageing, data visualization enthusiast, Phd candidate and incorrigible scientist. Leave my tea alone 🙃🌿

Header photo by Jason Leung on Unsplash
</td>
<td style="text-align:left;">
https://t.co/Sq2Y9HfxxI
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
66
</td>
<td style="text-align:right;">
217
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
92
</td>
<td style="text-align:right;">
201
</td>
<td style="text-align:left;">
2017-11-29 22:14:37
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/Sq2Y9HfxxI
</td>
<td style="text-align:left;">
https://www.linkedin.com/in/sarahstolle/
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/935995440792784900/1524063257
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/958343025666781184/Ra4-sYP1_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
935995440792784900
</td>
<td style="text-align:left;">
1035891111175315457
</td>
<td style="text-align:left;">
2018-09-01 14:04:21
</td>
<td style="text-align:left;">
TheSarahStolle
</td>
<td style="text-align:left;">
Promising title for the next \#amstRday talk 😂 https://t.co/nJseXTaXs9
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
45
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA5daZXoAYdlXK.jpg
</td>
<td style="text-align:left;">
https://t.co/nJseXTaXs9
</td>
<td style="text-align:left;">
https://twitter.com/TheSarahStolle/status/1035891111175315457/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmA5daZXoAYdlXK.jpg
</td>
<td style="text-align:left;">
https://t.co/nJseXTaXs9
</td>
<td style="text-align:left;">
https://twitter.com/TheSarahStolle/status/1035891111175315457/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/TheSarahStolle/status/1035891111175315457
</td>
<td style="text-align:left;">
Sarah Stolle
</td>
<td style="text-align:left;">
The Netherlands
</td>
<td style="text-align:left;">

Researcher of ageing, data visualization enthusiast, Phd candidate and incorrigible scientist. Leave my tea alone 🙃🌿

Header photo by Jason Leung on Unsplash
</td>
<td style="text-align:left;">
https://t.co/Sq2Y9HfxxI
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
66
</td>
<td style="text-align:right;">
217
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
92
</td>
<td style="text-align:right;">
201
</td>
<td style="text-align:left;">
2017-11-29 22:14:37
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/Sq2Y9HfxxI
</td>
<td style="text-align:left;">
https://www.linkedin.com/in/sarahstolle/
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/935995440792784900/1524063257
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/958343025666781184/Ra4-sYP1_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
935995440792784900
</td>
<td style="text-align:left;">
1035868919872086016
</td>
<td style="text-align:left;">
2018-09-01 12:36:10
</td>
<td style="text-align:left;">
TheSarahStolle
</td>
<td style="text-align:left;">
Great discovery for biological plots with large value differences
facet_zoom in ggforce \#ggplot2 \#rstats 😃 \#amstRday (**DerFredo?**) https://t.co/OTuRqpm42W
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
127
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
13
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
ggplot2 , rstats , amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAlSjSW0AEuNwZ.jpg
</td>
<td style="text-align:left;">
https://t.co/OTuRqpm42W
</td>
<td style="text-align:left;">
https://twitter.com/TheSarahStolle/status/1035868919872086016/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAlSjSW0AEuNwZ.jpg
</td>
<td style="text-align:left;">
https://t.co/OTuRqpm42W
</td>
<td style="text-align:left;">
https://twitter.com/TheSarahStolle/status/1035868919872086016/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/TheSarahStolle/status/1035868919872086016
</td>
<td style="text-align:left;">
Sarah Stolle
</td>
<td style="text-align:left;">
The Netherlands
</td>
<td style="text-align:left;">

Researcher of ageing, data visualization enthusiast, Phd candidate and incorrigible scientist. Leave my tea alone 🙃🌿

Header photo by Jason Leung on Unsplash
</td>
<td style="text-align:left;">
https://t.co/Sq2Y9HfxxI
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
66
</td>
<td style="text-align:right;">
217
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
92
</td>
<td style="text-align:right;">
201
</td>
<td style="text-align:left;">
2017-11-29 22:14:37
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/Sq2Y9HfxxI
</td>
<td style="text-align:left;">
https://www.linkedin.com/in/sarahstolle/
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/935995440792784900/1524063257
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/958343025666781184/Ra4-sYP1_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
25331832
</td>
<td style="text-align:left;">
1035817110981812224
</td>
<td style="text-align:left;">
2018-09-01 09:10:18
</td>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:left;">
.@SuzanBaert telling us about *scoped* dplyr functions. Nifty! \#AmstRday \#SatRday https://t.co/P7Cws7XTII
</td>
<td style="text-align:left;">
Twitter for iPad
</td>
<td style="text-align:right;">
81
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
AmstRday, SatRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_2KuHX0AArV49.jpg
</td>
<td style="text-align:left;">
https://t.co/P7Cws7XTII
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035817110981812224/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_2KuHX0AArV49.jpg
</td>
<td style="text-align:left;">
https://t.co/P7Cws7XTII
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035817110981812224/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035817110981812224
</td>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:left;">
Groningen
</td>
<td style="text-align:left;">
Open Data \| Open Algoritmes \| Geo-informatie \| Openbaar bestuur \| Mobiliteit
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1377
</td>
<td style="text-align:right;">
990
</td>
<td style="text-align:right;">
111
</td>
<td style="text-align:right;">
6622
</td>
<td style="text-align:right;">
958
</td>
<td style="text-align:left;">
2009-03-19 16:33:17
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
http://friesewoudloper.wordpress.com
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/25331832/1529010430
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
25331832
</td>
<td style="text-align:left;">
1035877184349642754
</td>
<td style="text-align:left;">
2018-09-01 13:09:01
</td>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:left;">
Now Rita Giordano’s lightning talk on regular expressions in R. “Learn RegEx. Do not copy, paste, remove… Use RegEx!” \#AmstRday \#SatRday https://t.co/e50SIDBLF5
</td>
<td style="text-align:left;">
Twitter for iPad
</td>
<td style="text-align:right;">
138
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRday, SatRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAszlJW4AA2F9j.jpg
</td>
<td style="text-align:left;">
https://t.co/e50SIDBLF5
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035877184349642754/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAszlJW4AA2F9j.jpg
</td>
<td style="text-align:left;">
https://t.co/e50SIDBLF5
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035877184349642754/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035877184349642754
</td>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:left;">
Groningen
</td>
<td style="text-align:left;">
Open Data \| Open Algoritmes \| Geo-informatie \| Openbaar bestuur \| Mobiliteit
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1377
</td>
<td style="text-align:right;">
990
</td>
<td style="text-align:right;">
111
</td>
<td style="text-align:right;">
6622
</td>
<td style="text-align:right;">
958
</td>
<td style="text-align:left;">
2009-03-19 16:33:17
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
http://friesewoudloper.wordpress.com
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/25331832/1529010430
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
25331832
</td>
<td style="text-align:left;">
1035786337205534721
</td>
<td style="text-align:left;">
2018-09-01 07:08:01
</td>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:left;">
Attending \#SatRday at (**GoDataDriven?**) in Amsterdam \#AmstRday \#R https://t.co/GJQAnsvP7g
</td>
<td style="text-align:left;">
Twitter for iPad
</td>
<td style="text-align:right;">
61
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
SatRday , AmstRday, R
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_aIC7X4AABkBS.jpg
</td>
<td style="text-align:left;">
https://t.co/GJQAnsvP7g
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035786337205534721/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_aIC7X4AABkBS.jpg
</td>
<td style="text-align:left;">
https://t.co/GJQAnsvP7g
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035786337205534721/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
1253544996
</td>
<td style="text-align:left;">
GoDataDriven
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035786337205534721
</td>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:left;">
Groningen
</td>
<td style="text-align:left;">
Open Data \| Open Algoritmes \| Geo-informatie \| Openbaar bestuur \| Mobiliteit
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1377
</td>
<td style="text-align:right;">
990
</td>
<td style="text-align:right;">
111
</td>
<td style="text-align:right;">
6622
</td>
<td style="text-align:right;">
958
</td>
<td style="text-align:left;">
2009-03-19 16:33:17
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
http://friesewoudloper.wordpress.com
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/25331832/1529010430
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
25331832
</td>
<td style="text-align:left;">
1035813276859420672
</td>
<td style="text-align:left;">
2018-09-01 08:55:04
</td>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:left;">
Next up, (**SuzanBaert?**)‘s talk on ’Getting more out of dplyr’ \#SatRday \#AmstRday https://t.co/5Qv75uwyzC
</td>
<td style="text-align:left;">
Twitter for iPad
</td>
<td style="text-align:right;">
77
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
SatRday , AmstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_yrhtX0AAfLU9.jpg
</td>
<td style="text-align:left;">
https://t.co/5Qv75uwyzC
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035813276859420672/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_yrhtX0AAfLU9.jpg
</td>
<td style="text-align:left;">
https://t.co/5Qv75uwyzC
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035813276859420672/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035813276859420672
</td>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:left;">
Groningen
</td>
<td style="text-align:left;">
Open Data \| Open Algoritmes \| Geo-informatie \| Openbaar bestuur \| Mobiliteit
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1377
</td>
<td style="text-align:right;">
990
</td>
<td style="text-align:right;">
111
</td>
<td style="text-align:right;">
6622
</td>
<td style="text-align:right;">
958
</td>
<td style="text-align:left;">
2009-03-19 16:33:17
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
http://friesewoudloper.wordpress.com
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/25331832/1529010430
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
25331832
</td>
<td style="text-align:left;">
1035867964715749376
</td>
<td style="text-align:left;">
2018-09-01 12:32:22
</td>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:left;">
You should check out the tmap package if you want to make beautiful maps in R https://t.co/hYORmmyTel \#SatRday \#AmstRday
</td>
<td style="text-align:left;">
Twitter for iPad
</td>
<td style="text-align:right;">
122
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
SatRday , AmstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
cran.r-project.org/web/packages/t…
</td>
<td style="text-align:left;">
https://t.co/hYORmmyTel
</td>
<td style="text-align:left;">
https://cran.r-project.org/web/packages/tmap/index.html
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035867964715749376
</td>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:left;">
Groningen
</td>
<td style="text-align:left;">
Open Data \| Open Algoritmes \| Geo-informatie \| Openbaar bestuur \| Mobiliteit
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1377
</td>
<td style="text-align:right;">
990
</td>
<td style="text-align:right;">
111
</td>
<td style="text-align:right;">
6622
</td>
<td style="text-align:right;">
958
</td>
<td style="text-align:left;">
2009-03-19 16:33:17
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
http://friesewoudloper.wordpress.com
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/25331832/1529010430
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
25331832
</td>
<td style="text-align:left;">
1035880863232352257
</td>
<td style="text-align:left;">
2018-09-01 13:23:38
</td>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:left;">
Two hobby projects from (**longhowlam?**) using the text2vec package https://t.co/mx3L3qUpdV &amp; https://t.co/enqIko18cR \#textmining \#AmstRday \#SatRday
</td>
<td style="text-align:left;">
Twitter for iPad
</td>
<td style="text-align:right;">
149
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
textmining, AmstRday , SatRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
github.com/longhowlam/jaap, github.com/longhowlam/tba…
</td>
<td style="text-align:left;">
https://t.co/mx3L3qUpdV, https://t.co/enqIko18cR
</td>
<td style="text-align:left;">
https://github.com/longhowlam/jaap , https://github.com/longhowlam/tbatb
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
166540104
</td>
<td style="text-align:left;">
longhowlam
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035880863232352257
</td>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:left;">
Groningen
</td>
<td style="text-align:left;">
Open Data \| Open Algoritmes \| Geo-informatie \| Openbaar bestuur \| Mobiliteit
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1377
</td>
<td style="text-align:right;">
990
</td>
<td style="text-align:right;">
111
</td>
<td style="text-align:right;">
6622
</td>
<td style="text-align:right;">
958
</td>
<td style="text-align:left;">
2009-03-19 16:33:17
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
http://friesewoudloper.wordpress.com
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/25331832/1529010430
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
25331832
</td>
<td style="text-align:left;">
1035805197967220736
</td>
<td style="text-align:left;">
2018-09-01 08:22:58
</td>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:left;">
Other R packages for working with databases in R mentioned by (**krlmlr?**) \#SatRday \#AmstRday https://t.co/qcNrP8g0xB
</td>
<td style="text-align:left;">
Twitter for iPad
</td>
<td style="text-align:right;">
88
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
SatRday , AmstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_rVUsXoAAB0At.jpg
</td>
<td style="text-align:left;">
https://t.co/qcNrP8g0xB
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035805197967220736/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_rVUsXoAAB0At.jpg
</td>
<td style="text-align:left;">
https://t.co/qcNrP8g0xB
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035805197967220736/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3354999513
</td>
<td style="text-align:left;">
krlmlr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035805197967220736
</td>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:left;">
Groningen
</td>
<td style="text-align:left;">
Open Data \| Open Algoritmes \| Geo-informatie \| Openbaar bestuur \| Mobiliteit
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1377
</td>
<td style="text-align:right;">
990
</td>
<td style="text-align:right;">
111
</td>
<td style="text-align:right;">
6622
</td>
<td style="text-align:right;">
958
</td>
<td style="text-align:left;">
2009-03-19 16:33:17
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
http://friesewoudloper.wordpress.com
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/25331832/1529010430
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
25331832
</td>
<td style="text-align:left;">
1035822832612204544
</td>
<td style="text-align:left;">
2018-09-01 09:33:02
</td>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:left;">
Check out these great tutorials by (**SuzanBaert?**): https://t.co/xThpY7UIZp Tomorrow her slides will also be online https://t.co/ELMuCaRXto \#AmstRday \#SatRday
</td>
<td style="text-align:left;">
Twitter for iPad
</td>
<td style="text-align:right;">
154
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
AmstRday, SatRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
suzan.rbind.io/categories/tut…, github.com/suzanbaert/Sat…
</td>
<td style="text-align:left;">
https://t.co/xThpY7UIZp, https://t.co/ELMuCaRXto
</td>
<td style="text-align:left;">
https://suzan.rbind.io/categories/tutorial/ , https://github.com/suzanbaert/SatRdaysAmsterdam18_dplyr
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035822832612204544
</td>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:left;">
Groningen
</td>
<td style="text-align:left;">
Open Data \| Open Algoritmes \| Geo-informatie \| Openbaar bestuur \| Mobiliteit
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1377
</td>
<td style="text-align:right;">
990
</td>
<td style="text-align:right;">
111
</td>
<td style="text-align:right;">
6622
</td>
<td style="text-align:right;">
958
</td>
<td style="text-align:left;">
2009-03-19 16:33:17
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
http://friesewoudloper.wordpress.com
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/25331832/1529010430
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
25331832
</td>
<td style="text-align:left;">
1035859393617833984
</td>
<td style="text-align:left;">
2018-09-01 11:58:19
</td>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:left;">
“What’s the fuzz about this R language?” answered by (**DerFredo?**) \#SatRday \#AmstRday https://t.co/sT3w6v2ZXX
</td>
<td style="text-align:left;">
Twitter for iPad
</td>
<td style="text-align:right;">
82
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
SatRday , AmstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAcnY2XcAA8pk8.jpg
</td>
<td style="text-align:left;">
https://t.co/sT3w6v2ZXX
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035859393617833984/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAcnY2XcAA8pk8.jpg
</td>
<td style="text-align:left;">
https://t.co/sT3w6v2ZXX
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035859393617833984/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
18238982
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035859393617833984
</td>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:left;">
Groningen
</td>
<td style="text-align:left;">
Open Data \| Open Algoritmes \| Geo-informatie \| Openbaar bestuur \| Mobiliteit
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1377
</td>
<td style="text-align:right;">
990
</td>
<td style="text-align:right;">
111
</td>
<td style="text-align:right;">
6622
</td>
<td style="text-align:right;">
958
</td>
<td style="text-align:left;">
2009-03-19 16:33:17
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
http://friesewoudloper.wordpress.com
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/25331832/1529010430
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
25331832
</td>
<td style="text-align:left;">
1035800743578673152
</td>
<td style="text-align:left;">
2018-09-01 08:05:16
</td>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:left;">
Next up, (**krlmlr?**) with his talk on the DBI package, R’s database interface https://t.co/9Q1Ua910cS \#AmstRday \#SatRday
</td>
<td style="text-align:left;">
Twitter for iPad
</td>
<td style="text-align:right;">
116
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRday, SatRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
cran.r-project.org/web/packages/D…
</td>
<td style="text-align:left;">
https://t.co/9Q1Ua910cS
</td>
<td style="text-align:left;">
https://cran.r-project.org/web/packages/DBI/DBI.pdf
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3354999513
</td>
<td style="text-align:left;">
krlmlr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035800743578673152
</td>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:left;">
Groningen
</td>
<td style="text-align:left;">
Open Data \| Open Algoritmes \| Geo-informatie \| Openbaar bestuur \| Mobiliteit
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1377
</td>
<td style="text-align:right;">
990
</td>
<td style="text-align:right;">
111
</td>
<td style="text-align:right;">
6622
</td>
<td style="text-align:right;">
958
</td>
<td style="text-align:left;">
2009-03-19 16:33:17
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
http://friesewoudloper.wordpress.com
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/25331832/1529010430
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
25331832
</td>
<td style="text-align:left;">
1035849423820087303
</td>
<td style="text-align:left;">
2018-09-01 11:18:42
</td>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:left;">
.@edwin_thoen: “Why should you care about how NSE (non-standard evaluation) works? because most R users slip into tool design sooner or later” \#SatRday \#AmstRday
</td>
<td style="text-align:left;">
Twitter for iPad
</td>
<td style="text-align:right;">
161
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
SatRday , AmstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
1570032288
</td>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035849423820087303
</td>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:left;">
Groningen
</td>
<td style="text-align:left;">
Open Data \| Open Algoritmes \| Geo-informatie \| Openbaar bestuur \| Mobiliteit
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1377
</td>
<td style="text-align:right;">
990
</td>
<td style="text-align:right;">
111
</td>
<td style="text-align:right;">
6622
</td>
<td style="text-align:right;">
958
</td>
<td style="text-align:left;">
2009-03-19 16:33:17
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
http://friesewoudloper.wordpress.com
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/25331832/1529010430
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
25331832
</td>
<td style="text-align:left;">
1035804426735378432
</td>
<td style="text-align:left;">
2018-09-01 08:19:54
</td>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:left;">
Easy access to databases in R with the dbplyr package: https://t.co/pPXkabCDiX \#AmstRday \#SatRday
</td>
<td style="text-align:left;">
Twitter for iPad
</td>
<td style="text-align:right;">
97
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRday, SatRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
cran.r-project.org/web/packages/d…
</td>
<td style="text-align:left;">
https://t.co/pPXkabCDiX
</td>
<td style="text-align:left;">
https://cran.r-project.org/web/packages/dbplyr/vignettes/dbplyr.html
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035804426735378432
</td>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:left;">
Groningen
</td>
<td style="text-align:left;">
Open Data \| Open Algoritmes \| Geo-informatie \| Openbaar bestuur \| Mobiliteit
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1377
</td>
<td style="text-align:right;">
990
</td>
<td style="text-align:right;">
111
</td>
<td style="text-align:right;">
6622
</td>
<td style="text-align:right;">
958
</td>
<td style="text-align:left;">
2009-03-19 16:33:17
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
http://friesewoudloper.wordpress.com
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/25331832/1529010430
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
25331832
</td>
<td style="text-align:left;">
1035884333972811778
</td>
<td style="text-align:left;">
2018-09-01 13:37:25
</td>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:left;">
Next up: (**sholderer?**) on the power of R Markdown in creating reports in MS Word \#RMD \#AmstRday \#SatRday https://t.co/0o08Yh13H1
</td>
<td style="text-align:left;">
Twitter for iPad
</td>
<td style="text-align:right;">
101
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
RMD , AmstRday, SatRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAzLSHX4AAFE58.jpg
</td>
<td style="text-align:left;">
https://t.co/0o08Yh13H1
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035884333972811778/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAzLSHX4AAFE58.jpg, http://pbs.twimg.com/media/DmAzLSNX4AAuM6P.jpg
</td>
<td style="text-align:left;">
https://t.co/0o08Yh13H1, https://t.co/0o08Yh13H1
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035884333972811778/photo/1, https://twitter.com/FrieseWoudloper/status/1035884333972811778/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
179263176
</td>
<td style="text-align:left;">
sholderer
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035884333972811778
</td>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:left;">
Groningen
</td>
<td style="text-align:left;">
Open Data \| Open Algoritmes \| Geo-informatie \| Openbaar bestuur \| Mobiliteit
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1377
</td>
<td style="text-align:right;">
990
</td>
<td style="text-align:right;">
111
</td>
<td style="text-align:right;">
6622
</td>
<td style="text-align:right;">
958
</td>
<td style="text-align:left;">
2009-03-19 16:33:17
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
http://friesewoudloper.wordpress.com
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/25331832/1529010430
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
184200446
</td>
<td style="text-align:left;">
1035804696617918469
</td>
<td style="text-align:left;">
2018-09-01 08:20:58
</td>
<td style="text-align:left;">
semakaran
</td>
<td style="text-align:left;">
\#amstRday \#rstats keynote talk from (**dataandme?**) 👩🏻‍💻🤗 https://t.co/YIfA6vn8fg
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
52
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
amstRday, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_q4PNXgAAtRer.jpg
</td>
<td style="text-align:left;">
https://t.co/YIfA6vn8fg
</td>
<td style="text-align:left;">
https://twitter.com/semakaran/status/1035804696617918469/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_q4PNXgAAtRer.jpg
</td>
<td style="text-align:left;">
https://t.co/YIfA6vn8fg
</td>
<td style="text-align:left;">
https://twitter.com/semakaran/status/1035804696617918469/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
https://api.twitter.com/1.1/geo/id/99cdab25eddd6bce.json
</td>
<td style="text-align:left;">
Amsterdam
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
city
</td>
<td style="text-align:left;">
The Netherlands
</td>
<td style="text-align:left;">
NL
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
4.728900, 5.079207, 5.079207, 4.728900, 52.278227, 52.278227, 52.431229, 52.431229
</td>
<td style="text-align:left;">
https://twitter.com/semakaran/status/1035804696617918469
</td>
<td style="text-align:left;">
sema
</td>
<td style="text-align:left;">
Amsterdam, Nederlands
</td>
<td style="text-align:left;">
Learning & growing with data🤓👩‍💻Analyst@Booking.com \| MSc Student in Data Science \| Tableau Public Featured Author \| R-Ladies Amsterdam \| NASA Datanaut
</td>
<td style="text-align:left;">
https://t.co/gnxfFtZA58
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
456
</td>
<td style="text-align:right;">
541
</td>
<td style="text-align:right;">
13
</td>
<td style="text-align:right;">
2882
</td>
<td style="text-align:right;">
1031
</td>
<td style="text-align:left;">
2010-08-28 23:34:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/gnxfFtZA58
</td>
<td style="text-align:left;">
https://dataception.wordpress.com
</td>
<td style="text-align:left;">
tr
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/184200446/1535912867
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/855440770517565441/TmHZUgIK_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
184200446
</td>
<td style="text-align:left;">
1035822711216513026
</td>
<td style="text-align:left;">
2018-09-01 09:32:33
</td>
<td style="text-align:left;">
semakaran
</td>
<td style="text-align:left;">
\#amstRday \#satRday we’ve “got more out of dplyr” thanks to (**SuzanBaert?**) ! https://t.co/UoGBtbXdQ5
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
72
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRday, satRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_7QXlW0AAC6fA.jpg
</td>
<td style="text-align:left;">
https://t.co/UoGBtbXdQ5
</td>
<td style="text-align:left;">
https://twitter.com/semakaran/status/1035822711216513026/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_7QXlW0AAC6fA.jpg
</td>
<td style="text-align:left;">
https://t.co/UoGBtbXdQ5
</td>
<td style="text-align:left;">
https://twitter.com/semakaran/status/1035822711216513026/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/semakaran/status/1035822711216513026
</td>
<td style="text-align:left;">
sema
</td>
<td style="text-align:left;">
Amsterdam, Nederlands
</td>
<td style="text-align:left;">
Learning & growing with data🤓👩‍💻Analyst@Booking.com \| MSc Student in Data Science \| Tableau Public Featured Author \| R-Ladies Amsterdam \| NASA Datanaut
</td>
<td style="text-align:left;">
https://t.co/gnxfFtZA58
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
456
</td>
<td style="text-align:right;">
541
</td>
<td style="text-align:right;">
13
</td>
<td style="text-align:right;">
2882
</td>
<td style="text-align:right;">
1031
</td>
<td style="text-align:left;">
2010-08-28 23:34:42
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/gnxfFtZA58
</td>
<td style="text-align:left;">
https://dataception.wordpress.com
</td>
<td style="text-align:left;">
tr
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/184200446/1535912867
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/855440770517565441/TmHZUgIK_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
976069167295197184
</td>
<td style="text-align:left;">
1035819845533749248
</td>
<td style="text-align:left;">
2018-09-01 09:21:10
</td>
<td style="text-align:left;">
IlsePit
</td>
<td style="text-align:left;">
(**SuzanBaert?**) casually blowing my mind by teaching us about scoped dplyr functions 🙌 \#amstRday \#satRdays \#rstats https://t.co/UqMCVbYRZm
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
110
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
16
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
amstRday, satRdays, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_4pGBXgAAMh8S.jpg
</td>
<td style="text-align:left;">
https://t.co/UqMCVbYRZm
</td>
<td style="text-align:left;">
https://twitter.com/IlsePit/status/1035819845533749248/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_4pGBXgAAMh8S.jpg
</td>
<td style="text-align:left;">
https://t.co/UqMCVbYRZm
</td>
<td style="text-align:left;">
https://twitter.com/IlsePit/status/1035819845533749248/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/IlsePit/status/1035819845533749248
</td>
<td style="text-align:left;">
Ilse Pit
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Methods and Statistics teacher at University of Amsterdam and co-organizer R-ladies Amsterdam. Lover of open science and cats.
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
81
</td>
<td style="text-align:right;">
80
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
159
</td>
<td style="text-align:right;">
370
</td>
<td style="text-align:left;">
2018-03-20 12:13:18
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/976070874880077824/P4p_7Xus_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
976069167295197184
</td>
<td style="text-align:left;">
1035516222866116608
</td>
<td style="text-align:left;">
2018-08-31 13:14:41
</td>
<td style="text-align:left;">
IlsePit
</td>
<td style="text-align:left;">
So hyped about this! (And less scared than I look, I promise :D ) \#amstRday https://t.co/bZ9LqxzLZB
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
75
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
TRUE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
twitter.com/Janinekhuc/sta…
</td>
<td style="text-align:left;">
https://t.co/bZ9LqxzLZB
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035507093283975170
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
1035507093283975170
</td>
<td style="text-align:left;">
Ready, set, go! Let’s get started with a fun weekend! A bunch of curious people ready to learn all about tidyverse &amp; webscraping! \#amstRdays \#rstats \#satRdays https://t.co/qjcuNFosdC
</td>
<td style="text-align:left;">
2018-08-31 12:38:24
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/IlsePit/status/1035516222866116608
</td>
<td style="text-align:left;">
Ilse Pit
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Methods and Statistics teacher at University of Amsterdam and co-organizer R-ladies Amsterdam. Lover of open science and cats.
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
81
</td>
<td style="text-align:right;">
80
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
159
</td>
<td style="text-align:right;">
370
</td>
<td style="text-align:left;">
2018-03-20 12:13:18
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/976070874880077824/P4p_7Xus_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
106091106
</td>
<td style="text-align:left;">
1035799538462806016
</td>
<td style="text-align:left;">
2018-09-01 08:00:28
</td>
<td style="text-align:left;">
Tesskorthout
</td>
<td style="text-align:left;">
Love it that (**dataandme?**) mentions my favorite podcast (**NSSDeviations?**) at \#amstRday! Would love to have (**hspter?**) and (**rdpeng?**) next year! \#rstats \#satRdays https://t.co/ARyrWx34JL
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
149
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
amstRday, rstats , satRdays
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_mLC6X0AAJXfh.jpg
</td>
<td style="text-align:left;">
https://t.co/ARyrWx34JL
</td>
<td style="text-align:left;">
https://twitter.com/Tesskorthout/status/1035799538462806016/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_mLC6X0AAJXfh.jpg
</td>
<td style="text-align:left;">
https://t.co/ARyrWx34JL
</td>
<td style="text-align:left;">
https://twitter.com/Tesskorthout/status/1035799538462806016/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3230388598, 3827302049, 24228154 , 9308212
</td>
<td style="text-align:left;">
dataandme , NSSDeviations, hspter , rdpeng
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Tesskorthout/status/1035799538462806016
</td>
<td style="text-align:left;">
Tess Korthout
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
PhD student, bioinformatics, epigenetics, co-founder (**RLadiesAMS?**)
</td>
<td style="text-align:left;">
https://t.co/VKBqNoVvdD
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
272
</td>
<td style="text-align:right;">
762
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
676
</td>
<td style="text-align:right;">
238
</td>
<td style="text-align:left;">
2010-01-18 13:31:51
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/VKBqNoVvdD
</td>
<td style="text-align:left;">
http://amsterdam2018.satrdays.org/
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/106091106/1531837339
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/781414975411724288/stts8RDZ_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
106091106
</td>
<td style="text-align:left;">
1035554309310693376
</td>
<td style="text-align:left;">
2018-08-31 15:46:01
</td>
<td style="text-align:left;">
Tesskorthout
</td>
<td style="text-align:left;">
So far the woRkshop is awesome! So excited for \#amstRday! https://t.co/zDCb9D5Gzo
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
57
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
TRUE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
twitter.com/Janinekhuc/sta…
</td>
<td style="text-align:left;">
https://t.co/zDCb9D5Gzo
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035479480230440960
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
1035479480230440960
</td>
<td style="text-align:left;">
Excited to kick off the first \#satRdays in Amsterdam. Follow \#amstRday for updates over the weekend- brilliant minds coming together to learn, teach and discuss \#rstats https://t.co/19lOvaxhD9
</td>
<td style="text-align:left;">
2018-08-31 10:48:41
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
12
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Tesskorthout/status/1035554309310693376
</td>
<td style="text-align:left;">
Tess Korthout
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
PhD student, bioinformatics, epigenetics, co-founder (**RLadiesAMS?**)
</td>
<td style="text-align:left;">
https://t.co/VKBqNoVvdD
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
272
</td>
<td style="text-align:right;">
762
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
676
</td>
<td style="text-align:right;">
238
</td>
<td style="text-align:left;">
2010-01-18 13:31:51
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/VKBqNoVvdD
</td>
<td style="text-align:left;">
http://amsterdam2018.satrdays.org/
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/106091106/1531837339
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/781414975411724288/stts8RDZ_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
1420994827
</td>
<td style="text-align:left;">
1035754506619940864
</td>
<td style="text-align:left;">
2018-09-01 05:01:32
</td>
<td style="text-align:left;">
TheStephLocke
</td>
<td style="text-align:left;">
Super excited today as \#SQLSatOslo and \#amstRday main events are happening. Big shout out to the organisers of both who’ve done amazing jobs - if you’re around you should thank them as it’s a purely volunteer role!
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
214
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
SQLSatOslo, amstRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/TheStephLocke/status/1035754506619940864
</td>
<td style="text-align:left;">
Steph Locke
</td>
<td style="text-align:left;">
Cardiff, UK
</td>
<td style="text-align:left;">
Leads (**LockeData?**) in \#dataScience & \#dataOps. (**microsoft?**) \#AI MVP. Builds communities: (**satrdays_org?**), (**msft_stack?**), (**cardiffrug?**)
</td>
<td style="text-align:left;">
https://t.co/k3gwlqktwL
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
4221
</td>
<td style="text-align:right;">
1678
</td>
<td style="text-align:right;">
328
</td>
<td style="text-align:right;">
13519
</td>
<td style="text-align:right;">
4414
</td>
<td style="text-align:left;">
2013-05-11 15:57:35
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/k3gwlqktwL
</td>
<td style="text-align:left;">
http://itsalocke.com
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1420994827/1535470643
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/971335139736346624/37TC7pkq_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
19766557
</td>
<td style="text-align:left;">
1037395125339672577
</td>
<td style="text-align:left;">
2018-09-05 17:40:46
</td>
<td style="text-align:left;">
Bootvis
</td>
<td style="text-align:left;">
My \#satrday presentation on using C++ to solve sudoku’s GitHub now:
https://t.co/sJnPZCVa4J (**satRdays_org?**) Please get in touch if you have any questions, feedbacks or other shouts.
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
180
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
satrday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
github.com/bobjansen/Rcpp…
</td>
<td style="text-align:left;">
https://t.co/sJnPZCVa4J
</td>
<td style="text-align:left;">
https://github.com/bobjansen/RcppSudoku
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
737390070252998656
</td>
<td style="text-align:left;">
satRdays_org
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Bootvis/status/1037395125339672577
</td>
<td style="text-align:left;">
Bob
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Hannibal
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
62
</td>
<td style="text-align:right;">
137
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:right;">
963
</td>
<td style="text-align:right;">
410
</td>
<td style="text-align:left;">
2009-01-30 13:16:08
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/733929214899027968/hoqAbzPo_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
1253544996
</td>
<td style="text-align:left;">
1036579543186849796
</td>
<td style="text-align:left;">
2018-09-03 11:39:56
</td>
<td style="text-align:left;">
GoDataDriven
</td>
<td style="text-align:left;">
(**edwin_thoen?**) Great to see that you liked it, Edwin. So did we, \#satRday Amsterdam might just become a regular thing.
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
103
</td>
<td style="text-align:left;">
1036324632884850690
</td>
<td style="text-align:left;">
1570032288
</td>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
satRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
1570032288
</td>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/GoDataDriven/status/1036579543186849796
</td>
<td style="text-align:left;">
GoDataDriven
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
We’re all about the DataDriven Enterprise. \#BigData Platform Implementations, \#Data Engineering and applied \#DataScience.
</td>
<td style="text-align:left;">
http://t.co/cXyUP5yZYX
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1670
</td>
<td style="text-align:right;">
901
</td>
<td style="text-align:right;">
137
</td>
<td style="text-align:right;">
1032
</td>
<td style="text-align:right;">
408
</td>
<td style="text-align:left;">
2013-03-09 06:14:18
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
http://t.co/cXyUP5yZYX
</td>
<td style="text-align:left;">
http://www.godatadriven.com/
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1253544996/1536304024
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1037959579185938432/BMCn_z6X_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
25331832
</td>
<td style="text-align:left;">
1035797417529102336
</td>
<td style="text-align:left;">
2018-09-01 07:52:03
</td>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:left;">
.@dataandme: “It’s important that newcomers contribute. We need people that contribute on all levels.” \#AmstRdam \#SatRday
</td>
<td style="text-align:left;">
Twitter for iPad
</td>
<td style="text-align:right;">
121
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRdam, SatRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035797417529102336
</td>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:left;">
Groningen
</td>
<td style="text-align:left;">
Open Data \| Open Algoritmes \| Geo-informatie \| Openbaar bestuur \| Mobiliteit
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1377
</td>
<td style="text-align:right;">
990
</td>
<td style="text-align:right;">
111
</td>
<td style="text-align:right;">
6622
</td>
<td style="text-align:right;">
958
</td>
<td style="text-align:left;">
2009-03-19 16:33:17
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
http://friesewoudloper.wordpress.com
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/25331832/1529010430
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
25331832
</td>
<td style="text-align:left;">
1035789286539513856
</td>
<td style="text-align:left;">
2018-09-01 07:19:44
</td>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:left;">
Kick-off with (**dataandme?**)‘s keynote telling us to ’LeaRn Out Loud’ \#AmstRdam \#SatRday https://t.co/33n5B1SVJu
</td>
<td style="text-align:left;">
Twitter for iPad
</td>
<td style="text-align:right;">
84
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRdam, SatRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_c2fBW0AACubq.jpg
</td>
<td style="text-align:left;">
https://t.co/33n5B1SVJu
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035789286539513856/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_c2fBW0AACubq.jpg
</td>
<td style="text-align:left;">
https://t.co/33n5B1SVJu
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035789286539513856/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035789286539513856
</td>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:left;">
Groningen
</td>
<td style="text-align:left;">
Open Data \| Open Algoritmes \| Geo-informatie \| Openbaar bestuur \| Mobiliteit
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1377
</td>
<td style="text-align:right;">
990
</td>
<td style="text-align:right;">
111
</td>
<td style="text-align:right;">
6622
</td>
<td style="text-align:right;">
958
</td>
<td style="text-align:left;">
2009-03-19 16:33:17
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
http://friesewoudloper.wordpress.com
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/25331832/1529010430
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
25331832
</td>
<td style="text-align:left;">
1035799092415348736
</td>
<td style="text-align:left;">
2018-09-01 07:58:42
</td>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:left;">
“What does doing data science look like?” (**rdpeng?**) wrote an interesting book on this topic: ‘Putting It All Together: Essays on Data Analysis’ https://t.co/8LiOE61oXc \#AmstRdam \#SatRDay
</td>
<td style="text-align:left;">
Twitter for iPad
</td>
<td style="text-align:right;">
184
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRdam, SatRDay
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
leanpub.com/dataanalysises…
</td>
<td style="text-align:left;">
https://t.co/8LiOE61oXc
</td>
<td style="text-align:left;">
https://leanpub.com/dataanalysisessays
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
9308212
</td>
<td style="text-align:left;">
rdpeng
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/FrieseWoudloper/status/1035799092415348736
</td>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:left;">
Groningen
</td>
<td style="text-align:left;">
Open Data \| Open Algoritmes \| Geo-informatie \| Openbaar bestuur \| Mobiliteit
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1377
</td>
<td style="text-align:right;">
990
</td>
<td style="text-align:right;">
111
</td>
<td style="text-align:right;">
6622
</td>
<td style="text-align:right;">
958
</td>
<td style="text-align:left;">
2009-03-19 16:33:17
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/uMLweYntDk
</td>
<td style="text-align:left;">
http://friesewoudloper.wordpress.com
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/25331832/1529010430
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
91104168
</td>
<td style="text-align:left;">
1035810580651810816
</td>
<td style="text-align:left;">
2018-09-01 08:44:21
</td>
<td style="text-align:left;">
RAPOSTHUMUS
</td>
<td style="text-align:left;">
Next up \#AmstRdam \#SatRday https://t.co/AnqE6gex5C
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
26
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRdam, SatRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_wOg0WwAEMS9r.jpg
</td>
<td style="text-align:left;">
https://t.co/AnqE6gex5C
</td>
<td style="text-align:left;">
https://twitter.com/RAPOSTHUMUS/status/1035810580651810816/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_wOg0WwAEMS9r.jpg
</td>
<td style="text-align:left;">
https://t.co/AnqE6gex5C
</td>
<td style="text-align:left;">
https://twitter.com/RAPOSTHUMUS/status/1035810580651810816/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/RAPOSTHUMUS/status/1035810580651810816
</td>
<td style="text-align:left;">
R.A. Posthumus
</td>
<td style="text-align:left;">
Zwolle
</td>
<td style="text-align:left;">
Prive account;IenW/RWS
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
470
</td>
<td style="text-align:right;">
947
</td>
<td style="text-align:right;">
530
</td>
<td style="text-align:right;">
14964
</td>
<td style="text-align:right;">
12080
</td>
<td style="text-align:left;">
2009-11-19 13:28:52
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/91104168/1514631916
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1124144375/rp_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
91104168
</td>
<td style="text-align:left;">
1035857585746927616
</td>
<td style="text-align:left;">
2018-09-01 11:51:08
</td>
<td style="text-align:left;">
RAPOSTHUMUS
</td>
<td style="text-align:left;">
50 ways… \#AmstRdam \#SatRday https://t.co/2LoUbz1qMX
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
29
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRdam, SatRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAa-iWX0AAJfLo.jpg
</td>
<td style="text-align:left;">
https://t.co/2LoUbz1qMX
</td>
<td style="text-align:left;">
https://twitter.com/RAPOSTHUMUS/status/1035857585746927616/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmAa-iWX0AAJfLo.jpg
</td>
<td style="text-align:left;">
https://t.co/2LoUbz1qMX
</td>
<td style="text-align:left;">
https://twitter.com/RAPOSTHUMUS/status/1035857585746927616/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/RAPOSTHUMUS/status/1035857585746927616
</td>
<td style="text-align:left;">
R.A. Posthumus
</td>
<td style="text-align:left;">
Zwolle
</td>
<td style="text-align:left;">
Prive account;IenW/RWS
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
470
</td>
<td style="text-align:right;">
947
</td>
<td style="text-align:right;">
530
</td>
<td style="text-align:right;">
14964
</td>
<td style="text-align:right;">
12080
</td>
<td style="text-align:left;">
2009-11-19 13:28:52
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/91104168/1514631916
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1124144375/rp_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
91104168
</td>
<td style="text-align:left;">
1035810260144070661
</td>
<td style="text-align:left;">
2018-09-01 08:43:05
</td>
<td style="text-align:left;">
RAPOSTHUMUS
</td>
<td style="text-align:left;">
(**jpagroenen?**) (**datafluisteraar?**) (**TransIP?**) Komt later zit nu bij \#AmstRdam \#SatRday
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
40
</td>
<td style="text-align:left;">
1035810108528369664
</td>
<td style="text-align:left;">
153201482
</td>
<td style="text-align:left;">
jpagroenen
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRdam, SatRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
153201482 , 3227592201, 28295885
</td>
<td style="text-align:left;">
jpagroenen , datafluisteraar, TransIP
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/RAPOSTHUMUS/status/1035810260144070661
</td>
<td style="text-align:left;">
R.A. Posthumus
</td>
<td style="text-align:left;">
Zwolle
</td>
<td style="text-align:left;">
Prive account;IenW/RWS
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
470
</td>
<td style="text-align:right;">
947
</td>
<td style="text-align:right;">
530
</td>
<td style="text-align:right;">
14964
</td>
<td style="text-align:right;">
12080
</td>
<td style="text-align:left;">
2009-11-19 13:28:52
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/91104168/1514631916
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1124144375/rp_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
91104168
</td>
<td style="text-align:left;">
1035807693800464384
</td>
<td style="text-align:left;">
2018-09-01 08:32:53
</td>
<td style="text-align:left;">
RAPOSTHUMUS
</td>
<td style="text-align:left;">
Yes there are stickers \#AmstRdam \#SatRday https://t.co/ncb8Zr8Y1l
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
41
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRdam, SatRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_tmZuXgAAIwsD.jpg
</td>
<td style="text-align:left;">
https://t.co/ncb8Zr8Y1l
</td>
<td style="text-align:left;">
https://twitter.com/RAPOSTHUMUS/status/1035807693800464384/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_tmZuXgAAIwsD.jpg
</td>
<td style="text-align:left;">
https://t.co/ncb8Zr8Y1l
</td>
<td style="text-align:left;">
https://twitter.com/RAPOSTHUMUS/status/1035807693800464384/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/RAPOSTHUMUS/status/1035807693800464384
</td>
<td style="text-align:left;">
R.A. Posthumus
</td>
<td style="text-align:left;">
Zwolle
</td>
<td style="text-align:left;">
Prive account;IenW/RWS
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
470
</td>
<td style="text-align:right;">
947
</td>
<td style="text-align:right;">
530
</td>
<td style="text-align:right;">
14964
</td>
<td style="text-align:right;">
12080
</td>
<td style="text-align:left;">
2009-11-19 13:28:52
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/91104168/1514631916
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1124144375/rp_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
91104168
</td>
<td style="text-align:left;">
1035824211917500416
</td>
<td style="text-align:left;">
2018-09-01 09:38:31
</td>
<td style="text-align:left;">
RAPOSTHUMUS
</td>
<td style="text-align:left;">
This wille interesting \#AmstRdam \#SatRday https://t.co/ioQ124aywn
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
41
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
AmstRdam, SatRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_8n5gX0AAbZLV.jpg
</td>
<td style="text-align:left;">
https://t.co/ioQ124aywn
</td>
<td style="text-align:left;">
https://twitter.com/RAPOSTHUMUS/status/1035824211917500416/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_8n5gX0AAbZLV.jpg
</td>
<td style="text-align:left;">
https://t.co/ioQ124aywn
</td>
<td style="text-align:left;">
https://twitter.com/RAPOSTHUMUS/status/1035824211917500416/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/RAPOSTHUMUS/status/1035824211917500416
</td>
<td style="text-align:left;">
R.A. Posthumus
</td>
<td style="text-align:left;">
Zwolle
</td>
<td style="text-align:left;">
Prive account;IenW/RWS
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
470
</td>
<td style="text-align:right;">
947
</td>
<td style="text-align:right;">
530
</td>
<td style="text-align:right;">
14964
</td>
<td style="text-align:right;">
12080
</td>
<td style="text-align:left;">
2009-11-19 13:28:52
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/91104168/1514631916
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1124144375/rp_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
714922299816853504
</td>
<td style="text-align:left;">
1035785540505874432
</td>
<td style="text-align:left;">
2018-09-01 07:04:51
</td>
<td style="text-align:left;">
oliverowner
</td>
<td style="text-align:left;">
This is amazing \#satRday
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
24
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
satRday
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/oliverowner/status/1035785540505874432
</td>
<td style="text-align:left;">
Gabriel
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
I currently no longer have an Oliver. I no longer have a James either so Amy is the last one left.
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
32
</td>
<td style="text-align:right;">
65
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
142
</td>
<td style="text-align:right;">
49
</td>
<td style="text-align:left;">
2016-03-29 21:08:53
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/714922299816853504/1465249466
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/743906145346129920/-a0c3u66_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
1291259790
</td>
<td style="text-align:left;">
1036168653950083072
</td>
<td style="text-align:left;">
2018-09-02 08:27:12
</td>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:left;">
(**RoryJosephQuinn?**) (**GalwayRusers?**) (**statsepi?**) (**jaynal83?**) A \#SatRdays in West of Ireland sometime? (**EngineLimerick?**) would make a nice venue https://t.co/DJAddmLyXS
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
131
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
2850269319
</td>
<td style="text-align:left;">
RoryJosephQuinn
</td>
<td style="text-align:left;">
TRUE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
SatRdays
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
twitter.com/romain_francoi…
</td>
<td style="text-align:left;">
https://t.co/DJAddmLyXS
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1035812809819521024
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
2850269319 , 964468230868865025, 197662233 , 398100183 , 966347586511736832
</td>
<td style="text-align:left;">
RoryJosephQuinn, GalwayRusers , statsepi , jaynal83 , EngineLimerick
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
1035812809819521024
</td>
<td style="text-align:left;">
Getting more out of \#dplyr, (**SuzanBaert?**) \#amstRday \#satrdays \#rstats \#tidyverse https://t.co/zLDLuXPnM9
</td>
<td style="text-align:left;">
2018-09-01 08:53:12
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
377578645
</td>
<td style="text-align:left;">
romain_francois
</td>
<td style="text-align:left;">
Romain François 🦄
</td>
<td style="text-align:right;">
5113
</td>
<td style="text-align:right;">
336
</td>
<td style="text-align:right;">
5837
</td>
<td style="text-align:left;">
France
</td>
<td style="text-align:left;">
👨‍💻 \#rstats 📦 with the \#tidyverse team.
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1036168653950083072
</td>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:left;">
Dublin, Ireland
</td>
<td style="text-align:left;">
Statistician and Coder - Data Sciences, Rstats, Python, Julia, MatLab, etc. (many tweets intended for my students)
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2844
</td>
<td style="text-align:right;">
2360
</td>
<td style="text-align:right;">
220
</td>
<td style="text-align:right;">
3547
</td>
<td style="text-align:right;">
4043
</td>
<td style="text-align:left;">
2013-03-23 12:10:36
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
https://www.linkedin.com/profile/view?id=14325915&trk=nav_responsive_tab_profile
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1291259790/1420153011
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/3427713318/840e4aa0a6dca9263a0507fbfe4c4074_normal.jpeg
</td>
</tr>
<tr>
<td style="text-align:left;">
1291259790
</td>
<td style="text-align:left;">
1035875496376991744
</td>
<td style="text-align:left;">
2018-09-01 13:02:18
</td>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:left;">
Regular Expressions with Rita Giordano @ \#SatRdays amsterdam https://t.co/Pao0ycriUz
</td>
<td style="text-align:left;">
Twitter Lite
</td>
<td style="text-align:right;">
60
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
SatRdays
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmArQcxW0AAASAY.jpg
</td>
<td style="text-align:left;">
https://t.co/Pao0ycriUz
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035875496376991744/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DmArQcxW0AAASAY.jpg, http://pbs.twimg.com/media/DmArQcwW0AEWoYR.jpg, http://pbs.twimg.com/media/DmArQc0X4AYsxd9.jpg
</td>
<td style="text-align:left;">
https://t.co/Pao0ycriUz, https://t.co/Pao0ycriUz, https://t.co/Pao0ycriUz
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035875496376991744/photo/1, https://twitter.com/dragonflystats/status/1035875496376991744/photo/1, https://twitter.com/dragonflystats/status/1035875496376991744/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/dragonflystats/status/1035875496376991744
</td>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:left;">
Dublin, Ireland
</td>
<td style="text-align:left;">
Statistician and Coder - Data Sciences, Rstats, Python, Julia, MatLab, etc. (many tweets intended for my students)
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2844
</td>
<td style="text-align:right;">
2360
</td>
<td style="text-align:right;">
220
</td>
<td style="text-align:right;">
3547
</td>
<td style="text-align:right;">
4043
</td>
<td style="text-align:left;">
2013-03-23 12:10:36
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/Y30wp2z2HL
</td>
<td style="text-align:left;">
https://www.linkedin.com/profile/view?id=14325915&trk=nav_responsive_tab_profile
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/1291259790/1420153011
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/3427713318/840e4aa0a6dca9263a0507fbfe4c4074_normal.jpeg
</td>
</tr>
<tr>
<td style="text-align:left;">
377578645
</td>
<td style="text-align:left;">
1035500746974945283
</td>
<td style="text-align:left;">
2018-08-31 12:13:11
</td>
<td style="text-align:left;">
romain_francois
</td>
<td style="text-align:left;">
Never too early to attend a \#satRdays \#rstats conference. \#rbaby 👶 https://t.co/gx7U8k3CVU
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
66
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
35
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
satRdays, rstats , rbaby
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl7WbzpX4AIiCiL.jpg
</td>
<td style="text-align:left;">
https://t.co/gx7U8k3CVU
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1035500746974945283/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl7WbzpX4AIiCiL.jpg, http://pbs.twimg.com/media/Dl7WbzpXoAAvzPE.jpg
</td>
<td style="text-align:left;">
https://t.co/gx7U8k3CVU, https://t.co/gx7U8k3CVU
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1035500746974945283/photo/1, https://twitter.com/romain_francois/status/1035500746974945283/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
https://api.twitter.com/1.1/geo/id/07d9f6d71c881000.json
</td>
<td style="text-align:left;">
UBER Amsterdam HQ
</td>
<td style="text-align:left;">
UBER Amsterdam HQ
</td>
<td style="text-align:left;">
poi
</td>
<td style="text-align:left;">
The Netherlands
</td>
<td style="text-align:left;">
NL
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
4.891585, 4.891585, 4.891585, 4.891585, 52.360512, 52.360512, 52.360512, 52.360512
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1035500746974945283
</td>
<td style="text-align:left;">
Romain François 🦄
</td>
<td style="text-align:left;">
France
</td>
<td style="text-align:left;">
👨‍💻 \#rstats 📦 with the \#tidyverse team.
</td>
<td style="text-align:left;">
https://t.co/8WIUhd0bJc
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5113
</td>
<td style="text-align:right;">
336
</td>
<td style="text-align:right;">
211
</td>
<td style="text-align:right;">
5837
</td>
<td style="text-align:right;">
5440
</td>
<td style="text-align:left;">
2011-09-21 20:02:22
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/8WIUhd0bJc
</td>
<td style="text-align:left;">
https://purrple.cat
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/377578645/1519142290
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/991018500591378432/U_9\_9qU-\_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
377578645
</td>
<td style="text-align:left;">
1034789475329691648
</td>
<td style="text-align:left;">
2018-08-29 13:06:51
</td>
<td style="text-align:left;">
romain_francois
</td>
<td style="text-align:left;">
Any \#rstats people going to \#satrdays with a stroller to lend for a few days? (**AirFranceKLM?**) lost ours between Nantes and Amsterdam 🤷‍♂️
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
135
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
rstats , satrdays
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3044797241
</td>
<td style="text-align:left;">
AirFranceKLM
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1034789475329691648
</td>
<td style="text-align:left;">
Romain François 🦄
</td>
<td style="text-align:left;">
France
</td>
<td style="text-align:left;">
👨‍💻 \#rstats 📦 with the \#tidyverse team.
</td>
<td style="text-align:left;">
https://t.co/8WIUhd0bJc
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5113
</td>
<td style="text-align:right;">
336
</td>
<td style="text-align:right;">
211
</td>
<td style="text-align:right;">
5837
</td>
<td style="text-align:right;">
5440
</td>
<td style="text-align:left;">
2011-09-21 20:02:22
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/8WIUhd0bJc
</td>
<td style="text-align:left;">
https://purrple.cat
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/377578645/1519142290
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/991018500591378432/U_9\_9qU-\_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035507093283975170
</td>
<td style="text-align:left;">
2018-08-31 12:38:24
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Ready, set, go! Let’s get started with a fun weekend! A bunch of curious people ready to learn all about tidyverse &amp; webscraping! \#amstRdays \#rstats \#satRdays https://t.co/qjcuNFosdC
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
164
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
amstRdays, rstats , satRdays
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl7cLx0WwAAa2p5.jpg
</td>
<td style="text-align:left;">
https://t.co/qjcuNFosdC
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035507093283975170/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl7cLx0WwAAa2p5.jpg, http://pbs.twimg.com/media/Dl7cLx2XoAE_4Ba.jpg, http://pbs.twimg.com/media/Dl7cLx3XsAABWHs.jpg
</td>
<td style="text-align:left;">
https://t.co/qjcuNFosdC, https://t.co/qjcuNFosdC, https://t.co/qjcuNFosdC
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035507093283975170/photo/1, https://twitter.com/Janinekhuc/status/1035507093283975170/photo/1, https://twitter.com/Janinekhuc/status/1035507093283975170/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035507093283975170
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
3808635677
</td>
<td style="text-align:left;">
1035539865788706816
</td>
<td style="text-align:left;">
2018-08-31 14:48:38
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Next up, Gilian Porte on scraping the internet with R. \#amstRdam \#satRdays \#rstats https://t.co/JwE2TRcujO
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
82
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
amstRdam, satRdays, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl76A00U4AEFqyz.jpg
</td>
<td style="text-align:left;">
https://t.co/JwE2TRcujO
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035539865788706816/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl76A00U4AEFqyz.jpg, http://pbs.twimg.com/media/Dl76A1JUcAItoDi.jpg
</td>
<td style="text-align:left;">
https://t.co/JwE2TRcujO, https://t.co/JwE2TRcujO
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035539865788706816/photo/1, https://twitter.com/Janinekhuc/status/1035539865788706816/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/Janinekhuc/status/1035539865788706816
</td>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
Aspiring behavioural Data Scientist, R-enthusiast, Co-Founder of (**RladiesAMS?**) & currently exploring causal inference for my thesis (**pacmedhealth?**)
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
168
</td>
<td style="text-align:right;">
234
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
232
</td>
<td style="text-align:right;">
360
</td>
<td style="text-align:left;">
2015-09-28 23:28:12
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en-gb
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/3808635677/1499856671
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
964088911
</td>
<td style="text-align:left;">
1035789843849207808
</td>
<td style="text-align:left;">
2018-09-01 07:21:57
</td>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:left;">
(**dataandme?**) Mara at \#satRdays \#SatRdayAmsterdam https://t.co/ruguTvAi0Z
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
46
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
satRdays , SatRdayAmsterdam
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_dXXrWwAAXavu.jpg
</td>
<td style="text-align:left;">
https://t.co/ruguTvAi0Z
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035789843849207808/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_dXXrWwAAXavu.jpg
</td>
<td style="text-align:left;">
https://t.co/ruguTvAi0Z
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035789843849207808/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3230388598
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
tl
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1035789843849207808
</td>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:left;">
Montpellier, France
</td>
<td style="text-align:left;">
\#rstats data scientist
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
163
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
117
</td>
<td style="text-align:right;">
383
</td>
<td style="text-align:left;">
2012-11-22 11:17:21
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
fr
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/964088911/1470756731
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/2881158206/bb964afd6af2d7beea05a5a2b9fec6af_normal.png
</td>
</tr>
<tr>
<td style="text-align:left;">
964088911
</td>
<td style="text-align:left;">
1034686865922764800
</td>
<td style="text-align:left;">
2018-08-29 06:19:07
</td>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:left;">
✈️➡️ \#satRdays Amsterdam https://t.co/uCxfPITLHm
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
24
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
16
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
satRdays
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DlvyMiAW0AAm-Ur.jpg
</td>
<td style="text-align:left;">
https://t.co/uCxfPITLHm
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1034686865922764800/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/DlvyMiAW0AAm-Ur.jpg
</td>
<td style="text-align:left;">
https://t.co/uCxfPITLHm
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1034686865922764800/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/cecilesauder/status/1034686865922764800
</td>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:left;">
Montpellier, France
</td>
<td style="text-align:left;">
\#rstats data scientist
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
104
</td>
<td style="text-align:right;">
163
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
117
</td>
<td style="text-align:right;">
383
</td>
<td style="text-align:left;">
2012-11-22 11:17:21
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
fr
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/964088911/1470756731
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/2881158206/bb964afd6af2d7beea05a5a2b9fec6af_normal.png
</td>
</tr>
<tr>
<td style="text-align:left;">
91104168
</td>
<td style="text-align:left;">
1035785194165469184
</td>
<td style="text-align:left;">
2018-09-01 07:03:28
</td>
<td style="text-align:left;">
RAPOSTHUMUS
</td>
<td style="text-align:left;">
En we gaan starten met \#satrdays amsterdsm https://t.co/XfJiZ3Fx5v
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
42
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
satrdays
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_ZG3lX0AAfwA-.jpg
</td>
<td style="text-align:left;">
https://t.co/XfJiZ3Fx5v
</td>
<td style="text-align:left;">
https://twitter.com/RAPOSTHUMUS/status/1035785194165469184/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_ZG3lX0AAfwA-.jpg
</td>
<td style="text-align:left;">
https://t.co/XfJiZ3Fx5v
</td>
<td style="text-align:left;">
https://twitter.com/RAPOSTHUMUS/status/1035785194165469184/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/RAPOSTHUMUS/status/1035785194165469184
</td>
<td style="text-align:left;">
R.A. Posthumus
</td>
<td style="text-align:left;">
Zwolle
</td>
<td style="text-align:left;">
Prive account;IenW/RWS
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
470
</td>
<td style="text-align:right;">
947
</td>
<td style="text-align:right;">
530
</td>
<td style="text-align:right;">
14964
</td>
<td style="text-align:right;">
12080
</td>
<td style="text-align:left;">
2009-11-19 13:28:52
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
nl
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/91104168/1514631916
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1124144375/rp_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
296664658
</td>
<td style="text-align:left;">
1035514892529352704
</td>
<td style="text-align:left;">
2018-08-31 13:09:23
</td>
<td style="text-align:left;">
matlabulous
</td>
<td style="text-align:left;">
.@satRdays_org workshop (**UberAmsterdam?**) \#satRdays \#satRdayAMS https://t.co/XxHW1Etym5
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
60
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
satRdays , satRdayAMS
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl7jTNjUcAA9XUe.jpg
</td>
<td style="text-align:left;">
https://t.co/XxHW1Etym5
</td>
<td style="text-align:left;">
https://twitter.com/matlabulous/status/1035514892529352704/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl7jTNjUcAA9XUe.jpg
</td>
<td style="text-align:left;">
https://t.co/XxHW1Etym5
</td>
<td style="text-align:left;">
https://twitter.com/matlabulous/status/1035514892529352704/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
737390070252998656, 297017781
</td>
<td style="text-align:left;">
satRdays_org , UberAmsterdam
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
https://api.twitter.com/1.1/geo/id/07d9f6d71c881000.json
</td>
<td style="text-align:left;">
UBER Amsterdam HQ
</td>
<td style="text-align:left;">
UBER Amsterdam HQ
</td>
<td style="text-align:left;">
poi
</td>
<td style="text-align:left;">
The Netherlands
</td>
<td style="text-align:left;">
NL
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
4.891585, 4.891585, 4.891585, 4.891585, 52.360512, 52.360512, 52.360512, 52.360512
</td>
<td style="text-align:left;">
https://twitter.com/matlabulous/status/1035514892529352704
</td>
<td style="text-align:left;">
Jo-fai (Joe) Chow
</td>
<td style="text-align:left;">
🇬🇧🇺🇸🇭🇰
</td>
<td style="text-align:left;">
Civil Engineer turned Data Science Evangelist & Community Manager (**h2oai?**) \| GitHub: woobe \| Formerly (**DominoDataLab?**) (**virginmedia?**) \| \#AroundTheWorldWithH2Oai
</td>
<td style="text-align:left;">
https://t.co/No9aXP6IEL
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1330
</td>
<td style="text-align:right;">
693
</td>
<td style="text-align:right;">
199
</td>
<td style="text-align:right;">
1847
</td>
<td style="text-align:right;">
2552
</td>
<td style="text-align:left;">
2011-05-11 05:55:44
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/No9aXP6IEL
</td>
<td style="text-align:left;">
http://www.jofaichow.co.uk
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/296664658/1524180604
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1021046533360406528/19NnYn60_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
891904584
</td>
<td style="text-align:left;">
1035823249681207297
</td>
<td style="text-align:left;">
2018-09-01 09:34:42
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
(**SuzanBaert?**) s glamour shot of her \#dplyr docs hardcopy. (**rstudio?**) , when’s the limited edition collectors hardcover coming out? \#satRdayAMS That tip about funs() being replaceable by \~ is great, btw. https://t.co/AYj5jBltqp
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
198
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
931042575158513664
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
dplyr , satRdayAMS
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_7vr5W0AA4LCW.jpg
</td>
<td style="text-align:left;">
https://t.co/AYj5jBltqp
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035823249681207297/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_7vr5W0AA4LCW.jpg
</td>
<td style="text-align:left;">
https://t.co/AYj5jBltqp
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035823249681207297/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
931042575158513664, 235261861
</td>
<td style="text-align:left;">
SuzanBaert, rstudio
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035823249681207297
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
UK
</td>
<td style="text-align:left;">
Make, Do and Mend. \#rstats with (**lockedata?**) and (**satrdays_org?**)
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
306
</td>
<td style="text-align:right;">
612
</td>
<td style="text-align:right;">
17
</td>
<td style="text-align:right;">
1218
</td>
<td style="text-align:right;">
439
</td>
<td style="text-align:left;">
2012-10-19 21:48:48
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
https://github.com/DaveParr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/891904584/1530362945
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1007683337132093440/cujXW7UY_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
891904584
</td>
<td style="text-align:left;">
1035483485350375424
</td>
<td style="text-align:left;">
2018-08-31 11:04:35
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
Had a great week in London learning \#cosmosdb. Now to Amsterdam for \#satRdayAMS \#rstats.
</td>
<td style="text-align:left;">
Twitter for Android
</td>
<td style="text-align:right;">
88
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
cosmosdb , satRdayAMS, rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/DaveParr/status/1035483485350375424
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
UK
</td>
<td style="text-align:left;">
Make, Do and Mend. \#rstats with (**lockedata?**) and (**satrdays_org?**)
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
306
</td>
<td style="text-align:right;">
612
</td>
<td style="text-align:right;">
17
</td>
<td style="text-align:right;">
1218
</td>
<td style="text-align:right;">
439
</td>
<td style="text-align:left;">
2012-10-19 21:48:48
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/dL1YwOL20E
</td>
<td style="text-align:left;">
https://github.com/DaveParr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/891904584/1530362945
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme5/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1007683337132093440/cujXW7UY_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
377578645
</td>
<td style="text-align:left;">
1035799564966682625
</td>
<td style="text-align:left;">
2018-09-01 08:00:35
</td>
<td style="text-align:left;">
romain_francois
</td>
<td style="text-align:left;">
⬆️ your 🤚 if you know what a \#tibble is. Survey during (**krlmlr?**) \#dbi talk at \#satRdayAMS 👶🤚 https://t.co/en42gNKaSz
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
90
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
12
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
tibble , dbi , satRdayAMS
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_mNdcW0AE-tGx.jpg
</td>
<td style="text-align:left;">
https://t.co/en42gNKaSz
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1035799564966682625/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_mNdcW0AE-tGx.jpg
</td>
<td style="text-align:left;">
https://t.co/en42gNKaSz
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1035799564966682625/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3354999513
</td>
<td style="text-align:left;">
krlmlr
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
https://api.twitter.com/1.1/geo/id/99cdab25eddd6bce.json
</td>
<td style="text-align:left;">
Amsterdam
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
city
</td>
<td style="text-align:left;">
The Netherlands
</td>
<td style="text-align:left;">
NL
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
4.728900, 5.079207, 5.079207, 4.728900, 52.278227, 52.278227, 52.431229, 52.431229
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1035799564966682625
</td>
<td style="text-align:left;">
Romain François 🦄
</td>
<td style="text-align:left;">
France
</td>
<td style="text-align:left;">
👨‍💻 \#rstats 📦 with the \#tidyverse team.
</td>
<td style="text-align:left;">
https://t.co/8WIUhd0bJc
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5113
</td>
<td style="text-align:right;">
336
</td>
<td style="text-align:right;">
211
</td>
<td style="text-align:right;">
5837
</td>
<td style="text-align:right;">
5440
</td>
<td style="text-align:left;">
2011-09-21 20:02:22
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/8WIUhd0bJc
</td>
<td style="text-align:left;">
https://purrple.cat
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/377578645/1519142290
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/991018500591378432/U_9\_9qU-\_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
377578645
</td>
<td style="text-align:left;">
1035792905007517696
</td>
<td style="text-align:left;">
2018-09-01 07:34:07
</td>
<td style="text-align:left;">
romain_francois
</td>
<td style="text-align:left;">
\#satRdayAMS at (**GoDataDriven?**) https://t.co/89R3cYtTOG
</td>
<td style="text-align:left;">
Twitter for iPhone
</td>
<td style="text-align:right;">
28
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
satRdayAMS
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_gHXfXgAAH9NA.jpg
</td>
<td style="text-align:left;">
https://t.co/89R3cYtTOG
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1035792905007517696/photo/1
</td>
<td style="text-align:left;">
photo
</td>
<td style="text-align:left;">
http://pbs.twimg.com/media/Dl_gHXfXgAAH9NA.jpg, http://pbs.twimg.com/media/Dl_gHXdX4AEC7v8.jpg, http://pbs.twimg.com/media/Dl_gHXLX4AEWa6Q.jpg
</td>
<td style="text-align:left;">
https://t.co/89R3cYtTOG, https://t.co/89R3cYtTOG, https://t.co/89R3cYtTOG
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1035792905007517696/photo/1, https://twitter.com/romain_francois/status/1035792905007517696/photo/1, https://twitter.com/romain_francois/status/1035792905007517696/photo/1
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
1253544996
</td>
<td style="text-align:left;">
GoDataDriven
</td>
<td style="text-align:left;">
und
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/romain_francois/status/1035792905007517696
</td>
<td style="text-align:left;">
Romain François 🦄
</td>
<td style="text-align:left;">
France
</td>
<td style="text-align:left;">
👨‍💻 \#rstats 📦 with the \#tidyverse team.
</td>
<td style="text-align:left;">
https://t.co/8WIUhd0bJc
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
5113
</td>
<td style="text-align:right;">
336
</td>
<td style="text-align:right;">
211
</td>
<td style="text-align:right;">
5837
</td>
<td style="text-align:right;">
5440
</td>
<td style="text-align:left;">
2011-09-21 20:02:22
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/8WIUhd0bJc
</td>
<td style="text-align:left;">
https://purrple.cat
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
https://pbs.twimg.com/profile_banners/377578645/1519142290
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme1/bg.png
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/991018500591378432/U_9\_9qU-\_normal.jpg
</td>
</tr>
<tr>
<td style="text-align:left;">
120816884
</td>
<td style="text-align:left;">
1035500737143418882
</td>
<td style="text-align:left;">
2018-08-31 12:13:09
</td>
<td style="text-align:left;">
rgiordano79
</td>
<td style="text-align:left;">
Only few hours and I will be in Amsterdam for the \#satRdayAMS. Looking forward to talk about \#regex in \#rstats 😊
</td>
<td style="text-align:left;">
Twitter Web Client
</td>
<td style="text-align:right;">
112
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
satRdayAMS, regex , rstats
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA
</td>
<td style="text-align:left;">
NA, NA, NA, NA, NA, NA, NA, NA
</td>
<td style="text-align:left;">
https://twitter.com/rgiordano79/status/1035500737143418882
</td>
<td style="text-align:left;">
Rita
</td>
<td style="text-align:left;">
France
</td>
<td style="text-align:left;">
Data analyst, researcher and passionate for data. Founder (**RLadiesStras?**).
</td>
<td style="text-align:left;">
https://t.co/alQHCeD7q1
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:right;">
121
</td>
<td style="text-align:right;">
231
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
211
</td>
<td style="text-align:right;">
93
</td>
<td style="text-align:left;">
2010-03-07 17:02:00
</td>
<td style="text-align:left;">
FALSE
</td>
<td style="text-align:left;">
https://t.co/alQHCeD7q1
</td>
<td style="text-align:left;">
https://rasrita.wordpress.com
</td>
<td style="text-align:left;">
en
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
http://abs.twimg.com/images/themes/theme13/bg.gif
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/816934985806606336/EmxKWSKm_normal.jpg
</td>
</tr>
</tbody>
</table>

</div>

\###161 tweets about SatRday Amsterdam.

## Which hashtags ?

``` r
hashtags <- rt$hashtags %>% 
  unlist() %>% 
  str_to_lower() %>%
  table() %>% 
  sort(decreasing = TRUE) %>% 
  enframe() %>%
  mutate( name = as.factor(name), value = as.numeric(value))
```

\###Print the table for all hashtags :

``` r
hashtags %>%
  kable() %>%
  kable_styling() %>%
  scroll_box(width = "100%", height = "200px")
```

<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:200px; overflow-x: scroll; width:100%; ">

<table class="table" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
name
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
value
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
amstrday
</td>
<td style="text-align:right;">
144
</td>
</tr>
<tr>
<td style="text-align:left;">
rstats
</td>
<td style="text-align:right;">
75
</td>
</tr>
<tr>
<td style="text-align:left;">
satrday
</td>
<td style="text-align:right;">
37
</td>
</tr>
<tr>
<td style="text-align:left;">
satrdays
</td>
<td style="text-align:right;">
23
</td>
</tr>
<tr>
<td style="text-align:left;">
amstrdam
</td>
<td style="text-align:right;">
9
</td>
</tr>
<tr>
<td style="text-align:left;">
rladies
</td>
<td style="text-align:right;">
8
</td>
</tr>
<tr>
<td style="text-align:left;">
satrdayams
</td>
<td style="text-align:right;">
7
</td>
</tr>
<tr>
<td style="text-align:left;">
dplyr
</td>
<td style="text-align:right;">
6
</td>
</tr>
<tr>
<td style="text-align:left;">
regex
</td>
<td style="text-align:right;">
4
</td>
</tr>
<tr>
<td style="text-align:left;">
rbaby
</td>
<td style="text-align:right;">
3
</td>
</tr>
<tr>
<td style="text-align:left;">
360selfie
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
amsterday
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
aroundtheworldwithh2oai
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
ggplot
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
moneyball
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
r
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
rshiny
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
tidyverse
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
amstrdays
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
automl
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
awesomer
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
cosmosdb
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
datascience
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
dbi
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
fyouflu
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
ggplot2
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
h2oai
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
hatsoff
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
lime
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
mlb
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
modelplotr
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
oslo
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
rcpp
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
rmarkdown
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
rmd
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
rquery
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
satrdayamsterdam
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
shiny
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
sqlsatoslo
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
textmining
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
tibble
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
winning
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
xai
</td>
<td style="text-align:right;">
1
</td>
</tr>
</tbody>
</table>

</div>

\###Barplot for hashtags used 2 times and more

``` r
gg <- hashtags %>%
  filter(value > 1) %>%
  ggplot(aes(x = reorder(name, value), y = value, fill = 6)) + 
      theme_bw() +
      geom_bar_interactive(aes(tooltip = value, data_id = name), stat="identity") +
      coord_flip() + 
      xlab("Hashtags") + 
      ylab("Number") + 
      guides(fill="none")


# ggiraph(ggobj = gg, hover_css = "fill-opacity:.6;cursor:pointer;",
#             width = 0.8, width_svg = 6,
#             height_svg = 8, selection_type = "none")
```

## Who’s tweeted

``` r
rt %>%
  group_by(name, screen_name, location, profile_image_url) %>%
  summarise(n = n()) %>%
  arrange(-n) -> names 

 #names %>%
#   mutate(image = glue('"include_graphics( {profile_image_url} )"'))

#names
#print(image_read(names$profile_image_url))

kable(names) %>%
  kable_styling() %>%
  scroll_box(width = "100%", height = "200px")
```

<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:200px; overflow-x: scroll; width:100%; ">

<table class="table" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
name
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
screen_name
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
location
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
profile_image_url
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
n
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg
</td>
<td style="text-align:right;">
28
</td>
</tr>
<tr>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:left;">
Groningen
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg
</td>
<td style="text-align:right;">
16
</td>
</tr>
<tr>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:left;">
Montpellier, France
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/2881158206/bb964afd6af2d7beea05a5a2b9fec6af_normal.png
</td>
<td style="text-align:right;">
12
</td>
</tr>
<tr>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:left;">
Dublin, Ireland
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/3427713318/840e4aa0a6dca9263a0507fbfe4c4074_normal.jpeg
</td>
<td style="text-align:right;">
11
</td>
</tr>
<tr>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:left;">
Germany, Europe, Earth
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1020786409622433792/dTcna0WF_normal.jpg
</td>
<td style="text-align:right;">
11
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:left;">
UK
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1007683337132093440/cujXW7UY_normal.jpg
</td>
<td style="text-align:right;">
10
</td>
</tr>
<tr>
<td style="text-align:left;">
R.A. Posthumus
</td>
<td style="text-align:left;">
RAPOSTHUMUS
</td>
<td style="text-align:left;">
Zwolle
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1124144375/rp_normal.jpg
</td>
<td style="text-align:right;">
6
</td>
</tr>
<tr>
<td style="text-align:left;">
Roel
</td>
<td style="text-align:left;">
RMHoge
</td>
<td style="text-align:left;">
Leiden
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/832899187566080000/CyyCNvC7_normal.jpg
</td>
<td style="text-align:right;">
6
</td>
</tr>
<tr>
<td style="text-align:left;">
Romain François 🦄
</td>
<td style="text-align:left;">
romain_francois
</td>
<td style="text-align:left;">
France
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/991018500591378432/U_9\_9qU-\_normal.jpg
</td>
<td style="text-align:right;">
6
</td>
</tr>
<tr>
<td style="text-align:left;">
Suzan Baert
</td>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:left;">
Belgium
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/931044588197998592/nL4heSc9_normal.jpg
</td>
<td style="text-align:right;">
6
</td>
</tr>
<tr>
<td style="text-align:left;">
Edwin Thoen
</td>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:left;">
Leiden, The Netherlands
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1011173218433077248/RIQypB5J_normal.jpg
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
smart-R
</td>
<td style="text-align:left;">
smartR101
</td>
<td style="text-align:left;">
Hilversum, Nederlands
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/923998501398351877/EXEH4wAz_normal.jpg
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
Jo-fai (Joe) Chow
</td>
<td style="text-align:left;">
matlabulous
</td>
<td style="text-align:left;">
🇬🇧🇺🇸🇭🇰
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1021046533360406528/19NnYn60_normal.jpg
</td>
<td style="text-align:right;">
4
</td>
</tr>
<tr>
<td style="text-align:left;">
Mara Averick
</td>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:left;">
Massachusetts
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/812016485069680640/tKpsducS_normal.jpg
</td>
<td style="text-align:right;">
4
</td>
</tr>
<tr>
<td style="text-align:left;">
R- Ladies Amsterdam
</td>
<td style="text-align:left;">
RLadiesAMS
</td>
<td style="text-align:left;">
Amsterdam, Nederlands
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/964843467150102528/ScQ2RYdF_normal.jpg
</td>
<td style="text-align:right;">
4
</td>
</tr>
<tr>
<td style="text-align:left;">
Rita
</td>
<td style="text-align:left;">
rgiordano79
</td>
<td style="text-align:left;">
France
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/816934985806606336/EmxKWSKm_normal.jpg
</td>
<td style="text-align:right;">
3
</td>
</tr>
<tr>
<td style="text-align:left;">
Sarah Stolle
</td>
<td style="text-align:left;">
TheSarahStolle
</td>
<td style="text-align:left;">
The Netherlands
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/958343025666781184/Ra4-sYP1_normal.jpg
</td>
<td style="text-align:right;">
3
</td>
</tr>
<tr>
<td style="text-align:left;">
Suthira Owlarn
</td>
<td style="text-align:left;">
S_Owla
</td>
<td style="text-align:left;">
Germany/Thailand
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/535734330622885888/Mmp0HQqH_normal.jpeg
</td>
<td style="text-align:right;">
3
</td>
</tr>
<tr>
<td style="text-align:left;">
Chris Black
</td>
<td style="text-align:left;">
infotroph
</td>
<td style="text-align:left;">
Nijmegen, NL
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/654666018296467456/9m3ijJ_Z\_normal.jpg
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
GoDataDriven
</td>
<td style="text-align:left;">
GoDataDriven
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1037959579185938432/BMCn_z6X_normal.jpg
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
Ilse Pit
</td>
<td style="text-align:left;">
IlsePit
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/976070874880077824/P4p_7Xus_normal.jpg
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
Madelijn Bazen
</td>
<td style="text-align:left;">
MadelijnBazen
</td>
<td style="text-align:left;">
Nederlands
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/957267685171253248/reG5qYm7_normal.jpg
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
Paul Feitsma
</td>
<td style="text-align:left;">
PaulFeitsma
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/705824513087270912/jrpSCU_T\_normal.jpg
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
Paul van Leeuwen
</td>
<td style="text-align:left;">
paulusj8
</td>
<td style="text-align:left;">
Nederlands
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1035477074570407937/G2zosk99_normal.jpg
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
sema
</td>
<td style="text-align:left;">
semakaran
</td>
<td style="text-align:left;">
Amsterdam, Nederlands
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/855440770517565441/TmHZUgIK_normal.jpg
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
Steven Nooijen
</td>
<td style="text-align:left;">
StevenNooijen
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/1036499367883100160/wv56JPq7_normal.jpg
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
Tess Korthout
</td>
<td style="text-align:left;">
Tesskorthout
</td>
<td style="text-align:left;">
Amsterdam, The Netherlands
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/781414975411724288/stts8RDZ_normal.jpg
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
Bob
</td>
<td style="text-align:left;">
Bootvis
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/733929214899027968/hoqAbzPo_normal.jpg
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
Floris Padt
</td>
<td style="text-align:left;">
FlorisPadt
</td>
<td style="text-align:left;">
Hilversum
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/2235592355/ad6Twit_normal.jpg
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
Gabriel
</td>
<td style="text-align:left;">
oliverowner
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/743906145346129920/-a0c3u66_normal.jpg
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
Ger
</td>
<td style="text-align:left;">
g_inberg
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/670311083182309380/tvityZ62_normal.jpg
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
Hilary Parker
</td>
<td style="text-align:left;">
hspter
</td>
<td style="text-align:left;">
San Francisco
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/611535712710729728/ZrqMrN21_normal.jpg
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
Raphaël Hoogvliets
</td>
<td style="text-align:left;">
HoogvlietsR
</td>
<td style="text-align:left;">
Nederlands
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/792312375407968256/1BXInKJf_normal.jpg
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
Steph Locke
</td>
<td style="text-align:left;">
TheStephLocke
</td>
<td style="text-align:left;">
Cardiff, UK
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/971335139736346624/37TC7pkq_normal.jpg
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
Stéphanie van der Pas
</td>
<td style="text-align:left;">
stephanievdpas
</td>
<td style="text-align:left;">
Leiden, Nederlands
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/990853991084019712/lOBvZvAq_normal.jpg
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
Veerle van Son
</td>
<td style="text-align:left;">
veerlevanson
</td>
<td style="text-align:left;">
’s-Hertogenbosch, Nederlands
</td>
<td style="text-align:left;">
http://pbs.twimg.com/profile_images/998990196669493250/pc6hKizY_normal.jpg
</td>
<td style="text-align:right;">
1
</td>
</tr>
</tbody>
</table>

</div>

``` r
gg <- names %>%
  ggplot(aes(x = reorder(name, n), y = n, fill = 6)) + 
      theme_bw() +
      geom_bar_interactive(aes(tooltip = n, data_id = screen_name),stat="identity") +
      coord_flip() + 
      xlab("Names") + 
      ylab("Number") + 
      guides(fill="none")

# ggiraph(ggobj = gg, hover_css = "fill-opacity:.6;cursor:pointer;",
#             width = 0.8, width_svg = 6,
#             height_svg = 8, selection_type = "none")
```

## Tweets map

``` r
# n <- length(names$location) df <- tibble(lon = rep(NA, n), lat = rep(NA,n))
# for (i in 1: n){ for (counter in 1:10){ if(is.na(df$lat[i])){ df[i,] <-
# geocode(names$location[i]) } } } df %>% summarise_all(funs(sum(is.na(.))))
# df_map <- bind_cols(names, df) %>% select(name, location, lon, lat, n)
# saveRDS(df_map, 'df_map.RDS')


df_map <- readRDS("df_map.RDS")

# map=get_map(location = c(2.3488, 48.8534), zoom = 5) ggmap1 <- ggmap(map) +
# geom_point(data = df_map, aes(x = lon, y = lat, color = name, size = n))
# ggmap1



tib_temp <- tibble(lon = na.omit(df_map$lon), lat = na.omit(df_map$lat)) %>%
    mutate(country = map.where(database = "world", lon, lat))

tib_temp <- tib_temp %>%
    left_join(ungroup(df_map), tib_temp, by = c("lon", "lat")) %>%
    distinct() %>%
    select(screen_name, country)


tib <- left_join(rt, tib_temp, by = c("screen_name"))

tib_map <- tib %>%
    rename(country = country.y) %>%
    group_by(country) %>%
    summarise(n = n()) %>%
    arrange(-n)

########################################''''''
# to get the countries code
df <- read.csv("https://raw.githubusercontent.com/plotly/datasets/master/2014_world_gdp_with_codes.csv")

tib_map <- left_join(tib_map, select(df, COUNTRY, CODE), by = c(country = "COUNTRY"))
tib_map$CODE[5] <- "GBR"
tib_map$CODE[8] <- "USA"
# light grey boundaries
l <- list(color = toRGB("grey"), width = 0.5)

# specify map projection/options
g <- list(showframe = FALSE, showcoastlines = FALSE, projection = list(type = "Mercator"))

p <- plot_geo(tib_map) %>%
    add_trace(z = ~n, color = ~n, colors = "Blues", text = ~country, locations = ~CODE,
        marker = list(line = l)) %>%
    colorbar(title = "Number of tweets") %>%
    layout(title = "SatRday number of tweets by country", geo = g)

p
```

<div id="htmlwidget-1" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"visdat":{"515a44da3894":["function () ","plotlyVisDat"]},"cur_data":"515a44da3894","attrs":{"515a44da3894":{"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"z":{},"color":{},"colors":"Blues","text":{},"locations":{},"marker":{"line":{"color":"rgba(190,190,190,1)","width":0.5}},"inherit":true}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"mapType":"geo","scene":{"zaxis":{"title":"n"}},"geo":{"domain":{"x":[0,1],"y":[0,1]},"showframe":false,"showcoastlines":false,"projection":{"type":"Mercator"}},"hovermode":"closest","showlegend":false,"legend":{"yanchor":"top","y":0.5},"title":"SatRday number of tweets by country"},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"colorbar":{"title":"Number of tweets","ticklen":2,"len":0.5,"lenmode":"fraction","y":1,"yanchor":"top"},"colorscale":[["0","rgba(247,251,255,1)"],["0.0416666666666667","rgba(239,246,252,1)"],["0.0833333333333333","rgba(230,240,250,1)"],["0.125","rgba(222,235,247,1)"],["0.166666666666667","rgba(214,230,244,1)"],["0.208333333333333","rgba(206,224,242,1)"],["0.25","rgba(198,219,239,1)"],["0.291666666666667","rgba(185,213,234,1)"],["0.333333333333333","rgba(172,208,230,1)"],["0.375","rgba(158,202,225,1)"],["0.416666666666667","rgba(142,193,221,1)"],["0.458333333333333","rgba(125,183,218,1)"],["0.5","rgba(107,174,214,1)"],["0.541666666666667","rgba(94,165,209,1)"],["0.583333333333333","rgba(81,155,203,1)"],["0.625","rgba(66,146,198,1)"],["0.666666666666667","rgba(57,135,192,1)"],["0.708333333333333","rgba(46,124,187,1)"],["0.75","rgba(33,113,181,1)"],["0.791666666666667","rgba(27,102,173,1)"],["0.833333333333333","rgba(19,91,164,1)"],["0.875","rgba(8,81,156,1)"],["0.916666666666667","rgba(9,70,139,1)"],["0.958333333333333","rgba(9,59,123,1)"],["1","rgba(8,48,107,1)"]],"showscale":true,"z":[93,21,11,11,11,9,6,5,3],"text":["Netherlands","France","Germany","Ireland","UK:Great Britain",null,"Belgium","USA","Thailand"],"locations":["NLD","FRA","DEU","IRL","GBR",null,"BEL","USA","THA"],"marker":{"line":{"colorbar":{"title":"","ticklen":2},"cmin":3,"cmax":93,"colorscale":[["0","rgba(247,251,255,1)"],["0.0416666666666667","rgba(239,246,252,1)"],["0.0833333333333333","rgba(230,240,250,1)"],["0.125","rgba(222,235,247,1)"],["0.166666666666667","rgba(214,230,244,1)"],["0.208333333333333","rgba(206,224,242,1)"],["0.25","rgba(198,219,239,1)"],["0.291666666666667","rgba(185,213,234,1)"],["0.333333333333333","rgba(172,208,230,1)"],["0.375","rgba(158,202,225,1)"],["0.416666666666667","rgba(142,193,221,1)"],["0.458333333333333","rgba(125,183,218,1)"],["0.5","rgba(107,174,214,1)"],["0.541666666666667","rgba(94,165,209,1)"],["0.583333333333333","rgba(81,155,203,1)"],["0.625","rgba(66,146,198,1)"],["0.666666666666667","rgba(57,135,192,1)"],["0.708333333333333","rgba(46,124,187,1)"],["0.75","rgba(33,113,181,1)"],["0.791666666666667","rgba(27,102,173,1)"],["0.833333333333333","rgba(19,91,164,1)"],["0.875","rgba(8,81,156,1)"],["0.916666666666667","rgba(9,70,139,1)"],["0.958333333333333","rgba(9,59,123,1)"],["1","rgba(8,48,107,1)"]],"showscale":false,"color":"rgba(190,190,190,1)","width":0.5}},"type":"choropleth","geo":"geo","frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

``` r
#names$profile_image_url[1]
include_graphics(names$profile_image_url)
```

![](http://pbs.twimg.com/profile_images/962820093917974528/pqBm3uIx_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/1032285340302802946/eBhbcopV_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/2881158206/bb964afd6af2d7beea05a5a2b9fec6af_normal.png)<!-- -->![](http://pbs.twimg.com/profile_images/3427713318/840e4aa0a6dca9263a0507fbfe4c4074_normal.jpeg)<!-- -->![](http://pbs.twimg.com/profile_images/1020786409622433792/dTcna0WF_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/1007683337132093440/cujXW7UY_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/1124144375/rp_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/832899187566080000/CyyCNvC7_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/991018500591378432/U_9_9qU-_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/931044588197998592/nL4heSc9_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/1011173218433077248/RIQypB5J_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/923998501398351877/EXEH4wAz_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/1021046533360406528/19NnYn60_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/812016485069680640/tKpsducS_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/964843467150102528/ScQ2RYdF_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/816934985806606336/EmxKWSKm_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/958343025666781184/Ra4-sYP1_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/535734330622885888/Mmp0HQqH_normal.jpeg)<!-- -->![](http://pbs.twimg.com/profile_images/654666018296467456/9m3ijJ_Z_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/1037959579185938432/BMCn_z6X_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/976070874880077824/P4p_7Xus_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/957267685171253248/reG5qYm7_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/705824513087270912/jrpSCU_T_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/1035477074570407937/G2zosk99_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/855440770517565441/TmHZUgIK_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/1036499367883100160/wv56JPq7_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/781414975411724288/stts8RDZ_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/733929214899027968/hoqAbzPo_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/2235592355/ad6Twit_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/743906145346129920/-a0c3u66_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/670311083182309380/tvityZ62_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/611535712710729728/ZrqMrN21_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/792312375407968256/1BXInKJf_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/971335139736346624/37TC7pkq_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/990853991084019712/lOBvZvAq_normal.jpg)<!-- -->![](http://pbs.twimg.com/profile_images/998990196669493250/pc6hKizY_normal.jpg)<!-- -->

### Tweets the most liked

``` r
rt %>%
  select(name,  favorite_count, text) %>%
  arrange(-favorite_count) -> favorite_tweets

kable(favorite_tweets) %>%
  kable_styling() %>%
  scroll_box(width = "100%", height = "200px")
```

<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:200px; overflow-x: scroll; width:100%; ">

<table class="table" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
name
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
favorite_count
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
text
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Mara Averick
</td>
<td style="text-align:right;">
190
</td>
<td style="text-align:left;">
So. Much. Useful. Stuffs. (**SuzanBaert?**) on scoped dplyr verbs! \#rstats \#AmstRday \#satRday (**satRdays_org?**)
📽 https://t.co/mLrNvjBaYG https://t.co/EIVqre9Gmj
</td>
</tr>
<tr>
<td style="text-align:left;">
R- Ladies Amsterdam
</td>
<td style="text-align:right;">
58
</td>
<td style="text-align:left;">

\#rladies awesomeness at \#amstRday

(**RladiesBrussels?**) (**RLadiesStras?**) (**RLadiesGlobal?**) (**Tesskorthout?**) (**TheSarahStolle?**) (**rgiordano79?**) (**cecilesauder?**) https://t.co/5V9hPRWG6j
</td>
</tr>
<tr>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:right;">
51
</td>
<td style="text-align:left;">
Come back from \#AmstRday, \#Rbaby 👶 Lexie put her new \#RLadies sticker on her 💻 to work with mummy. https://t.co/18vuAuSRTG
</td>
</tr>
<tr>
<td style="text-align:left;">
Edwin Thoen
</td>
<td style="text-align:right;">
46
</td>
<td style="text-align:left;">
My slides of \#amstRday are here https://t.co/Iv5OhFV0nv. Also there is a, rather lengthy, blog post on NSE here https://t.co/dat9Uc0QR7. Questions and remarks are very welcome. \#rstats
</td>
</tr>
<tr>
<td style="text-align:left;">
Rita
</td>
<td style="text-align:right;">
38
</td>
<td style="text-align:left;">
The slides from my presentation about \#regex in \#rstats (**satRdays_org?**) \#amstRday are available on github: https://t.co/Lnonk4p1TA
</td>
</tr>
<tr>
<td style="text-align:left;">
Romain François 🦄
</td>
<td style="text-align:right;">
35
</td>
<td style="text-align:left;">
Never too early to attend a \#satRdays \#rstats conference. \#rbaby 👶 https://t.co/gx7U8k3CVU
</td>
</tr>
<tr>
<td style="text-align:left;">
Mara Averick
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:left;">
.@krlmlr talking DBI (**satRdays_org?**) \#amsteRday \#rstats https://t.co/JFbQALSQjd
</td>
</tr>
<tr>
<td style="text-align:left;">
Mara Averick
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:left;">
💘🙏🌷 to everyone who made (**satRdays_org?**) \#AmstRday such a 💥! (**GoDataDriven?**) (**fishnets88?**) (**Janinekhuc?**) (**Tesskorthout?**) (**RConsortium?**) &amp;co 👋🇳🇱 https://t.co/zBBPZMYkpi
</td>
</tr>
<tr>
<td style="text-align:left;">
Tess Korthout
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:left;">
Love it that (**dataandme?**) mentions my favorite podcast (**NSSDeviations?**) at \#amstRday! Would love to have (**hspter?**) and (**rdpeng?**) next year! \#rstats \#satRdays https://t.co/ARyrWx34JL
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
27
</td>
<td style="text-align:left;">
(**SuzanBaert?**) starting off with sharing her excitement about \#amstRday ! Get ready, she’s sharing all her \#dplyr secrets with us! ’Getting more out of dplyr‘ \#rstats https://t.co/XJGATsQqlU
</td>
</tr>
<tr>
<td style="text-align:left;">
Romain François 🦄
</td>
<td style="text-align:right;">
27
</td>
<td style="text-align:left;">
Open source day after \#amstRday. regex and cheatsheets. https://t.co/kmXpuPnhfa
</td>
</tr>
<tr>
<td style="text-align:left;">
Chris Black
</td>
<td style="text-align:right;">
27
</td>
<td style="text-align:left;">
My highlight of the morning at \#amstRday: (**SuzanBaert?**) with a exceptionally clear walk-through of the scoped dplyr verbs. Slides at https://t.co/I4fc2ySWtl, but look for video — her explanations are outstanding.
</td>
</tr>
<tr>
<td style="text-align:left;">
Suzan Baert
</td>
<td style="text-align:right;">
27
</td>
<td style="text-align:left;">
Spreading the hex sticker love at \#AmstRday !! 🎉🎉 (**rweekly_org?**) (**RLadiesGlobal?**) https://t.co/QbIcK2sXF4
</td>
</tr>
<tr>
<td style="text-align:left;">
Jo-fai (Joe) Chow
</td>
<td style="text-align:right;">
24
</td>
<td style="text-align:left;">
(**RLadiesAMS?**) (**RladiesBrussels?**) (**RLadiesStras?**) (**RLadiesGlobal?**) (**Tesskorthout?**) (**TheSarahStolle?**) (**rgiordano79?**) (**cecilesauder?**) (**SuzanBaert?**) (**dataandme?**) (**Janinekhuc?**) (**IlsePit?**) \#rladies \#amstRday \#360selfie 🤳🏻😎 https://t.co/zR5hhnzuYn
</td>
</tr>
<tr>
<td style="text-align:left;">
Jo-fai (Joe) Chow
</td>
<td style="text-align:right;">
24
</td>
<td style="text-align:left;">

I forgot to say a big thank you to (**satRdays_org?**) \#rstats \#amstRday especially (**fishnets88?**) &amp; (**GoDataDriven?**) for having me again. I hope you all enjoyed a short version of \#Moneyball. See you next time :)

It was also great to meet (**dataandme?**) 🎉

\#AroundTheWorldWithH2Oai
\#360Selfie https://t.co/oYb0sVATcE
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:left;">
Our keynote (**dataandme?**) . Starting the day with ‘That’s not \[data\] science.’ \#amstRday \#rstats https://t.co/BBN8T5piKu
</td>
</tr>
<tr>
<td style="text-align:left;">
Mara Averick
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:left;">
Make life easier w/ dplyr/dbplyr syntax, other 📦s … \#amstRday \#amstRday \#rstats \#dplyr \#rquery 💪 (**krlmlr?**) https://t.co/NMBCWyZJo9
</td>
</tr>
<tr>
<td style="text-align:left;">
Veerle van Son
</td>
<td style="text-align:right;">
22
</td>
<td style="text-align:left;">
I received my first hex sticker yesterday! \#amstRday \#rladies https://t.co/tDrfI6CXBI
</td>
</tr>
<tr>
<td style="text-align:left;">
Stéphanie van der Pas
</td>
<td style="text-align:right;">
20
</td>
<td style="text-align:left;">
What a great \#amstRday! Featuring Science Gossip (the journal! great find by (**dataandme?**)), the bang bang operator (**suzanbaert?**), and an entertaining talk on Non-Standard Evaluation by (**edwin_thoen?**)! https://t.co/KMWLCyOPNx
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
17
</td>
<td style="text-align:left;">
Could you not join \#amstRday or would like to look up your fav speakers slides? We will soon link the slides on our website. In the meantime, some of our speakers already made their fantastic slides available. More will be added as slides are made available \#rstats
</td>
</tr>
<tr>
<td style="text-align:left;">
Ilse Pit
</td>
<td style="text-align:right;">
16
</td>
<td style="text-align:left;">
(**SuzanBaert?**) casually blowing my mind by teaching us about scoped dplyr functions 🙌 \#amstRday \#satRdays \#rstats https://t.co/UqMCVbYRZm
</td>
</tr>
<tr>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:right;">
16
</td>
<td style="text-align:left;">
✈️➡️ \#satRdays Amsterdam https://t.co/uCxfPITLHm
</td>
</tr>
<tr>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:right;">
15
</td>
<td style="text-align:left;">
Rita Giordano talks about
Regulars Expressions in \#rstats 👍 at \#AmstRday
\#satRday https://t.co/N8Hb2rfJ1M
</td>
</tr>
<tr>
<td style="text-align:left;">
Suzan Baert
</td>
<td style="text-align:right;">
15
</td>
<td style="text-align:left;">
Also love the quote (**dataandme?**) shared on being kind to beginners \#amstRday https://t.co/1NACHNncVG
</td>
</tr>
<tr>
<td style="text-align:left;">
Edwin Thoen
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:left;">
Guess who I finally got to meet today at \#amsteRday! https://t.co/CC5iDghizR
</td>
</tr>
<tr>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:left;">
Data science-ing by (**dataandme?**) at \#amstRday 😁 https://t.co/sN9pnMSeS1
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:left;">
Joe-Fai Chow (**matlabulous?**) introduces the moneyball app developed using R, Shiny and H2O AutoML \#rstats \#amstRday \#h2oai \#rshiny \#lime (**h2oai?**) https://t.co/7A7oSNfScz
</td>
</tr>
<tr>
<td style="text-align:left;">
GoDataDriven
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:left;">
The magic of data at \#AmstRday! Yesterday started with great workshops at (**Uber_NL?**). Today is full of \#R talks at the conference. It is lovely to contribute to more \#Rstats \#datascience awesomeness with (**satRdays_org?**), (**rstudio?**), (**RLadiesAMS?**), and thanks to all inspiring speakers! https://t.co/tj7GmwjQ5G
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
13
</td>
<td style="text-align:left;">
Don’t miss your chance to get some awesome stickers sponsored by (**rstudio?**) and (**LockeData?**) \#amstRday \#rstats https://t.co/E1M9ZvPKLB
</td>
</tr>
<tr>
<td style="text-align:left;">
Suzan Baert
</td>
<td style="text-align:right;">
13
</td>
<td style="text-align:left;">
Two talks done at \#amstRday! (**dataandme?**) had a terrific talk showing how even the word “scientist” was controversial 🎉
</td>
</tr>
<tr>
<td style="text-align:left;">
Sarah Stolle
</td>
<td style="text-align:right;">
13
</td>
<td style="text-align:left;">
Great discovery for biological plots with large value differences
facet_zoom in ggforce \#ggplot2 \#rstats 😃 \#amstRday (**DerFredo?**) https://t.co/OTuRqpm42W
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
12
</td>
<td style="text-align:left;">
Excited to kick off the first \#satRdays in Amsterdam. Follow \#amstRday for updates over the weekend- brilliant minds coming together to learn, teach and discuss \#rstats https://t.co/19lOvaxhD9
</td>
</tr>
<tr>
<td style="text-align:left;">
Edwin Thoen
</td>
<td style="text-align:right;">
12
</td>
<td style="text-align:left;">
Had a fabulous day yesterday at the very first \#amstRday! Would be delighted if this became a regular thing. Many thanks to the organising committee and (**GoDataDriven?**) for the venue.
</td>
</tr>
<tr>
<td style="text-align:left;">
Romain François 🦄
</td>
<td style="text-align:right;">
12
</td>
<td style="text-align:left;">
⬆️ your 🤚 if you know what a \#tibble is. Survey during (**krlmlr?**) \#dbi talk at \#satRdayAMS 👶🤚 https://t.co/en42gNKaSz
</td>
</tr>
<tr>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:left;">
Dank u wel &amp; thank you to the attendees of my session „50 ways to show your data“ at \#amstRday. Slides and script are now available at https://t.co/ZlD26fpiZJ \#rstats /(**satRdays_org?**)
</td>
</tr>
<tr>
<td style="text-align:left;">
R- Ladies Amsterdam
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:left;">
More \#rladies power! (**rgiordano79?**) from (**RLadiesStras?**) telling us about the awesomeness of \#regex in \#rstats! \#amstRday https://t.co/rpxEAboBaG
</td>
</tr>
<tr>
<td style="text-align:left;">
Suzan Baert
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:left;">
Shiny apps with multiple languages? 😱😱😱😱. I love it. Great talk by Dominik Krzemiński! \#amstRday https://t.co/blJ3SxKigc
</td>
</tr>
<tr>
<td style="text-align:left;">
Romain François 🦄
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:left;">
Getting more out of \#dplyr, (**SuzanBaert?**) \#amstRday \#satrdays \#rstats \#tidyverse https://t.co/zLDLuXPnM9
</td>
</tr>
<tr>
<td style="text-align:left;">
Roel
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:left;">
The \#amstRday is on its way! Today tutorials, tomorrow speakers and on sunday we can hack together, for instance to create \#rstats 📦.  
(**satRdays_org?**) https://t.co/2aG87Q1Sur https://t.co/TnEVyVvjCE
</td>
</tr>
<tr>
<td style="text-align:left;">
Suzan Baert
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:left;">
For people who don’t know SQL, or are learning it, (**krlmlr?**) shared a nice trick to get a query from R code with dbplyr \#amstRday https://t.co/E9tOZFdjko
</td>
</tr>
<tr>
<td style="text-align:left;">
Rita
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:left;">
Only few hours and I will be in Amsterdam for the \#satRdayAMS. Looking forward to talk about \#regex in \#rstats 😊
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
9
</td>
<td style="text-align:left;">
Dominik Krzemiński sharing with us how to make your shiny apps shine even brighter ! \#rstats \#amstRday \#rshiny https://t.co/HCzzystHVy
</td>
</tr>
<tr>
<td style="text-align:left;">
Rita
</td>
<td style="text-align:right;">
9
</td>
<td style="text-align:left;">
Going back to Strasbourg. Thanks the organiser of (**satRdays_org?**) \#amstRday (**GoDataDriven?**) and (**LockeData?**) for sponsoring the event. Very well organised! I really enjoyed!
</td>
</tr>
<tr>
<td style="text-align:left;">
Suthira Owlarn
</td>
<td style="text-align:right;">
9
</td>
<td style="text-align:left;">
Huge thanks to everyone involved in organising \#amstRday! I learned so much, met so many awesome \#rstats people (including many (**RLadiesAMS?**)) and had so much fun!! My first but definitely not my last (**satRdays_org?**) event!! :D
</td>
</tr>
<tr>
<td style="text-align:left;">
Steven Nooijen
</td>
<td style="text-align:right;">
9
</td>
<td style="text-align:left;">
Dusted off my account especially to Tweet about \#amstRday today! Great to have about a 100 R lovers here, of which 14 awesome speakers 🎉 https://t.co/c6JXcRZWB5
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:left;">
Lexie, our youngest and most motivated workshop attendee \#rstats \#amstRday \#satRday https://t.co/cB9ByN03Um
</td>
</tr>
<tr>
<td style="text-align:left;">
Jo-fai (Joe) Chow
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:left;">

After \#amstRday, I am bringing the (**h2oai?**) (**IBMDataScience?**) (**Aginity?**) \#Moneyball to \#Oslo. Come and join us tomorrow ⚾️🇳🇴

\#AroundTheWorldWithH2Oai
\#AutoML \#XAI \#Shiny \#rstats https://t.co/MwcafHE6SP
</td>
</tr>
<tr>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:left;">
Hmm, so (**TheStephLocke?**) is almost around the corner 😀 or at least (**LockeData?**) is \#amstRday https://t.co/LTCyHKaicV
</td>
</tr>
<tr>
<td style="text-align:left;">
Hilary Parker
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:left;">
(**Tesskorthout?**) (**dataandme?**) (**NSSDeviations?**) (**rdpeng?**) aww yay!! that makes my morning!! =) (uh and would LOVE to come to Amsterdam!) \#amstRday
</td>
</tr>
<tr>
<td style="text-align:left;">
smart-R
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:left;">
50 Beautiful gRaphs by Thomas Hütter using (gg)-packages e.g. waterfall, treemap, ggradar  #amstRday slides to be published on https://t.co/8Gaw4Sio9c \#satRdays https://t.co/7YBuog5Huq
</td>
</tr>
<tr>
<td style="text-align:left;">
Roel
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:left;">
After explaining text2vec, (**longhowlam?**) gives us an important lesson: “always check your results with the business, or in this case my wife” \#AmstRday https://t.co/HwQgzhK5Oj
</td>
</tr>
<tr>
<td style="text-align:left;">
Roel
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:left;">
Dominik Krzemiński assures us that we can now translate your shiny apps to klingon (or other languages if you’d like) \#rstats \#amstRday https://t.co/8yyuwLWEFs
</td>
</tr>
<tr>
<td style="text-align:left;">
Steph Locke
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:left;">
Super excited today as \#SQLSatOslo and \#amstRday main events are happening. Big shout out to the organisers of both who’ve done amazing jobs - if you’re around you should thank them as it’s a purely volunteer role!
</td>
</tr>
<tr>
<td style="text-align:left;">
Romain François 🦄
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:left;">
\#satRdayAMS at (**GoDataDriven?**) https://t.co/89R3cYtTOG
</td>
</tr>
<tr>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
(**SuzanBaert?**) talk about
“Getting more out of \#dplyr” at \#amstRday
\#rstats https://t.co/cGdqWwTjvb
</td>
</tr>
<tr>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
(**sholderer?**) Olga talks about
Using R/ R Markdown to create individual reports at \#amstRday
\#SatRday
\#rstats
Hey (**DavidGohel?**) , it’s about your work 😁 https://t.co/ydLHzcm8xU
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
\#amstRday beautiful view, networking &amp; drinks https://t.co/1Z2jBrSTRd
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
Thanks for joining us for a fantastic kick-off of the first \#amstRday conference! It was truly awe inspiring! https://t.co/7RYE80Gte5
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
Our dearly loved mtcars dataset. (**DerFredo?**) so, who actually thinks lollipop charts are cute? \#amstRday \#ggplot \#rstats https://t.co/7TrGbWcgVY
</td>
</tr>
<tr>
<td style="text-align:left;">
Edwin Thoen
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
🤬😡🤬, hit by de flu right before \#amstRday. Would be so gutted to miss it. Hope I can make it by drugging-up tomorrow. Pfff… \#rstats \#fyouflu
</td>
</tr>
<tr>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
Starting off for my first ever \#SatRday \#amstRday /(**satRdays_org?**) https://t.co/WR2zrJmQQe
</td>
</tr>
<tr>
<td style="text-align:left;">
R- Ladies Amsterdam
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
(**RladiesBrussels?**) power at \#amstRday ! Great talk by (**SuzanBaert?**) on how to get more out of dplyr. \#rstats \#rladies https://t.co/yOHq8wCyWO
</td>
</tr>
<tr>
<td style="text-align:left;">
Roel
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
Bob Jansen: Solved the world’s hardest sudoku within a minute with pure R. And thought: that can be done faster. Let’s use Rcpp! \#AmstRday
</td>
</tr>
<tr>
<td style="text-align:left;">
sema
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
\#amstRday \#satRday we’ve “got more out of dplyr” thanks to (**SuzanBaert?**) ! https://t.co/UoGBtbXdQ5
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
After a great lunch, let’s continue with (**edwin_thoen?**) ‘An exploration of NSE and tidyeval’ \#rstats \#amstRday https://t.co/UuTbmgJkwS
</td>
</tr>
<tr>
<td style="text-align:left;">
Paul van Leeuwen
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
Running (**DerFredo?**)’s code with those great hand-made lollipop-charts from last weekend’s \#AmstRday. It was fun and I learned a lot! \#rstats https://t.co/q904gpcBBY
</td>
</tr>
<tr>
<td style="text-align:left;">
Edwin Thoen
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
I thought the 10-minute lightening talks at \#amstRday were so much more informative and entertaining than the usual 5-minute versions. Just saying (**UseR2019_Conf?**) \#rstats
</td>
</tr>
<tr>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
Taking \#amstRday to the next round: (**SuzanBaert?**) getting more out of dplyr. \#rstats https://t.co/msg8FTnGzv
</td>
</tr>
<tr>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
Attending \#SatRday at (**GoDataDriven?**) in Amsterdam \#AmstRday \#R https://t.co/GJQAnsvP7g
</td>
</tr>
<tr>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
You should check out the tmap package if you want to make beautiful maps in R https://t.co/hYORmmyTel \#SatRday \#AmstRday
</td>
</tr>
<tr>
<td style="text-align:left;">
sema
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
\#amstRday \#rstats keynote talk from (**dataandme?**) 👩🏻‍💻🤗 https://t.co/YIfA6vn8fg
</td>
</tr>
<tr>
<td style="text-align:left;">
Paul Feitsma
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
Really enjoyed the talks last weekend at \#satRDays in \#AmstRday with (**dataandme?**) (**SuzanBaert?**) (**rgiordano79?**) (**GoDataDriven?**) and more \#satRdayAMS
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
The final fun⚡️talk, solving sudokus with \#rcpp by Bob Jansen! \#amstRday \#rstats https://t.co/NFR1lB2jez
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
Next up, (**krlmlr?**) on the most ‘Recent development in R’s database interface’ \#amstRday \#rstats https://t.co/V3TjS0Rm4o
</td>
</tr>
<tr>
<td style="text-align:left;">
Ger
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
Interesting talks at the first \#satRday Amsterdam! \#AmstRday. Got some of the famous stickers as well:-) \#rstats https://t.co/dUQDAu8Iwn
</td>
</tr>
<tr>
<td style="text-align:left;">
Chris Black
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
Highlight of the afternoon for me at \#AmstRday: Rianne Schouten showing mice::ampute, which generates missing data from a specified multivariate pattern. this looks VERY handy for testing model assumptions. https://t.co/aDs2hkahEe
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
“it’s hard to read a Sudoku problem into R wrong. It’s a perfect language for that”
\#amstRday
</td>
</tr>
<tr>
<td style="text-align:left;">
smart-R
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
Nice - mice::ampute now they also eat your data next to your cheese (at random and not at random) \#amstRday thanks to https://t.co/zRShbLhCJs https://t.co/iAMKjU6IUJ
</td>
</tr>
<tr>
<td style="text-align:left;">
Sarah Stolle
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
R \#dplyr has bang bang 💥!! functions 💥!! 😄#awesomeR \#rstats \#amstRday (**SuzanBaert?**)
</td>
</tr>
<tr>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
.@SuzanBaert telling us about *scoped* dplyr functions. Nifty! \#AmstRday \#SatRday https://t.co/P7Cws7XTII
</td>
</tr>
<tr>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
Other R packages for working with databases in R mentioned by (**krlmlr?**) \#SatRday \#AmstRday https://t.co/qcNrP8g0xB
</td>
</tr>
<tr>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
(**RoryJosephQuinn?**) (**GalwayRusers?**) (**statsepi?**) (**jaynal83?**) A \#SatRdays in West of Ireland sometime? (**EngineLimerick?**) would make a nice venue https://t.co/DJAddmLyXS
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
Ready, set, go! Let’s get started with a fun weekend! A bunch of curious people ready to learn all about tidyverse &amp; webscraping! \#amstRdays \#rstats \#satRdays https://t.co/qjcuNFosdC
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
2nd ⚡️-talk (**longhowlam?**) showing us how to use text2vec for fun projects \#rstats \#amstRday https://t.co/aLL9FkWMG3
</td>
</tr>
<tr>
<td style="text-align:left;">
Suthira Owlarn
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
(**WeAreRLadies?**) (**JennyBryan?**) (**g3rv4?**) (**DesiNavadeh?**) (**romain_francois?**)’ and (**cecilesauder?**)’s \#rbaby was a delightful part of \#amstRday over the weekend! :D
</td>
</tr>
<tr>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
Last round of lightning tasks at \#amstRday started by Rianne Schouten \#rstats https://t.co/jVOFxvs3E4
</td>
</tr>
<tr>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
Next up for his \#amstRday session on recent DBI development is (**krlmlr?**) \#rstats https://t.co/Owpj8kz3iS
</td>
</tr>
<tr>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
Full room also for (**rgiordano79?**) kicking off the lightning talks at \#amstRday \#rstats https://t.co/KXltjX68Er
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
(**edwin_thoen?**) setting up a great punchline for an extended coding joke in \#amstRday about non-standard eval https://t.co/2f1TpFKqgm
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
“Three weeks of reporting by hand for 30 reports reduced to three days of r coding and .rmd documents with parameters” \#amstRday \#rstats \#Winning
</td>
</tr>
<tr>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
That’s a wrap for \#AmstRday 2018. Great conference. https://t.co/JqrPHgZMc8
</td>
</tr>
<tr>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
Longhow Lam giving a lightning talk on text2vec with \#rstats : predicting house prices \#AmstRday https://t.co/8de0ibGpqa
</td>
</tr>
<tr>
<td style="text-align:left;">
R- Ladies Amsterdam
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
Excited to see \#Rladies at \#amstRday ! https://t.co/0FOgCTXuxu
</td>
</tr>
<tr>
<td style="text-align:left;">
Roel
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">

Did I just tweet the entire Saturday program for \#amstRday ? 🙀

Yes! https://t.co/BfP60hVWyp
</td>
</tr>
<tr>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
Next up: (**sholderer?**) on the power of R Markdown in creating reports in MS Word \#RMD \#AmstRday \#SatRday https://t.co/0o08Yh13H1
</td>
</tr>
<tr>
<td style="text-align:left;">
Tess Korthout
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
So far the woRkshop is awesome! So excited for \#amstRday! https://t.co/zDCb9D5Gzo
</td>
</tr>
<tr>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
Kick-off with (**dataandme?**)‘s keynote telling us to ’LeaRn Out Loud’ \#AmstRdam \#SatRday https://t.co/33n5B1SVJu
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
Had a great week in London learning \#cosmosdb. Now to Amsterdam for \#satRdayAMS \#rstats.
</td>
</tr>
<tr>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
And last but not least… Bob Jansen 
tells us how to solve sudoku with Rcpp at \#AmstRday
\#SatRday
\#rstats https://t.co/UatXYQBcpn
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
(**dataandme?**) finishing off with the need for all R-users of every skill level to contribute to open source to move the \#rstats community ahead! \#amstRday \#satRdays https://t.co/6ILTDPg37T
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
And next up, is (**sholderer?**) showing us how to create pretty reproducible reports with \#rmarkdown in \#rstats \#amstRday https://t.co/mEQUMOpFxd
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
(**DerFredo?**) showing us how to visualise data in just about 50 different ways. \#amstRday \#rstats \#ggplot https://t.co/LZhiWvYoi3
</td>
</tr>
<tr>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
It’s (**dataandme?**) taking the stage for the opening keynote of \#amstRday \#rstats https://t.co/aRjyltgXZ3
</td>
</tr>
<tr>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
After lunch: (**edwin_thoen?**) about NSE and tidyeval. \#amstRday \#rstats https://t.co/9cEToYsbIA
</td>
</tr>
<tr>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
Back home from a pleasant weekend in Amsterdam, big thanks go to the \#amstRday team for organizing a fantastic event and for having me as a speaker! I had a great time mingling with all of you R community members! \#rstats /(**satRdays_org?**)
</td>
</tr>
<tr>
<td style="text-align:left;">
Raphaël Hoogvliets
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">

(**matlabulous?**) (**dataandme?**) (**satRdays_org?**) (**fishnets88?**) (**GoDataDriven?**) Oh no, can’t believe I missed this, right in my own city 😑.

Looks really great! Where do I sign up for the next one? \#AmstRday
</td>
</tr>
<tr>
<td style="text-align:left;">
Madelijn Bazen
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
Excellent \#satRday conference, with excellent \#rstats takeaways :) Thank you \#AmstRday and \#RLadies! https://t.co/hXC2c2gkMn
</td>
</tr>
<tr>
<td style="text-align:left;">
Floris Padt
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
(**edwin_thoen?**) Thanks (**EdwinThoen?**) for coming despite of flu and giving a talk on steroids \#amstRday about tidyeval interesting, mind boggling and entertaining,
</td>
</tr>
<tr>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
Very impressed with the \#AmstRday venue. Fair play to (**GoDataDriven?**) for providing a great venue. \#AmstRday \#RStats https://t.co/qiAyoYaGUx
</td>
</tr>
<tr>
<td style="text-align:left;">
Suzan Baert
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
(**edwin_thoen?**) working through a big cold to share something not quite that straightforward. \#hatsoff \#AmstRday https://t.co/TI658PtSze
</td>
</tr>
<tr>
<td style="text-align:left;">
Sarah Stolle
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
Promising title for the next \#amstRday talk 😂 https://t.co/nJseXTaXs9
</td>
</tr>
<tr>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
Now Rita Giordano’s lightning talk on regular expressions in R. “Learn RegEx. Do not copy, paste, remove… Use RegEx!” \#AmstRday \#SatRday https://t.co/e50SIDBLF5
</td>
</tr>
<tr>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
Next up, (**SuzanBaert?**)‘s talk on ’Getting more out of dplyr’ \#SatRday \#AmstRday https://t.co/5Qv75uwyzC
</td>
</tr>
<tr>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
Two hobby projects from (**longhowlam?**) using the text2vec package https://t.co/mx3L3qUpdV &amp; https://t.co/enqIko18cR \#textmining \#AmstRday \#SatRday
</td>
</tr>
<tr>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
.@edwin_thoen: “Why should you care about how NSE (non-standard evaluation) works? because most R users slip into tool design sooner or later” \#SatRday \#AmstRday
</td>
</tr>
<tr>
<td style="text-align:left;">
Ilse Pit
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
So hyped about this! (And less scared than I look, I promise :D ) \#amstRday https://t.co/bZ9LqxzLZB
</td>
</tr>
<tr>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
.@dataandme: “It’s important that newcomers contribute. We need people that contribute on all levels.” \#AmstRdam \#SatRday
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
Next up, Gilian Porte on scraping the internet with R. \#amstRdam \#satRdays \#rstats https://t.co/JwE2TRcujO
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Jeroen Groot tells us about analysis of data to get insights about smart charging of electric cars. \#AmstRday \#rstats https://t.co/DLVbmWdsJO
</td>
</tr>
<tr>
<td style="text-align:left;">
Paul van Leeuwen
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
.@longhowlam explaining how to predict house prices with the text2vec package. \#AmstRday https://t.co/YAErIzwsym
</td>
</tr>
<tr>
<td style="text-align:left;">
Thomas Hütter
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Dominik (not on Twitter - yet) came all the way from Cardiff (not Poland 😉) to \#amstRday to make Shiny shine even more. \#rstats https://t.co/g07YOFZUB5
</td>
</tr>
<tr>
<td style="text-align:left;">
Madelijn Bazen
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Great \#amstRday keynote talk ‘That’s not \[data\] science!’ by (**dataandme?**)! Learning new words like ex•o•ter•ic and Rgossip..Definitely worth taking the 7:30 train on a \#satRday! https://t.co/ixPUJL7z4A
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
(**matlabulous?**) knocked it out of the park with his \#mlb moneyball talk at \#amstRday using h2o, lime and shiny to make a winning team! ⚾ https://t.co/TMuObVnGi8 (retweet to fix horrible typo)
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
(**DerFredo?**) thanks for the ‘sweet’ live coding session \#amstRday https://t.co/yRYxN13VFv
</td>
</tr>
<tr>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
‘Why ROC curves are unfit for business modelling’ with Pieter Marcus @ \#AmstRday. Check out the modelplotR package. \#SatRdays https://t.co/kn7u8Rkoid
</td>
</tr>
<tr>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
‘Solving Sudokus with R and C++’ With Bob Jansen at \#AmstRday \#satrdays https://t.co/VC3wx0GLWi
</td>
</tr>
<tr>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Jo Fai Chow from (**h2oai?**) talks Baseball and Moneyball @ \#AmstRday \#satrdays https://t.co/s8CJAKl02o
</td>
</tr>
<tr>
<td style="text-align:left;">
smart-R
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
An exploration of NSE and tidyeval by Edwin Thoen https://t.co/TAHYEKPXGp, \#amstRday https://t.co/7xsYGW9w65, nice to be a Koala and get it all explained https://t.co/lXxYXCTpoO
</td>
</tr>
<tr>
<td style="text-align:left;">
Roel
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">

Rita slashes through shopping lists with R.

Regular expressions made easy by Rita Giordano \#AmstRday
</td>
</tr>
<tr>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Check out these great tutorials by (**SuzanBaert?**): https://t.co/xThpY7UIZp Tomorrow her slides will also be online https://t.co/ELMuCaRXto \#AmstRday \#SatRday
</td>
</tr>
<tr>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Next up, (**krlmlr?**) with his talk on the DBI package, R’s database interface https://t.co/9Q1Ua910cS \#AmstRday \#SatRday
</td>
</tr>
<tr>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
“What does doing data science look like?” (**rdpeng?**) wrote an interesting book on this topic: ‘Putting It All Together: Essays on Data Analysis’ https://t.co/8LiOE61oXc \#AmstRdam \#SatRDay
</td>
</tr>
<tr>
<td style="text-align:left;">
Romain François 🦄
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Any \#rstats people going to \#satrdays with a stroller to lend for a few days? (**AirFranceKLM?**) lost ours between Nantes and Amsterdam 🤷‍♂️
</td>
</tr>
<tr>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
(**dataandme?**) Mara at \#satRdays \#SatRdayAmsterdam https://t.co/ruguTvAi0Z
</td>
</tr>
<tr>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
\#amstRday \#rstats (**dataandme?**) keynote https://t.co/hu45Wkb8qk
</td>
</tr>
<tr>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Thomas Hütter shows us
50 ways to show our data 💹📈📉📊 at \#AmstRday \#satRday \#rstats https://t.co/OXB6trV6EW
</td>
</tr>
<tr>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
(**krlmlr?**) talk at \#amstRday \#rstats https://t.co/L8ZPe3Ou5o
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Check out the full emoji featured programme for \#amstRday \#rstats https://t.co/wMFjC8GoN4
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Coffee time ☕️, before we continue with our ✨⚡️ lightning talks! \#amstRday \#rstats https://t.co/Ch1fgOLuqJ
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Pieter Marcus discussing ‘Why you shouldn’t use ROC curves to assess the business value of your model!’ - an r package that makes it easier to communicate your ML results to non-tech people \#modelplotR \#rstats \#amstRday https://t.co/oI5oO0fAca
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Or come find me at \#amstRday . I’m wearing the same shirt as Oz in this picture, but I have more hair and am in Amsterdam. https://t.co/wjiAyUc0F9
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Great examples of performant natural language processing at \#amstRday https://t.co/QHNhBCzDjv
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
(**rgiordano79?**) helping regular people express themselves using \#regex at \#amstRday https://t.co/UYtthIh2kz
</td>
</tr>
<tr>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
‘Using \#rstats and R markdown for Individual Reports’ with Olga Sholderer - lightning talk @ \#AmstRday \#SatRdays https://t.co/j8smV5BLDA
</td>
</tr>
<tr>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
“Generating Missing Values with Ampute” with Rianne Schouten @ \#AmstRday \#rstats https://t.co/83eJX3p6k5
</td>
</tr>
<tr>
<td style="text-align:left;">
smart-R
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Thanks (**Dominik?**) Krzemiński #amstRday very useful:
Making Shiny shine even brighter
https://t.co/UeqNRR2TYj https://t.co/GiO71d7Z00 https://t.co/qhYvcSweK3 all from https://t.co/PaH9chdk3k https://t.co/tsX1bwx1b2
</td>
</tr>
<tr>
<td style="text-align:left;">
smart-R
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
BIG thanks to Bob Jansen and \#amstRday for solving the hardest puzzles this \#satRday https://t.co/8Gaw4Sio9c, a lot to digest https://t.co/yIIWveIwKy
</td>
</tr>
<tr>
<td style="text-align:left;">
Steven Nooijen
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Always good to think about why data is missing, and what’s the reason for it. Great talk (**RianneSchouten?**) \#amstRday https://t.co/ePZETdGvWB
</td>
</tr>
<tr>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
“What’s the fuzz about this R language?” answered by (**DerFredo?**) \#SatRday \#AmstRday https://t.co/sT3w6v2ZXX
</td>
</tr>
<tr>
<td style="text-align:left;">
Willy Tadema
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Easy access to databases in R with the dbplyr package: https://t.co/pPXkabCDiX \#AmstRday \#SatRday
</td>
</tr>
<tr>
<td style="text-align:left;">
GoDataDriven
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
(**edwin_thoen?**) Great to see that you liked it, Edwin. So did we, \#satRday Amsterdam might just become a regular thing.
</td>
</tr>
<tr>
<td style="text-align:left;">
R.A. Posthumus
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
(**jpagroenen?**) (**datafluisteraar?**) (**TransIP?**) Komt later zit nu bij \#AmstRdam \#SatRday
</td>
</tr>
<tr>
<td style="text-align:left;">
R.A. Posthumus
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Yes there are stickers \#AmstRdam \#SatRday https://t.co/ncb8Zr8Y1l
</td>
</tr>
<tr>
<td style="text-align:left;">
Jo-fai (Joe) Chow
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
.@satRdays_org workshop (**UberAmsterdam?**) \#satRdays \#satRdayAMS https://t.co/XxHW1Etym5
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
(**SuzanBaert?**) s glamour shot of her \#dplyr docs hardcopy. (**rstudio?**) , when’s the limited edition collectors hardcover coming out? \#satRdayAMS That tip about funs() being replaceable by \~ is great, btw. https://t.co/AYj5jBltqp
</td>
</tr>
<tr>
<td style="text-align:left;">
Paul Feitsma
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
(**cecilesauder?**) Will next \#amstRday be there daycaRe? Then I will also bring my kids and can they play together!
</td>
</tr>
<tr>
<td style="text-align:left;">
Cécile Sauder
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Now, Dominik Krzemiński with
“Making Shiny shine even brighter” 😎☀️☀️☀️☀️ at \#amstRday \#satRday \#rstats https://t.co/FYOMsEsh05
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Kick-off to the first \#satRdays in Amsterdam! Let’s get it started! \#amstRday \#rstats (**Tesskorthout?**) https://t.co/tzc7siIi8l
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Nick Jones from (**Uber?**) starting off the weekend with a \#tidyverse workshop. \#amstRday \#rstats \#satRdays https://t.co/XnHG6ouvhI
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Welcome (back) to Twitter! \#amstRday https://t.co/xDcOuvDUy3
</td>
</tr>
<tr>
<td style="text-align:left;">
Janine Khuc
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Couldn’t make it to \#amstRday? Don’t worry, (**rgiordano79?**) regex slides are online! Thanks for sharing! https://t.co/qw97jfycbB
</td>
</tr>
<tr>
<td style="text-align:left;">
Suthira Owlarn
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
(**StevenNooijen?**) I hope you’ll continue to tweet between now and the next \#amstRday! :)
</td>
</tr>
<tr>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
How to avoid electric vehicles charge-ups overloading the Electricity Grid With Jeroen Groot - Lightning Talk @ \#AmstRday \#rstats https://t.co/LxznG1Eptr
</td>
</tr>
<tr>
<td style="text-align:left;">
Bob
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
My \#satrday presentation on using C++ to solve sudoku’s GitHub now:
https://t.co/sJnPZCVa4J (**satRdays_org?**) Please get in touch if you have any questions, feedbacks or other shouts.
</td>
</tr>
<tr>
<td style="text-align:left;">
R.A. Posthumus
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Next up \#AmstRdam \#SatRday https://t.co/AnqE6gex5C
</td>
</tr>
<tr>
<td style="text-align:left;">
R.A. Posthumus
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
50 ways… \#AmstRdam \#SatRday https://t.co/2LoUbz1qMX
</td>
</tr>
<tr>
<td style="text-align:left;">
R.A. Posthumus
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
This wille interesting \#AmstRdam \#SatRday https://t.co/ioQ124aywn
</td>
</tr>
<tr>
<td style="text-align:left;">
Gabriel
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
This is amazing \#satRday
</td>
</tr>
<tr>
<td style="text-align:left;">
Kevin O’Brien
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Regular Expressions with Rita Giordano @ \#SatRdays amsterdam https://t.co/Pao0ycriUz
</td>
</tr>
<tr>
<td style="text-align:left;">
R.A. Posthumus
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
En we gaan starten met \#satrdays amsterdsm https://t.co/XfJiZ3Fx5v
</td>
</tr>
</tbody>
</table>

</div>

### Tweets the most retweeted

``` r
rt %>%
  select(screen_name,  retweet_count, text) %>%
  arrange(-retweet_count) -> retweet_tweets

kable(retweet_tweets) %>%
  kable_styling() %>%
  scroll_box(width = "100%", height = "200px")
```

<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:200px; overflow-x: scroll; width:100%; ">

<table class="table" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
screen_name
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
retweet_count
</th>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
text
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:right;">
45
</td>
<td style="text-align:left;">
So. Much. Useful. Stuffs. (**SuzanBaert?**) on scoped dplyr verbs! \#rstats \#AmstRday \#satRday (**satRdays_org?**)
📽 https://t.co/mLrNvjBaYG https://t.co/EIVqre9Gmj
</td>
</tr>
<tr>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:right;">
22
</td>
<td style="text-align:left;">
My slides of \#amstRday are here https://t.co/Iv5OhFV0nv. Also there is a, rather lengthy, blog post on NSE here https://t.co/dat9Uc0QR7. Questions and remarks are very welcome. \#rstats
</td>
</tr>
<tr>
<td style="text-align:left;">
RLadiesAMS
</td>
<td style="text-align:right;">
15
</td>
<td style="text-align:left;">

\#rladies awesomeness at \#amstRday

(**RladiesBrussels?**) (**RLadiesStras?**) (**RLadiesGlobal?**) (**Tesskorthout?**) (**TheSarahStolle?**) (**rgiordano79?**) (**cecilesauder?**) https://t.co/5V9hPRWG6j
</td>
</tr>
<tr>
<td style="text-align:left;">
rgiordano79
</td>
<td style="text-align:right;">
13
</td>
<td style="text-align:left;">
The slides from my presentation about \#regex in \#rstats (**satRdays_org?**) \#amstRday are available on github: https://t.co/Lnonk4p1TA
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
9
</td>
<td style="text-align:left;">
Could you not join \#amstRday or would like to look up your fav speakers slides? We will soon link the slides on our website. In the meantime, some of our speakers already made their fantastic slides available. More will be added as slides are made available \#rstats
</td>
</tr>
<tr>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:left;">
Make life easier w/ dplyr/dbplyr syntax, other 📦s … \#amstRday \#amstRday \#rstats \#dplyr \#rquery 💪 (**krlmlr?**) https://t.co/NMBCWyZJo9
</td>
</tr>
<tr>
<td style="text-align:left;">
matlabulous
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">

I forgot to say a big thank you to (**satRdays_org?**) \#rstats \#amstRday especially (**fishnets88?**) &amp; (**GoDataDriven?**) for having me again. I hope you all enjoyed a short version of \#Moneyball. See you next time :)

It was also great to meet (**dataandme?**) 🎉

\#AroundTheWorldWithH2Oai
\#360Selfie https://t.co/oYb0sVATcE
</td>
</tr>
<tr>
<td style="text-align:left;">
romain_francois
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
Open source day after \#amstRday. regex and cheatsheets. https://t.co/kmXpuPnhfa
</td>
</tr>
<tr>
<td style="text-align:left;">
stephanievdpas
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
What a great \#amstRday! Featuring Science Gossip (the journal! great find by (**dataandme?**)), the bang bang operator (**suzanbaert?**), and an entertaining talk on Non-Standard Evaluation by (**edwin_thoen?**)! https://t.co/KMWLCyOPNx
</td>
</tr>
<tr>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
Spreading the hex sticker love at \#AmstRday !! 🎉🎉 (**rweekly_org?**) (**RLadiesGlobal?**) https://t.co/QbIcK2sXF4
</td>
</tr>
<tr>
<td style="text-align:left;">
Tesskorthout
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
Love it that (**dataandme?**) mentions my favorite podcast (**NSSDeviations?**) at \#amstRday! Would love to have (**hspter?**) and (**rdpeng?**) next year! \#rstats \#satRdays https://t.co/ARyrWx34JL
</td>
</tr>
<tr>
<td style="text-align:left;">
GoDataDriven
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
The magic of data at \#AmstRday! Yesterday started with great workshops at (**Uber_NL?**). Today is full of \#R talks at the conference. It is lovely to contribute to more \#Rstats \#datascience awesomeness with (**satRdays_org?**), (**rstudio?**), (**RLadiesAMS?**), and thanks to all inspiring speakers! https://t.co/tj7GmwjQ5G
</td>
</tr>
<tr>
<td style="text-align:left;">
RLadiesAMS
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
More \#rladies power! (**rgiordano79?**) from (**RLadiesStras?**) telling us about the awesomeness of \#regex in \#rstats! \#amstRday https://t.co/rpxEAboBaG
</td>
</tr>
<tr>
<td style="text-align:left;">
smartR101
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
50 Beautiful gRaphs by Thomas Hütter using (gg)-packages e.g. waterfall, treemap, ggradar  #amstRday slides to be published on https://t.co/8Gaw4Sio9c \#satRdays https://t.co/7YBuog5Huq
</td>
</tr>
<tr>
<td style="text-align:left;">
TheSarahStolle
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
Great discovery for biological plots with large value differences
facet_zoom in ggforce \#ggplot2 \#rstats 😃 \#amstRday (**DerFredo?**) https://t.co/OTuRqpm42W
</td>
</tr>
<tr>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
.@krlmlr talking DBI (**satRdays_org?**) \#amsteRday \#rstats https://t.co/JFbQALSQjd
</td>
</tr>
<tr>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
Come back from \#AmstRday, \#Rbaby 👶 Lexie put her new \#RLadies sticker on her 💻 to work with mummy. https://t.co/18vuAuSRTG
</td>
</tr>
<tr>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
Rita Giordano talks about
Regulars Expressions in \#rstats 👍 at \#AmstRday
\#satRday https://t.co/N8Hb2rfJ1M
</td>
</tr>
<tr>
<td style="text-align:left;">
matlabulous
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
(**RLadiesAMS?**) (**RladiesBrussels?**) (**RLadiesStras?**) (**RLadiesGlobal?**) (**Tesskorthout?**) (**TheSarahStolle?**) (**rgiordano79?**) (**cecilesauder?**) (**SuzanBaert?**) (**dataandme?**) (**Janinekhuc?**) (**IlsePit?**) \#rladies \#amstRday \#360selfie 🤳🏻😎 https://t.co/zR5hhnzuYn
</td>
</tr>
<tr>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
Longhow Lam giving a lightning talk on text2vec with \#rstats : predicting house prices \#AmstRday https://t.co/8de0ibGpqa
</td>
</tr>
<tr>
<td style="text-align:left;">
IlsePit
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
(**SuzanBaert?**) casually blowing my mind by teaching us about scoped dplyr functions 🙌 \#amstRday \#satRdays \#rstats https://t.co/UqMCVbYRZm
</td>
</tr>
<tr>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
Data science-ing by (**dataandme?**) at \#amstRday 😁 https://t.co/sN9pnMSeS1
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
Joe-Fai Chow (**matlabulous?**) introduces the moneyball app developed using R, Shiny and H2O AutoML \#rstats \#amstRday \#h2oai \#rshiny \#lime (**h2oai?**) https://t.co/7A7oSNfScz
</td>
</tr>
<tr>
<td style="text-align:left;">
dataandme
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
💘🙏🌷 to everyone who made (**satRdays_org?**) \#AmstRday such a 💥! (**GoDataDriven?**) (**fishnets88?**) (**Janinekhuc?**) (**Tesskorthout?**) (**RConsortium?**) &amp;co 👋🇳🇱 https://t.co/zBBPZMYkpi
</td>
</tr>
<tr>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
You should check out the tmap package if you want to make beautiful maps in R https://t.co/hYORmmyTel \#SatRday \#AmstRday
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
(**SuzanBaert?**) starting off with sharing her excitement about \#amstRday ! Get ready, she’s sharing all her \#dplyr secrets with us! ’Getting more out of dplyr‘ \#rstats https://t.co/XJGATsQqlU
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
(**dataandme?**) finishing off with the need for all R-users of every skill level to contribute to open source to move the \#rstats community ahead! \#amstRday \#satRdays https://t.co/6ILTDPg37T
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
(**DerFredo?**) showing us how to visualise data in just about 50 different ways. \#amstRday \#rstats \#ggplot https://t.co/LZhiWvYoi3
</td>
</tr>
<tr>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
Dank u wel &amp; thank you to the attendees of my session „50 ways to show your data“ at \#amstRday. Slides and script are now available at https://t.co/ZlD26fpiZJ \#rstats /(**satRdays_org?**)
</td>
</tr>
<tr>
<td style="text-align:left;">
RLadiesAMS
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
(**RladiesBrussels?**) power at \#amstRday ! Great talk by (**SuzanBaert?**) on how to get more out of dplyr. \#rstats \#rladies https://t.co/yOHq8wCyWO
</td>
</tr>
<tr>
<td style="text-align:left;">
smartR101
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
Nice - mice::ampute now they also eat your data next to your cheese (at random and not at random) \#amstRday thanks to https://t.co/zRShbLhCJs https://t.co/iAMKjU6IUJ
</td>
</tr>
<tr>
<td style="text-align:left;">
RMHoge
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
The \#amstRday is on its way! Today tutorials, tomorrow speakers and on sunday we can hack together, for instance to create \#rstats 📦.  
(**satRdays_org?**) https://t.co/2aG87Q1Sur https://t.co/TnEVyVvjCE
</td>
</tr>
<tr>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
Also love the quote (**dataandme?**) shared on being kind to beginners \#amstRday https://t.co/1NACHNncVG
</td>
</tr>
<tr>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
Check out these great tutorials by (**SuzanBaert?**): https://t.co/xThpY7UIZp Tomorrow her slides will also be online https://t.co/ELMuCaRXto \#AmstRday \#SatRday
</td>
</tr>
<tr>
<td style="text-align:left;">
TheStephLocke
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
Super excited today as \#SQLSatOslo and \#amstRday main events are happening. Big shout out to the organisers of both who’ve done amazing jobs - if you’re around you should thank them as it’s a purely volunteer role!
</td>
</tr>
<tr>
<td style="text-align:left;">
romain_francois
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
Any \#rstats people going to \#satrdays with a stroller to lend for a few days? (**AirFranceKLM?**) lost ours between Nantes and Amsterdam 🤷‍♂️
</td>
</tr>
<tr>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
(**SuzanBaert?**) talk about
“Getting more out of \#dplyr” at \#amstRday
\#rstats https://t.co/cGdqWwTjvb
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Excited to kick off the first \#satRdays in Amsterdam. Follow \#amstRday for updates over the weekend- brilliant minds coming together to learn, teach and discuss \#rstats https://t.co/19lOvaxhD9
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Lexie, our youngest and most motivated workshop attendee \#rstats \#amstRday \#satRday https://t.co/cB9ByN03Um
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Dominik Krzemiński sharing with us how to make your shiny apps shine even brighter ! \#rstats \#amstRday \#rshiny https://t.co/HCzzystHVy
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Our dearly loved mtcars dataset. (**DerFredo?**) so, who actually thinks lollipop charts are cute? \#amstRday \#ggplot \#rstats https://t.co/7TrGbWcgVY
</td>
</tr>
<tr>
<td style="text-align:left;">
paulusj8
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Running (**DerFredo?**)’s code with those great hand-made lollipop-charts from last weekend’s \#AmstRday. It was fun and I learned a lot! \#rstats https://t.co/q904gpcBBY
</td>
</tr>
<tr>
<td style="text-align:left;">
S_Owla
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Huge thanks to everyone involved in organising \#amstRday! I learned so much, met so many awesome \#rstats people (including many (**RLadiesAMS?**)) and had so much fun!! My first but definitely not my last (**satRdays_org?**) event!! :D
</td>
</tr>
<tr>
<td style="text-align:left;">
matlabulous
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">

After \#amstRday, I am bringing the (**h2oai?**) (**IBMDataScience?**) (**Aginity?**) \#Moneyball to \#Oslo. Come and join us tomorrow ⚾️🇳🇴

\#AroundTheWorldWithH2Oai
\#AutoML \#XAI \#Shiny \#rstats https://t.co/MwcafHE6SP
</td>
</tr>
<tr>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Hmm, so (**TheStephLocke?**) is almost around the corner 😀 or at least (**LockeData?**) is \#amstRday https://t.co/LTCyHKaicV
</td>
</tr>
<tr>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Dominik (not on Twitter - yet) came all the way from Cardiff (not Poland 😉) to \#amstRday to make Shiny shine even more. \#rstats https://t.co/g07YOFZUB5
</td>
</tr>
<tr>
<td style="text-align:left;">
veerlevanson
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
I received my first hex sticker yesterday! \#amstRday \#rladies https://t.co/tDrfI6CXBI
</td>
</tr>
<tr>
<td style="text-align:left;">
romain_francois
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Getting more out of \#dplyr, (**SuzanBaert?**) \#amstRday \#satrdays \#rstats \#tidyverse https://t.co/zLDLuXPnM9
</td>
</tr>
<tr>
<td style="text-align:left;">
infotroph
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
My highlight of the morning at \#amstRday: (**SuzanBaert?**) with a exceptionally clear walk-through of the scoped dplyr verbs. Slides at https://t.co/I4fc2ySWtl, but look for video — her explanations are outstanding.
</td>
</tr>
<tr>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
That’s a wrap for \#AmstRday 2018. Great conference. https://t.co/JqrPHgZMc8
</td>
</tr>
<tr>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Jo Fai Chow from (**h2oai?**) talks Baseball and Moneyball @ \#AmstRday \#satrdays https://t.co/s8CJAKl02o
</td>
</tr>
<tr>
<td style="text-align:left;">
smartR101
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
An exploration of NSE and tidyeval by Edwin Thoen https://t.co/TAHYEKPXGp, \#amstRday https://t.co/7xsYGW9w65, nice to be a Koala and get it all explained https://t.co/lXxYXCTpoO
</td>
</tr>
<tr>
<td style="text-align:left;">
smartR101
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
BIG thanks to Bob Jansen and \#amstRday for solving the hardest puzzles this \#satRday https://t.co/8Gaw4Sio9c, a lot to digest https://t.co/yIIWveIwKy
</td>
</tr>
<tr>
<td style="text-align:left;">
RMHoge
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
After explaining text2vec, (**longhowlam?**) gives us an important lesson: “always check your results with the business, or in this case my wife” \#AmstRday https://t.co/HwQgzhK5Oj
</td>
</tr>
<tr>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
For people who don’t know SQL, or are learning it, (**krlmlr?**) shared a nice trick to get a query from R code with dbplyr \#amstRday https://t.co/E9tOZFdjko
</td>
</tr>
<tr>
<td style="text-align:left;">
TheSarahStolle
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
R \#dplyr has bang bang 💥!! functions 💥!! 😄#awesomeR \#rstats \#amstRday (**SuzanBaert?**)
</td>
</tr>
<tr>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
.@edwin_thoen: “Why should you care about how NSE (non-standard evaluation) works? because most R users slip into tool design sooner or later” \#SatRday \#AmstRday
</td>
</tr>
<tr>
<td style="text-align:left;">
semakaran
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
\#amstRday \#rstats keynote talk from (**dataandme?**) 👩🏻‍💻🤗 https://t.co/YIfA6vn8fg
</td>
</tr>
<tr>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Thomas Hütter shows us
50 ways to show our data 💹📈📉📊 at \#AmstRday \#satRday \#rstats https://t.co/OXB6trV6EW
</td>
</tr>
<tr>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
(**krlmlr?**) talk at \#amstRday \#rstats https://t.co/L8ZPe3Ou5o
</td>
</tr>
<tr>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
And last but not least… Bob Jansen 
tells us how to solve sudoku with Rcpp at \#AmstRday
\#SatRday
\#rstats https://t.co/UatXYQBcpn
</td>
</tr>
<tr>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
(**sholderer?**) Olga talks about
Using R/ R Markdown to create individual reports at \#amstRday
\#SatRday
\#rstats
Hey (**DavidGohel?**) , it’s about your work 😁 https://t.co/ydLHzcm8xU
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Our keynote (**dataandme?**) . Starting the day with ‘That’s not \[data\] science.’ \#amstRday \#rstats https://t.co/BBN8T5piKu
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Kick-off to the first \#satRdays in Amsterdam! Let’s get it started! \#amstRday \#rstats (**Tesskorthout?**) https://t.co/tzc7siIi8l
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Check out the full emoji featured programme for \#amstRday \#rstats https://t.co/wMFjC8GoN4
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Don’t miss your chance to get some awesome stickers sponsored by (**rstudio?**) and (**LockeData?**) \#amstRday \#rstats https://t.co/E1M9ZvPKLB
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
After a great lunch, let’s continue with (**edwin_thoen?**) ‘An exploration of NSE and tidyeval’ \#rstats \#amstRday https://t.co/UuTbmgJkwS
</td>
</tr>
<tr>
<td style="text-align:left;">
rgiordano79
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Going back to Strasbourg. Thanks the organiser of (**satRdays_org?**) \#amstRday (**GoDataDriven?**) and (**LockeData?**) for sponsoring the event. Very well organised! I really enjoyed!
</td>
</tr>
<tr>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Had a fabulous day yesterday at the very first \#amstRday! Would be delighted if this became a regular thing. Many thanks to the organising committee and (**GoDataDriven?**) for the venue.
</td>
</tr>
<tr>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
I thought the 10-minute lightening talks at \#amstRday were so much more informative and entertaining than the usual 5-minute versions. Just saying (**UseR2019_Conf?**) \#rstats
</td>
</tr>
<tr>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Last round of lightning tasks at \#amstRday started by Rianne Schouten \#rstats https://t.co/jVOFxvs3E4
</td>
</tr>
<tr>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
After lunch: (**edwin_thoen?**) about NSE and tidyeval. \#amstRday \#rstats https://t.co/9cEToYsbIA
</td>
</tr>
<tr>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Back home from a pleasant weekend in Amsterdam, big thanks go to the \#amstRday team for organizing a fantastic event and for having me as a speaker! I had a great time mingling with all of you R community members! \#rstats /(**satRdays_org?**)
</td>
</tr>
<tr>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Full room also for (**rgiordano79?**) kicking off the lightning talks at \#amstRday \#rstats https://t.co/KXltjX68Er
</td>
</tr>
<tr>
<td style="text-align:left;">
g_inberg
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Interesting talks at the first \#satRday Amsterdam! \#AmstRday. Got some of the famous stickers as well:-) \#rstats https://t.co/dUQDAu8Iwn
</td>
</tr>
<tr>
<td style="text-align:left;">
infotroph
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Highlight of the afternoon for me at \#AmstRday: Rianne Schouten showing mice::ampute, which generates missing data from a specified multivariate pattern. this looks VERY handy for testing model assumptions. https://t.co/aDs2hkahEe
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
(**matlabulous?**) knocked it out of the park with his \#mlb moneyball talk at \#amstRday using h2o, lime and shiny to make a winning team! ⚾ https://t.co/TMuObVnGi8 (retweet to fix horrible typo)
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
“Three weeks of reporting by hand for 30 reports reduced to three days of r coding and .rmd documents with parameters” \#amstRday \#rstats \#Winning
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Great examples of performant natural language processing at \#amstRday https://t.co/QHNhBCzDjv
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
“it’s hard to read a Sudoku problem into R wrong. It’s a perfect language for that”
\#amstRday
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
(**DerFredo?**) thanks for the ‘sweet’ live coding session \#amstRday https://t.co/yRYxN13VFv
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
(**rgiordano79?**) helping regular people express themselves using \#regex at \#amstRday https://t.co/UYtthIh2kz
</td>
</tr>
<tr>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
How to avoid electric vehicles charge-ups overloading the Electricity Grid With Jeroen Groot - Lightning Talk @ \#AmstRday \#rstats https://t.co/LxznG1Eptr
</td>
</tr>
<tr>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
‘Using \#rstats and R markdown for Individual Reports’ with Olga Sholderer - lightning talk @ \#AmstRday \#SatRdays https://t.co/j8smV5BLDA
</td>
</tr>
<tr>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
‘Solving Sudokus with R and C++’ With Bob Jansen at \#AmstRday \#satrdays https://t.co/VC3wx0GLWi
</td>
</tr>
<tr>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
“Generating Missing Values with Ampute” with Rianne Schouten @ \#AmstRday \#rstats https://t.co/83eJX3p6k5
</td>
</tr>
<tr>
<td style="text-align:left;">
smartR101
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Thanks (**Dominik?**) Krzemiński #amstRday very useful:
Making Shiny shine even brighter
https://t.co/UeqNRR2TYj https://t.co/GiO71d7Z00 https://t.co/qhYvcSweK3 all from https://t.co/PaH9chdk3k https://t.co/tsX1bwx1b2
</td>
</tr>
<tr>
<td style="text-align:left;">
RMHoge
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Dominik Krzemiński assures us that we can now translate your shiny apps to klingon (or other languages if you’d like) \#rstats \#amstRday https://t.co/8yyuwLWEFs
</td>
</tr>
<tr>
<td style="text-align:left;">
StevenNooijen
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Dusted off my account especially to Tweet about \#amstRday today! Great to have about a 100 R lovers here, of which 14 awesome speakers 🎉 https://t.co/c6JXcRZWB5
</td>
</tr>
<tr>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Shiny apps with multiple languages? 😱😱😱😱. I love it. Great talk by Dominik Krzemiński! \#amstRday https://t.co/blJ3SxKigc
</td>
</tr>
<tr>
<td style="text-align:left;">
TheSarahStolle
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Promising title for the next \#amstRday talk 😂 https://t.co/nJseXTaXs9
</td>
</tr>
<tr>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
.@SuzanBaert telling us about *scoped* dplyr functions. Nifty! \#AmstRday \#SatRday https://t.co/P7Cws7XTII
</td>
</tr>
<tr>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Attending \#SatRday at (**GoDataDriven?**) in Amsterdam \#AmstRday \#R https://t.co/GJQAnsvP7g
</td>
</tr>
<tr>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
“What’s the fuzz about this R language?” answered by (**DerFredo?**) \#SatRday \#AmstRday https://t.co/sT3w6v2ZXX
</td>
</tr>
<tr>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Next up: (**sholderer?**) on the power of R Markdown in creating reports in MS Word \#RMD \#AmstRday \#SatRday https://t.co/0o08Yh13H1
</td>
</tr>
<tr>
<td style="text-align:left;">
semakaran
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
\#amstRday \#satRday we’ve “got more out of dplyr” thanks to (**SuzanBaert?**) ! https://t.co/UoGBtbXdQ5
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Ready, set, go! Let’s get started with a fun weekend! A bunch of curious people ready to learn all about tidyverse &amp; webscraping! \#amstRdays \#rstats \#satRdays https://t.co/qjcuNFosdC
</td>
</tr>
<tr>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
✈️➡️ \#satRdays Amsterdam https://t.co/uCxfPITLHm
</td>
</tr>
<tr>
<td style="text-align:left;">
romain_francois
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
⬆️ your 🤚 if you know what a \#tibble is. Survey during (**krlmlr?**) \#dbi talk at \#satRdayAMS 👶🤚 https://t.co/en42gNKaSz
</td>
</tr>
<tr>
<td style="text-align:left;">
romain_francois
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
\#satRdayAMS at (**GoDataDriven?**) https://t.co/89R3cYtTOG
</td>
</tr>
<tr>
<td style="text-align:left;">
rgiordano79
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
Only few hours and I will be in Amsterdam for the \#satRdayAMS. Looking forward to talk about \#regex in \#rstats 😊
</td>
</tr>
<tr>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Guess who I finally got to meet today at \#amsteRday! https://t.co/CC5iDghizR
</td>
</tr>
<tr>
<td style="text-align:left;">
PaulFeitsma
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
(**cecilesauder?**) Will next \#amstRday be there daycaRe? Then I will also bring my kids and can they play together!
</td>
</tr>
<tr>
<td style="text-align:left;">
PaulFeitsma
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Really enjoyed the talks last weekend at \#satRDays in \#AmstRday with (**dataandme?**) (**SuzanBaert?**) (**rgiordano79?**) (**GoDataDriven?**) and more \#satRdayAMS
</td>
</tr>
<tr>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
\#amstRday \#rstats (**dataandme?**) keynote https://t.co/hu45Wkb8qk
</td>
</tr>
<tr>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Now, Dominik Krzemiński with
“Making Shiny shine even brighter” 😎☀️☀️☀️☀️ at \#amstRday \#satRday \#rstats https://t.co/FYOMsEsh05
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
\#amstRday beautiful view, networking &amp; drinks https://t.co/1Z2jBrSTRd
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Nick Jones from (**Uber?**) starting off the weekend with a \#tidyverse workshop. \#amstRday \#rstats \#satRdays https://t.co/XnHG6ouvhI
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
And next up, is (**sholderer?**) showing us how to create pretty reproducible reports with \#rmarkdown in \#rstats \#amstRday https://t.co/mEQUMOpFxd
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Welcome (back) to Twitter! \#amstRday https://t.co/xDcOuvDUy3
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Coffee time ☕️, before we continue with our ✨⚡️ lightning talks! \#amstRday \#rstats https://t.co/Ch1fgOLuqJ
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Thanks for joining us for a fantastic kick-off of the first \#amstRday conference! It was truly awe inspiring! https://t.co/7RYE80Gte5
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Jeroen Groot tells us about analysis of data to get insights about smart charging of electric cars. \#AmstRday \#rstats https://t.co/DLVbmWdsJO
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Pieter Marcus discussing ‘Why you shouldn’t use ROC curves to assess the business value of your model!’ - an r package that makes it easier to communicate your ML results to non-tech people \#modelplotR \#rstats \#amstRday https://t.co/oI5oO0fAca
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
2nd ⚡️-talk (**longhowlam?**) showing us how to use text2vec for fun projects \#rstats \#amstRday https://t.co/aLL9FkWMG3
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Couldn’t make it to \#amstRday? Don’t worry, (**rgiordano79?**) regex slides are online! Thanks for sharing! https://t.co/qw97jfycbB
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
The final fun⚡️talk, solving sudokus with \#rcpp by Bob Jansen! \#amstRday \#rstats https://t.co/NFR1lB2jez
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Next up, (**krlmlr?**) on the most ‘Recent development in R’s database interface’ \#amstRday \#rstats https://t.co/V3TjS0Rm4o
</td>
</tr>
<tr>
<td style="text-align:left;">
paulusj8
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
.@longhowlam explaining how to predict house prices with the text2vec package. \#AmstRday https://t.co/YAErIzwsym
</td>
</tr>
<tr>
<td style="text-align:left;">
S_Owla
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
(**WeAreRLadies?**) (**JennyBryan?**) (**g3rv4?**) (**DesiNavadeh?**) (**romain_francois?**)’ and (**cecilesauder?**)’s \#rbaby was a delightful part of \#amstRday over the weekend! :D
</td>
</tr>
<tr>
<td style="text-align:left;">
S_Owla
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
(**StevenNooijen?**) I hope you’ll continue to tweet between now and the next \#amstRday! :)
</td>
</tr>
<tr>
<td style="text-align:left;">
edwin_thoen
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
🤬😡🤬, hit by de flu right before \#amstRday. Would be so gutted to miss it. Hope I can make it by drugging-up tomorrow. Pfff… \#rstats \#fyouflu
</td>
</tr>
<tr>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
It’s (**dataandme?**) taking the stage for the opening keynote of \#amstRday \#rstats https://t.co/aRjyltgXZ3
</td>
</tr>
<tr>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Next up for his \#amstRday session on recent DBI development is (**krlmlr?**) \#rstats https://t.co/Owpj8kz3iS
</td>
</tr>
<tr>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Starting off for my first ever \#SatRday \#amstRday /(**satRdays_org?**) https://t.co/WR2zrJmQQe
</td>
</tr>
<tr>
<td style="text-align:left;">
DerFredo
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Taking \#amstRday to the next round: (**SuzanBaert?**) getting more out of dplyr. \#rstats https://t.co/msg8FTnGzv
</td>
</tr>
<tr>
<td style="text-align:left;">
HoogvlietsR
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">

(**matlabulous?**) (**dataandme?**) (**satRdays_org?**) (**fishnets88?**) (**GoDataDriven?**) Oh no, can’t believe I missed this, right in my own city 😑.

Looks really great! Where do I sign up for the next one? \#AmstRday
</td>
</tr>
<tr>
<td style="text-align:left;">
MadelijnBazen
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Excellent \#satRday conference, with excellent \#rstats takeaways :) Thank you \#AmstRday and \#RLadies! https://t.co/hXC2c2gkMn
</td>
</tr>
<tr>
<td style="text-align:left;">
MadelijnBazen
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Great \#amstRday keynote talk ‘That’s not \[data\] science!’ by (**dataandme?**)! Learning new words like ex•o•ter•ic and Rgossip..Definitely worth taking the 7:30 train on a \#satRday! https://t.co/ixPUJL7z4A
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
(**edwin_thoen?**) setting up a great punchline for an extended coding joke in \#amstRday about non-standard eval https://t.co/2f1TpFKqgm
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Or come find me at \#amstRday . I’m wearing the same shirt as Oz in this picture, but I have more hair and am in Amsterdam. https://t.co/wjiAyUc0F9
</td>
</tr>
<tr>
<td style="text-align:left;">
FlorisPadt
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
(**edwin_thoen?**) Thanks (**EdwinThoen?**) for coming despite of flu and giving a talk on steroids \#amstRday about tidyeval interesting, mind boggling and entertaining,
</td>
</tr>
<tr>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
‘Why ROC curves are unfit for business modelling’ with Pieter Marcus @ \#AmstRday. Check out the modelplotR package. \#SatRdays https://t.co/kn7u8Rkoid
</td>
</tr>
<tr>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Very impressed with the \#AmstRday venue. Fair play to (**GoDataDriven?**) for providing a great venue. \#AmstRday \#RStats https://t.co/qiAyoYaGUx
</td>
</tr>
<tr>
<td style="text-align:left;">
RLadiesAMS
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Excited to see \#Rladies at \#amstRday ! https://t.co/0FOgCTXuxu
</td>
</tr>
<tr>
<td style="text-align:left;">
hspter
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
(**Tesskorthout?**) (**dataandme?**) (**NSSDeviations?**) (**rdpeng?**) aww yay!! that makes my morning!! =) (uh and would LOVE to come to Amsterdam!) \#amstRday
</td>
</tr>
<tr>
<td style="text-align:left;">
RMHoge
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Bob Jansen: Solved the world’s hardest sudoku within a minute with pure R. And thought: that can be done faster. Let’s use Rcpp! \#AmstRday
</td>
</tr>
<tr>
<td style="text-align:left;">
RMHoge
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">

Rita slashes through shopping lists with R.

Regular expressions made easy by Rita Giordano \#AmstRday
</td>
</tr>
<tr>
<td style="text-align:left;">
RMHoge
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">

Did I just tweet the entire Saturday program for \#amstRday ? 🙀

Yes! https://t.co/BfP60hVWyp
</td>
</tr>
<tr>
<td style="text-align:left;">
StevenNooijen
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Always good to think about why data is missing, and what’s the reason for it. Great talk (**RianneSchouten?**) \#amstRday https://t.co/ePZETdGvWB
</td>
</tr>
<tr>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
(**edwin_thoen?**) working through a big cold to share something not quite that straightforward. \#hatsoff \#AmstRday https://t.co/TI658PtSze
</td>
</tr>
<tr>
<td style="text-align:left;">
SuzanBaert
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Two talks done at \#amstRday! (**dataandme?**) had a terrific talk showing how even the word “scientist” was controversial 🎉
</td>
</tr>
<tr>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Now Rita Giordano’s lightning talk on regular expressions in R. “Learn RegEx. Do not copy, paste, remove… Use RegEx!” \#AmstRday \#SatRday https://t.co/e50SIDBLF5
</td>
</tr>
<tr>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Next up, (**SuzanBaert?**)‘s talk on ’Getting more out of dplyr’ \#SatRday \#AmstRday https://t.co/5Qv75uwyzC
</td>
</tr>
<tr>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Two hobby projects from (**longhowlam?**) using the text2vec package https://t.co/mx3L3qUpdV &amp; https://t.co/enqIko18cR \#textmining \#AmstRday \#SatRday
</td>
</tr>
<tr>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Other R packages for working with databases in R mentioned by (**krlmlr?**) \#SatRday \#AmstRday https://t.co/qcNrP8g0xB
</td>
</tr>
<tr>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Next up, (**krlmlr?**) with his talk on the DBI package, R’s database interface https://t.co/9Q1Ua910cS \#AmstRday \#SatRday
</td>
</tr>
<tr>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Easy access to databases in R with the dbplyr package: https://t.co/pPXkabCDiX \#AmstRday \#SatRday
</td>
</tr>
<tr>
<td style="text-align:left;">
IlsePit
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
So hyped about this! (And less scared than I look, I promise :D ) \#amstRday https://t.co/bZ9LqxzLZB
</td>
</tr>
<tr>
<td style="text-align:left;">
Tesskorthout
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
So far the woRkshop is awesome! So excited for \#amstRday! https://t.co/zDCb9D5Gzo
</td>
</tr>
<tr>
<td style="text-align:left;">
Bootvis
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
My \#satrday presentation on using C++ to solve sudoku’s GitHub now:
https://t.co/sJnPZCVa4J (**satRdays_org?**) Please get in touch if you have any questions, feedbacks or other shouts.
</td>
</tr>
<tr>
<td style="text-align:left;">
GoDataDriven
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
(**edwin_thoen?**) Great to see that you liked it, Edwin. So did we, \#satRday Amsterdam might just become a regular thing.
</td>
</tr>
<tr>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
.@dataandme: “It’s important that newcomers contribute. We need people that contribute on all levels.” \#AmstRdam \#SatRday
</td>
</tr>
<tr>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Kick-off with (**dataandme?**)‘s keynote telling us to ’LeaRn Out Loud’ \#AmstRdam \#SatRday https://t.co/33n5B1SVJu
</td>
</tr>
<tr>
<td style="text-align:left;">
FrieseWoudloper
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
“What does doing data science look like?” (**rdpeng?**) wrote an interesting book on this topic: ‘Putting It All Together: Essays on Data Analysis’ https://t.co/8LiOE61oXc \#AmstRdam \#SatRDay
</td>
</tr>
<tr>
<td style="text-align:left;">
RAPOSTHUMUS
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Next up \#AmstRdam \#SatRday https://t.co/AnqE6gex5C
</td>
</tr>
<tr>
<td style="text-align:left;">
RAPOSTHUMUS
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
50 ways… \#AmstRdam \#SatRday https://t.co/2LoUbz1qMX
</td>
</tr>
<tr>
<td style="text-align:left;">
RAPOSTHUMUS
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
(**jpagroenen?**) (**datafluisteraar?**) (**TransIP?**) Komt later zit nu bij \#AmstRdam \#SatRday
</td>
</tr>
<tr>
<td style="text-align:left;">
RAPOSTHUMUS
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Yes there are stickers \#AmstRdam \#SatRday https://t.co/ncb8Zr8Y1l
</td>
</tr>
<tr>
<td style="text-align:left;">
RAPOSTHUMUS
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
This wille interesting \#AmstRdam \#SatRday https://t.co/ioQ124aywn
</td>
</tr>
<tr>
<td style="text-align:left;">
oliverowner
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
This is amazing \#satRday
</td>
</tr>
<tr>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
(**RoryJosephQuinn?**) (**GalwayRusers?**) (**statsepi?**) (**jaynal83?**) A \#SatRdays in West of Ireland sometime? (**EngineLimerick?**) would make a nice venue https://t.co/DJAddmLyXS
</td>
</tr>
<tr>
<td style="text-align:left;">
dragonflystats
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Regular Expressions with Rita Giordano @ \#SatRdays amsterdam https://t.co/Pao0ycriUz
</td>
</tr>
<tr>
<td style="text-align:left;">
romain_francois
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Never too early to attend a \#satRdays \#rstats conference. \#rbaby 👶 https://t.co/gx7U8k3CVU
</td>
</tr>
<tr>
<td style="text-align:left;">
Janinekhuc
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Next up, Gilian Porte on scraping the internet with R. \#amstRdam \#satRdays \#rstats https://t.co/JwE2TRcujO
</td>
</tr>
<tr>
<td style="text-align:left;">
cecilesauder
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
(**dataandme?**) Mara at \#satRdays \#SatRdayAmsterdam https://t.co/ruguTvAi0Z
</td>
</tr>
<tr>
<td style="text-align:left;">
RAPOSTHUMUS
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
En we gaan starten met \#satrdays amsterdsm https://t.co/XfJiZ3Fx5v
</td>
</tr>
<tr>
<td style="text-align:left;">
matlabulous
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
.@satRdays_org workshop (**UberAmsterdam?**) \#satRdays \#satRdayAMS https://t.co/XxHW1Etym5
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
(**SuzanBaert?**) s glamour shot of her \#dplyr docs hardcopy. (**rstudio?**) , when’s the limited edition collectors hardcover coming out? \#satRdayAMS That tip about funs() being replaceable by \~ is great, btw. https://t.co/AYj5jBltqp
</td>
</tr>
<tr>
<td style="text-align:left;">
DaveParr
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:left;">
Had a great week in London learning \#cosmosdb. Now to Amsterdam for \#satRdayAMS \#rstats.
</td>
</tr>
</tbody>
</table>

</div>

### words frequency in the tweets

``` r
#tokenization 
tib_words <- rt %>%
  select(name, status_id, text) %>%
  unnest_tokens(output = "word",
                input = text,
                token = "tweets")
```

    ## Using `to_lower = TRUE` with `token = 'tweets'` may not preserve URLs.

``` r
#remove stop_words

tib_words_signifiant <- tib_words %>%
  anti_join(stop_words, by=c("word"))


#remove hashtags and urls

tib_words_signifiant <- tib_words_signifiant %>%
  filter(!str_detect(word, "http")) %>%
  filter(!str_detect(word, "#"))


#frequency

freq_words <- tib_words_signifiant %>%
  group_by(word) %>%
  summarise(freq=n()) %>%
  arrange(-freq) %>%
  filter(freq > 3)

freq_words %>%
  kable() %>%
  kable_styling() %>%
  scroll_box(width = "100%", height = "200px")
```

<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:200px; overflow-x: scroll; width:100%; ">
<table class="table" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
word
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
freq
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
talk
</td>
<td style="text-align:right;">
22
</td>
</tr>
<tr>
<td style="text-align:left;">
(**dataandme?**)
</td>
<td style="text-align:right;">
17
</td>
</tr>
<tr>
<td style="text-align:left;">
(**suzanbaert?**)
</td>
<td style="text-align:right;">
15
</td>
</tr>
<tr>
<td style="text-align:left;">
amsterdam
</td>
<td style="text-align:right;">
13
</td>
</tr>
<tr>
<td style="text-align:left;">
data
</td>
<td style="text-align:right;">
13
</td>
</tr>
<tr>
<td style="text-align:left;">
(**satrdaysorg?**)
</td>
<td style="text-align:right;">
11
</td>
</tr>
<tr>
<td style="text-align:left;">
slides
</td>
<td style="text-align:right;">
11
</td>
</tr>
<tr>
<td style="text-align:left;">
dplyr
</td>
<td style="text-align:right;">
10
</td>
</tr>
<tr>
<td style="text-align:left;">
talks
</td>
<td style="text-align:right;">
10
</td>
</tr>
<tr>
<td style="text-align:left;">
(**godatadriven?**)
</td>
<td style="text-align:right;">
9
</td>
</tr>
<tr>
<td style="text-align:left;">
(**edwinthoen?**)
</td>
<td style="text-align:right;">
8
</td>
</tr>
<tr>
<td style="text-align:left;">
(**krlmlr?**)
</td>
<td style="text-align:right;">
8
</td>
</tr>
<tr>
<td style="text-align:left;">
shiny
</td>
<td style="text-align:right;">
8
</td>
</tr>
<tr>
<td style="text-align:left;">
(**rgiordano79?**)
</td>
<td style="text-align:right;">
7
</td>
</tr>
<tr>
<td style="text-align:left;">
lightning
</td>
<td style="text-align:right;">
7
</td>
</tr>
<tr>
<td style="text-align:left;">
package
</td>
<td style="text-align:right;">
7
</td>
</tr>
<tr>
<td style="text-align:left;">
people
</td>
<td style="text-align:right;">
7
</td>
</tr>
<tr>
<td style="text-align:left;">
amp
</td>
<td style="text-align:right;">
6
</td>
</tr>
<tr>
<td style="text-align:left;">
keynote
</td>
<td style="text-align:right;">
6
</td>
</tr>
<tr>
<td style="text-align:left;">
love
</td>
<td style="text-align:right;">
6
</td>
</tr>
<tr>
<td style="text-align:left;">
regular
</td>
<td style="text-align:right;">
6
</td>
</tr>
<tr>
<td style="text-align:left;">
weekend
</td>
<td style="text-align:right;">
6
</td>
</tr>
<tr>
<td style="text-align:left;">
(**derfredo?**)
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
(**tesskorthout?**)
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
🎉
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
50
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
bob
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
check
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
conference
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
dominik
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
fun
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
jansen
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
krzemiński
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
nse
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
reports
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
rita
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
science
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
speakers
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
text2vec
</td>
<td style="text-align:right;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">

-   </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    ☀️
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    😱
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    awesome
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    bang
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    contribute
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    excited
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    expressions
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    kick
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    learn
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    nice
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    regex
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    satrdaysorg
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    scoped
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    sharing
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    shine
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    started
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    starting
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    tidyeval
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    tomorrow
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    venue
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    <tr>
    <td style="text-align:left;">
    workshop
    </td>
    <td style="text-align:right;">
    4
    </td>
    </tr>
    </tbody>
    </table>
    </div>

``` r
#wordcloud

pal <- brewer.pal(9,"Set1")
pal <- pal[-6]
wordcloud(freq_words$word,
          freq_words$freq,
          min.freq=2, 
          colors = pal,
          random.order = FALSE)
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-9-1.png" width="672" />

### Words relation

``` r
# words_cooc <- tib_words_signifiant %>%
#   pairwise_count(word, feature = name, sort = TRUE)
# words_cors <- tib_words_signifiant %>%
#   pairwise_cor_(word, feature = name, sort = TRUE)

#doesn't work with the pipe, I don't know why


words_cooc <- pairwise_count(tib_words_signifiant, word, name, sort=TRUE)
words_cors <- pairwise_cor(tib_words_signifiant, word, name, sort = TRUE)

words_cooc <- left_join(words_cooc,
                       words_cors,
                       by=c("item1","item2")) %>%
                filter(correlation > 0.6 ) %>%
                filter(n > 2)


words_graph <- graph_from_data_frame(words_cooc)

my_graph <- words_graph %>%
   ggraph(layout = "fr") +
   geom_edge_link(edge_colour="steelblue") +
   geom_node_point(color = "khaki1", size = 5) +
   geom_node_text(aes(label = name), repel = TRUE) +
   theme_void()

my_graph
```

    ## Warning: Using the `size` aesthetic in this geom was deprecated in ggplot2 3.4.0.
    ## ℹ Please use `linewidth` in the `default_aes` field and elsewhere instead.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-10-1.png" width="672" />

\###Photos gallery of tweets

``` r
photos <- na.exclude(unlist(rt$media_url))

#include_graphics(photos)
```
