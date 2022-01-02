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

La configuration par défaut n'est pas toujours la meilleure. De plus, celle-ci évolue avec la version considérée de <cite style='font-family:courrier;color:darkOrange'>/bin/bash</cite>. C'est pourquoi, mieux vaux tender de maîtriser sa configuration afin de la
rendre reproductible et performante. 

# Configuration par défaut

La version <cite style='font-family:courrier;color:darkOrange'>/bin/bash</cite> utilisée est 
<img src='images/linux/bash-version.png' witdh="80%">

La configuration par défaut de est 
<img src='images/linux/bash-shopt-default.png' witdh="80%">


# Configuration préférentielle proposée

<table>
<tr><th>objet</th><th><cite style='font-family:courrier;color:lime'>option shopt</cite></th><th>objet</th><th>préconisation</th><th>raisons</th></tr>
<tr><td>autocd</td><td>usage en shell interactif</td><td>off</td><td>je veux que le changement de répertoire requiere explicitement l'usage de la commande <cite class='exec'>cd</cite></td></tr>
<tr><td>cdable_vars</td><td>usage en shell interactif</td><td>off</td><td>je veux que le changement de répertoire en usage de variable SHELL expose explicitement l'usage de la variable par la syntaxe <cite class='kw'>$</cite></td></tr>
</table>

