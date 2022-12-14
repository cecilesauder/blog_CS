---
title: Playing with dplyr5000 - Part 1
author: Cécile Sauder
date: '2018-10-21'
topics:
  - DataViz
  - Github API
tags:
  - ggplot2
  - magick
  - tidyverse
header: "/img/unnamed-chunk-5-1.png"
---

**dplyr5000** is a data package with the 5000 first travis builds of **dplyr**.
I would like to make a beautiful barplot with these data, inspired by
this [tweet from Mara Averick](https://twitter.com/dataandme/status/1050355574070751233).

{{< tweet "1050355574070751233" >}}

# Packages

[**gh**](https://github.com/r-lib/gh) allows to get data from github.

``` r
# devtools::install_github("r-lib/gh")
# devtools::install_github("romainfrancois/dplyr5000")

library(gh)
library(dplyr5000)
library(tidyverse)
library(grid) 
library(magick)
```

# With the Jonathan Carroll code from [this post](https://jcarroll.com.au/2016/06/03/images-as-x-axis-labels-updated/)

``` r
## ##########
## INDEPENDENT CODE TO BE SOURCED:
## source : https://jcarroll.com.au/2016/06/03/images-as-x-axis-labels-updated/
## ##########
# user-level interface to the element grob
my_axis = function(img, angle = 90) {
  structure(
    list(img=img, angle=angle),
    class = c("element_custom", "element_blank", "element_text", "element") # inheritance test workaround
  )
}
# returns a gTree with two children: the text label, and a rasterGrob below
element_grob.element_custom <- function(element, x, ...)  {
  stopifnot(length(x) == length(element$img))
  tag <- names(element$img)
  # add vertical padding to leave space
  g1 <- textGrob(paste0(tag, "\n\n\n\n\n"), x=x, rot = element$angle, vjust=0.6)
  g2 <- mapply(rasterGrob, x=x, image=element$img[tag], 
               MoreArgs=list(vjust=0.7, interpolate=FALSE,
                             height=unit(3,"lines")),
               SIMPLIFY=FALSE)
  
  gTree(children=do.call(gList, c(g2, list(g1))), cl="custom_axis")
}
# gTrees don't know their size and ggplot would squash it, so give it room
grobHeight.custom_axis = heightDetails.custom_axis = function(x, ...)
  unit(6, "lines")
## ##########
## END
## ##########
```

## Tidying the dplyr5000 data with dplyr

I filter users with more than 40 travis builds.

``` r
# tibble with results to plot
tib <- dplyr5000 %>% 
  group_by(user) %>% 
  tally(sort = TRUE) %>%
  filter(!is.na(user), n > 40)
```

## Getting users avatar on github

``` r
get_github_avatar <- function(x){
  profil <- gh("/users/:username", username = x)
  image_read(profil[["avatar_url"]])
}

pix <- map(tib$user, get_github_avatar)

names(pix) <- tib$user
```

## Ggploting the results

``` r
tib %>%
  ggplot(aes(x= reorder(user,-n), y = n, fill = 1)) +
  geom_bar(stat = "identity") +
  guides(fill=FALSE) + 
  labs(
    title = "#dplyr travis builds",
    subtitle = "people who made more than 40 builds",
    x="", y="builds"
  ) +
  theme(axis.text.x  = my_axis(pix, angle = 0), 
        axis.text.y  = element_text(size=14),
        axis.title.x = element_blank())
```

    ## Warning: The `<scale>` argument of `guides()` cannot be `FALSE`. Use "none" instead as
    ## of ggplot2 3.3.4.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" />
