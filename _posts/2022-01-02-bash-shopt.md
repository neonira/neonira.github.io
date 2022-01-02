---
layout: post
title: Shell <cite style='font-family:courrier;color:darkOrange'>/bin/bash</cite> et options de configuration <cite style='font-family:courrier;color:lime'>shopt</cite>
category: category-linuxverse
summary: Préconisations de configuration 
image: images/linux/bash.jpg
# comments: true
permalink: lv-shell-2
---

# Objectif 

Configurer son environnement shell de manière a être efficace, confortable et prédictible. 

La configuration par défaut n'est pas toujours la meilleure. De plus, celle-ci évolue avec la version considérée de <cite style='font-family:courrier;color:darkOrange'>/bin/bash</cite>. C'est pourquoi, mieux vaux tenter de maîtriser sa configuration afin de la
rendre reproductible et performante. 

# Configuration par défaut

La version <cite style='font-family:courrier;color:darkOrange'>/bin/bash</cite> utilisée est 

<img src='images/linux/bash-version.png' witdh="80%">

La configuration par défaut de est 

<img src='images/linux/bash-shopt-default.png' witdh="80%">


# Configuration préférentielle proposée

## Options qu'il est conseillé d'activer

Les options à activer sont positionnées par la commande <cite class='exec'>shopt -s option-name</cite>.

<table>
<tr><th><cite style='font-family:courrier;color:lime'>option shopt</cite></th><th>objet</th><th>préconisation</th><th>raisons</th></tr>
<tr><td><cite class='oc'>cdspell</cite></td><td>usage en shell interactif</td><td>on</td><td>je veux que les petites erreurs de frappes soient corrigées automatiquement par le shell lors de l'usage de la commande <cite class='exec'>cd</cite></td></tr>
<tr><td><cite class='oc'>dirspell</cite></td><td>usage en shell interactif</td><td>on</td><td>je veux que les petites erreurs de frappes soient corrigées
automatiquement par le shell</td></tr>
<tr><td><cite class='oc'>prompt_vars</cite></td><td>gestion des variables dans le prompt</td><td>on</td><td>je préfère que le shell expande les variables et les calculs dans le prompt</td></tr>
<tr><td><cite class='oc'>shift_verbose</cite></td><td>gestion des erreurs sur le nomrbe d'arguments</td><td>on</td><td>je préfère que le shell renvoie une erreur si j'excède le nombre réel d'arguments</td></tr>
<tr><td><cite class='oc'>source_path</cite></td><td>recherche fichier à sourcer</td><td>on</td><td>je préfère que le shell recherche le fichier à sourcer dans la variable <cite class='op'>PATH</cite></td></tr>
</table>


## Options laissées à votre libre arbitre

Votre choix d'activation ou de désactivation est libre. Comprenez cependant les implications de vos choix. 

<table>
<tr><th><cite style='font-family:courrier;color:lime'>option shopt</cite></th><th>objet</th><th>préconisation</th><th>raisons</th></tr>
<tr><td><cite class='oc'>nullglob</cite></td><td>extension des patterns de recherche de fichiers</td><td>on</td><td>à vous de choisir, la gestion de chaîne nulle ou égale à un pattern</td></tr>
</table>

## Options qu'il est conseillé de désactiver

Les options à déactiver sont positionnées par la commande <cite class='exec'>shopt -u option-name</cite>.

<table>
<tr><th><cite style='font-family:courrier;color:lime'>option shopt</cite></th><th>objet</th><th>préconisation</th><th>raisons</th></tr>
<tr><td><cite class='oc'>autocd</cite></td><td>usage en shell interactif</td><td>off</td><td>je veux que le changement de répertoire requiere explicitement l'usage de la commande <cite class='exec'>cd</cite></td></tr>
<tr><td><cite class='oc'>cdable_vars</cite></td><td>usage en shell interactif</td><td>off</td><td>je veux que le changement de répertoire en usage de variable SHELL expose explicitement l'usage de la variable par la syntaxe <cite class='op'>$</cite></td></tr>
<tr><td><cite class='oc'>cdspell</cite></td><td>usage en shell interactif</td><td>on</td><td>je veux que les petites erreurs de frappes soient corrigées automatiquement par le shell</td></tr>

</table>

