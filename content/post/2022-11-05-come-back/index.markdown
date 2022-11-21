---
title: Come back...
author: Cécile Sauder
date: '2022-11-05'
slug: []
categories: []
tags: [comeback]
description: ''
topics: [blogdown, comeback]
header: "/img/back_dr-who-doctor-who.gif"
---


## Mise à jour 

Voilà, voilà, depuis le dernier post y a 4 ans il s'est passé beaucoup de choses,
je mettrais le "About" à jour parcequ'il est vraiment à revoir :'D


J'ai carrément tout repris à zero, crée un nouveau repo Github. 


J'ai donc recrée un blog tout vide, puis tenté d'avoir le même aspect que l'ancien... 
Nous voilà donc 2 jours plus tard 😅

Si tu veux plus de détails tu peux aller voir les [25 commits](https://github.com/cecilesauder/blog_CS/commits/main) que j'ai fait
pour en arriver là 😅


## Eternels problèmes de GIT

😠 "GRRR encore et encore pareil, j'ai 20 commits, 
tout va bien, et pas moyen de faire un push..."

Alors cet énervement venait du fait qu'à chaque fois j'ai des soucis pour pouvoir
faire des push que j'attribue à RStudio alors que non, juste le SSH mal configuré. 

Ça me demande mon identifiant et mot de passe HTTPS et quand je le tape : 
"FAIL AUTHENTIFICATION"...

<div class="tenor-gif-embed" data-postid="26051038" data-share-method="host" data-aspect-ratio="1.31148" data-width="30%"><a href="https://tenor.com/view/annoyed-disappointed-mad-upset-gif-26051038">Annoyed Disappointed GIF</a>from <a href="https://tenor.com/search/annoyed-gifs">Annoyed GIFs</a></div> <script type="text/javascript" async src="https://tenor.com/embed.js"></script>

La solution pour gérer ça a été de changer l'url (qui était en HTTPS) pour mettre
celle en SSH, soit dans mon cas : 


```bash
git remote set-url origin git@github.com:cecilesauder/blog_CS.git
```

Après le push marche beaucoup mieux, 'fin il marche tout court, y compris 
depuis RStudio.



## Problème de balise HTML qui n'affiche rien

Insérer le GIF avec sa balise `HTML` me qui me fait penser à un autre truc qui 
m'a bien soulée cette nuit, mes balises n'étaient pas prises en compte 
(en aurais-je déjà parlé dans le About et déjà oublié ? possible...)

Enfin ce problème là avait déjà été corrigé grâce à `blogdown::check_site()` sur 
l'ancien blog, mais comme j'avais pas compris j'avais viré les lignes créées,
en fait faut rajouter un markup dans le `config.toml`

Y a la solution [ICI](https://stackoverflow.com/questions/63198652/hugo-shortcode-ignored-saying-raw-html-omitted) si toi aussi t'en chies 😜


## Problème des icones dans Contact

J'ai aussi des soucis avec les icones font
awesome de contacts (j'aurais mien mis des icones ici mais du coup non).

Sûrement une trop vieille version appelée dans le CSS... Allez il me reste 1h 
grand max pour trouver la solution... 

<div class="tenor-gif-embed" data-postid="17677371" data-share-method="host" data-aspect-ratio="1" data-width="40%"><a href="https://tenor.com/view/waiting-cat-filing-nail-getting-ready-bring-it-on-im-listening-gif-17677371">Waiting Cat Filing Nail GIF</a>from <a href="https://tenor.com/search/waiting-gifs">Waiting GIFs</a></div> <script type="text/javascript" async src="https://tenor.com/embed.js"></script>


Alors j'ai trouvé l'endroit où la librairie est appelée c'est dans `backburn/layouts/partials/head.html`, j'ai mis le lien de la 6.2 à la place...

Suspens...


<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="800" />

Donc d'abord un FAIL, avec des carrés chelous que j'avais pas avant...
Puis j'ai cherché comment les déclarer dans des balises 
4 ans plus et en effet ça venait de là : 


<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="800" />

Mission accomplie !

## La page Topics en erreur 404...

ouais ça je sais pas ça m'agace !

Les titres ont pas forcément une bonne taille non plus, à tester dans le CSS du 
theme pour voir ce qu'il y a de mieux. 


Enfin, ça ira pour le moment j'ai accompli mon challenge avant d'aller chercher
la petite à l'école !

J'ai 2 réunions ce soir mais j'ai trop envie de remettre les anciens posts...
On verra, ptet cette nuit.


<div class="tenor-gif-embed" data-postid="11819904" data-share-method="host" data-aspect-ratio="1.55844" data-width="50%"><a href="https://tenor.com/view/talk-soon-talk-to-you-soon-later-leaving-bye-gif-11819904">Talk Soon GIF</a>from <a href="https://tenor.com/search/talk+soon-gifs">Talk Soon GIFs</a></div> <script type="text/javascript" async src="https://tenor.com/embed.js"></script>
