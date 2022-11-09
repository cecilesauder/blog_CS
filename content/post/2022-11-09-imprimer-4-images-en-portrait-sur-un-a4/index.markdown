---
title: Imprimer 4 images en portrait sur un A4
author: Cécile Sauder
date: '2022-11-09'
slug: []
categories: []
tags: []
description: ''
topics: []
---

# Ou Dès fois Ubuntu, c''est un peu relou... Mais heureusement il y a R

L'idée, c'est de mettre 4 images en portrait sur une feuille A4 parce que personne
a décidé de coder ça dans le truc d'impression d'Ubuntu 😕.

Allez au boulot, on sort les 📦 et c'est parti !


```r
library(tidyverse)
library(magick)

img <- image_read("1.png")

img %>%
  image_append()
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-1.png" width="707" />

```r
li <- c(img,img) %>%
  image_append()

A4 <- c(li, li) %>%
  image_append(stack = TRUE) %>%
  image_scale("x3508")

print(A4)
```

```
## # A tibble: 1 × 7
##   format width height colorspace matte filesize density
##   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
## 1 PNG     2480   3508 sRGB       TRUE         0 67x67
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-2.png" width="1240" />
Pis balançons direct le pdt quitte à faire, par contre à mon avis c'est très sale ce que j'ai fait.

Enfin c'est sûr faudrait le coder pour 4,6,8,... Fin comme le truc bien quoi.


```r
A4 %>%
  image_write(path = "2x2_flyers_recto.png", format = "png")
```

Bon ben la même pour le verso : 


```r
img <- image_read("2.png")

img %>%
  image_append()
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="707" />

```r
li <- c(img,img) %>%
  image_append()

A4 <- c(li, li) %>%
  image_append(stack = TRUE) %>%
  image_scale("x3508")

print(A4)
```

```
## # A tibble: 1 × 7
##   format width height colorspace matte filesize density
##   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
## 1 PNG     2480   3508 sRGB       TRUE         0 67x67
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-2.png" width="1240" />

```r
A4 %>%
  image_write(path = "2x2_flyers_verso.png", format = "png")
```

C'était du rapide 😅


