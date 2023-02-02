---
title: Wordcloud pour illustrer un article
author: Cécile Sauder
date: '2023-02-02'
topics:
  - DataViz
  - Text Analysis
tags:
  - wordcloud2
  - tidytext
header: "/img/eva.png"
---

### Librairies


```r
library(tidyverse)
library(tidytext)
library(pdftools)

library(proustr)
library(stopwords)
library("mixr") # Lise Vaudor package

library(magick)
library(wordcloud2)
```

## Récupérer le texte du PDF

Avec la fonction *pdf_text* du package *pdf_tools*


```r
txt <- pdf_text("Article Revue Balisages_Joëlle Le Marec et Eva Sandri_25 octobre 2022.pdf")
```

On obtient ainsi un *chr* de 17 éléments (correspondants aux 17 pages)

Une question se pose, qu'est ce que je garde, pourquoi, comment ?

Est ce que j'enlève titre et abstract ? noms d'autrice, biblio ?

L'abstract en anglais ça me parait évident, je vais aussi virer la biblio mais 
pas les noms. 

J'en profite pour enlever les 2 pages de bibliographie, c'est pourquoi je ne
garde que *txt[1:15]*


```r
zz <- textConnection(txt[1:15])  #enleve page 16 et 17

rl <- readLines(zz) # lit toutes les lignes (803)

tib<- tibble(txt = rl,
             lignes = 1:length(rl)) %>%
  filter(!lignes %in% 30:47)  #J'enleve seulement l'abstract (lignes 30 à 47)
```

On a maintenant un tableau *tib* qui contient une colonne *txt* avec du texte 
et une colonne *lignes*, avec le numéro de ligne associé (de 1 à 785)




## Nettoyage du texte 

<div class="tenor-gif-embed" data-postid="4365544" data-share-method="host" data-aspect-ratio="1.39276" data-width="100%"><a href="https://tenor.com/view/sponge-bob-cartoons-cleaning-clean-cl-gif-4365544">Clean All The Things!!!! GIF</a>from <a href="https://tenor.com/search/sponge+bob-gifs">Sponge Bob GIFs</a></div> <script type="text/javascript" async src="https://tenor.com/embed.js"></script>


C'est la partie laborieuse, je remplace les apostrophes, les chiffres, les liens 
internet, etc...


```r
tib <- tib %>%
  mutate(txt = txt %>%
           str_replace_all(pattern = "’|'", replacement =  " ") %>% #remplace apostrophe par espace
           str_replace_all(pattern = "\\d", replacement = "") %>% # remplace un chiffre par un espace
           str_remove_all("http\\S*") %>% # enlève tout ce qui commence par http
           str_remove_all("\\S*@\\S*")) %>% # enlève tout ce qui contient @
  unnest_tokens(output = "word",
                input = txt,
                token = "words",
                format = "text") %>%
  filter(str_length(word) > 1) #enleve tous les trucs de taille 1, chiffre ou character
```

J'ai maintenant un tableau *tib* de deux colonnes, *lignes* qui contient le
numéro de la ligne et *word* qui contient des mots (un par ligne). 
Ce tableau contient 6526 lignes.


### Gestion des stopwords (mots vides de sens)

J'ai utilisé ici les packages **proustr**, **stopwrds** et **mixr** (de Lise 
Vaudor)


```r
tib <- tib %>%
  filter(!word %in% proust_stopwords()) %>%
  filter(!word %in% stopwords("fr", source = "stopwords-iso"))
```

Il ne reste plus que 2971 mots qui ont du sens. Parmi ces mots ils y a bien 
sûr des adjectifs, noms, verbes... des singulier et des pluriels, que l'on 
voudrait regrouper. 

J'utilise le lexique 382 du package *mixr*,  qui contient 125721 observations,
j'ai essayé avec un lexique un peu plus récent (le 383) mais ça n'était pas 
vraiment mieux.


```r
lexique382=mixr::get_lexicon("fr")
dplyr::sample_n(lexique382,10)
```

```
## # A tibble: 10 × 3
##    word        lemma        type 
##    <chr>       <chr>        <chr>
##  1 démariée    démarier     ver  
##  2 desséchez   dessécher    ver  
##  3 idéal       idéal        adj  
##  4 story_board story_board  nom  
##  5 gâteuses    gâteux       adj  
##  6 dilution    dilution     nom  
##  7 léchèrent   lécher       ver  
##  8 reconfigure reconfigurer ver  
##  9 cuveau      cuveau       nom  
## 10 pyxides     pyxide       nom
```

```r
tib_non_vides <- tib %>%
  left_join(lexique382) %>%
  mutate(word = if_else(
    is.na(lemma),
    word,
    lemma)) %>%
  select(lignes, word)
```

```
## Joining, by = "word"
```

Je calcule ensuite la fréquence d'apparition de chaque mot 


```r
mot_freq<- tib_non_vides %>%
  count(word, sort = TRUE)


mot_freq
```

```
## # A tibble: 1,256 × 2
##    word             n
##    <chr>        <int>
##  1 savoir          40
##  2 pratique        33
##  3 public          26
##  4 conversation    24
##  5 féministe       24
##  6 espace          21
##  7 lieu            21
##  8 collectif       20
##  9 cours           20
## 10 étudiant        19
## # … with 1,246 more rows
```



## Wordcloud

J'utilise ici le package *wordcloud2* qui permet de choisir la forme de nuage
que l'on souhaite, comme j'avais fait dans le précédent post avec une forme de
canard. 

C'est un article sur le féminisme, donc j'ai choisi cette image symbolique pour
la forme du nuage.


```r
image_read("feminism.jpg") %>%
  image_scale("200x")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-8-1.png" width="100" />




```r
mot_freq %>%
  wordcloud2(figPath = "feminism.jpg",
             widgetsize = c(820,1382),
             color = "purple")
```

La fonction est souvent longue pour afficher le wordcloud donc je n'éxecute
pas le code précédent mais ça donnera comme résultat qqchose comme ça (les mots
sont placés aléatoirement mais leur taille dépend de leur fréquence donc ne 
changera pas)

![](eva.png)

Et voilà ! 


