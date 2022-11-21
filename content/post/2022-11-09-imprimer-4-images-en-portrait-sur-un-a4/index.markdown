---
title: Imprimer 4 images en portrait sur un A4
author: Cécile Sauder
date: '2022-11-09'
tags:
  - magick
topics:
  - DataViz
header: "/img/1.png"
---

## Ou Dès fois Ubuntu, c''est un peu relou... Mais heureusement il y a R

L'idée, c'est de mettre 4 images en portrait sur une feuille A4 parce que personne
a décidé de coder ça dans le truc d'impression d'Ubuntu 😕.

Allez au boulot, on sort les 📦 et c'est parti !

- On commence par lire l'image (1.png c'est la sortie Canva jme suis pas foulée), 
et la mettre dans `img`.

- Ensuite dans `li` je mets une ligne, je colle donc deux fois mon image en 
ligne avec `image_append` 

- Et pour finir, dans `A4` je colle deux `li` à la verticale, toujours avec 
 `image_append` , mais en rajoutant l'option `stack = TRUE`, puis je mets au 
 format A4 avec ` image_scale("x3508") ` , pourquoi `x3508` ?
 
 3508 c'est le nombre de pixels correspondant à la hauteur d'un A4 en 300dpi (et 
 2480 pixels sa hauteur)


```r
library(tidyverse)
library(magick)

img <- image_read("1.png")


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

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-1.png" width="1240" />
Pis balançons (ouais on est plusieurs dans ma tête) direct le pdf quitte à faire, 
par contre à mon avis c'est très sale ce que j'ai fait...

Enfin c'est sûr faudrait faire une fonction et le coder pour 4,6,8,... Fin comme le truc bien quoi.
Mais Hadley (voir GIF haha) il a dit à partir de 3 fois, et là j'ai fait qu'un seul copier-coller à chaque fois ça passe 😁.

<div class="tenor-gif-embed" data-postid="11365139" data-share-method="host" data-aspect-ratio="1.42857" data-width="50%"><a href="https://tenor.com/view/hadley-wickham-rstats-typing-rcode-gif-11365139">Hadley Wickham GIF</a>from <a href="https://tenor.com/search/hadley-gifs">Hadley GIFs</a></div> <script type="text/javascript" async src="https://tenor.com/embed.js"></script>


Bon ensuite je sauve l'image et je choisis son nom (c'est bien pour ça 
que ça valait pas le coup de le changer avant).


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


<div class="tenor-gif-embed" data-postid="6232513" data-share-method="host" data-aspect-ratio="1.77305" data-width="100%"><a href="https://tenor.com/view/theflash-flash-dc-dccomics-cw-gif-6232513">Theflash Dc GIF</a>from <a href="https://tenor.com/search/theflash-gifs">Theflash GIFs</a></div> <script type="text/javascript" async src="https://tenor.com/embed.js"></script>


