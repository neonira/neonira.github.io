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

<img src='images/linux/bash-shopt-default.png' width="90%">


# Configuration préférentielle proposée

## Options qu'il est conseillé d'activer

Les options à activer sont positionnées par la commande <cite class='exec'>shopt -s option-name</cite>.

<table>
<tr><th><cite style='font-family:courrier;color:lime'>option shopt</cite></th><th>objet</th><th>raisons</th></tr>
<tr><td><cite class='oc'>cdspell</cite></td><td>correction frappe en mode interactif</td><td>corrige automatiquement les erreurs de frappe sur la command <cite class='exec'>cd</cite></td></tr>
<tr><td><cite class='oc'>dirspell</cite></td><td>correction frappe en mode interactif</td><td>corrige automatiquement les petites erreurs de frappes sur les noms de répertoires</td></tr>
<tr><td><cite class='oc'>checkjobs</cite></td><td>gestion des jobs</td><td>informe moi des jobs et de leur status avant de terminer le shell</td></tr>
<tr><td><cite class='oc'>checkwinsize</cite></td><td>gestion du fenêtrage</td><td>retaille automatiquement les fenêtres</td></tr>
<tr><td><cite class='oc'>cmdhist</cite></td><td>gestion de l'historique</td><td>sauve les entrées multiligne en une seule entrée dans l'historique des commandes</td></tr>
<tr><td><cite class='oc'>hostcomplete</cite></td><td>gestion de la complétion sur les noms de hosts</td><td>active la complétion des hostnames</td></tr>
<tr><td><cite class='oc'>interactive_comments</cite></td><td>gestion des commentaires en shell interactif</td><td>active la possibilité de gérer des commentaires interactivement. Très utile pour créer des procédures et avoir des suggestions</td></tr>
<tr><td><cite class='oc'>prompt_vars</cite></td><td>gestion des variables dans le prompt</td><td>je préfère que le shell expande les variables et les calculs dans le prompt</td></tr>
<tr><td><cite class='oc'>shift_verbose</cite></td><td>gestion des erreurs sur le nomrbe d'arguments</td><td>informe moi des erreurs si j'excède le nombre réel d'arguments</td></tr>
<tr><td><cite class='oc'>source_path</cite></td><td>recherche fichier à sourcer</td><td>recherche le fichier à sourcer dans la variable <cite class='op'>PATH</cite></td></tr>
</table>



## Options laissées à votre libre arbitre

Votre choix d'activation ou de désactivation est libre. Comprenez cependant les implications de vos choix. 

<table>
<tr><th><cite style='font-family:courrier;color:lime'>option shopt</cite></th><th>objet</th><th>raisons</th></tr>
<tr><td><cite class='oc'>checkhash</cite></td><td>hash table de recherche des commandes</td><td>peut augmenter la performance de votre shell</td></tr>
<tr><td><cite class='oc'>lithist</cite></td><td>gestion de l'historique</td><td>choix du terminateur de commande, newline ou point virgule, pour les commandes multi-lignes dans l'historique</td></tr>
<tr><td><cite class='oc'>mailwarn</cite></td><td>gestion du courriel</td><td>information sur arrivée de courriel</td></tr>
<tr><td><cite class='oc'>no_empty_cmd_completion</cite></td><td>gestion des erreurs</td><td>autoriser ou non la complétion vide?</td></tr>
<tr><td><cite class='oc'>progcomp</cite></td><td>usage des facilités de programmation</td><td>à vous de choisir la manière dont le shell interprète vos commandes</td></tr>
<tr><td><cite class='oc'>nullglob</cite></td><td>extension des patterns de recherche de fichiers</td><td>à vous de choisir, la gestion de chaîne nulle ou égale à un pattern</td></tr>
<tr><td><cite class='oc'>lastpipe</cite></td><td>extension des pipes</td><td>préférablement off cependant</td></tr>
</table>


## Options qu'il est conseillé de désactiver

Les options à déactiver sont positionnées par la commande <cite class='exec'>shopt -u option-name</cite>.

<table>
<tr><th><cite style='font-family:courrier;color:lime'>option shopt</cite></th><th>objet</th><th>raisons</th></tr>
<tr><td><cite class='oc'>autocd</cite></td><td>gestion changement de répertoire</td><td>le changement de répertoire requière explicitement l'usage de la commande <cite class='exec'>cd</cite></td></tr>
<tr><td><cite class='oc'>cdable_vars</cite></td><td>gestion changement de répertoire</td><td>le changement de répertoire en usage de variable SHELL expose explicitement l'usage de la variable par la syntaxe <cite class='op'>$</cite></td></tr>
<tr><td><cite class='oc'>compat*</cite></td><td>gestion des modes de compatibilités inter version <cite style='font-family:courrier;color:darkOrange'>/bin/bash</cite></td><td>je préfère le comportement standard du shell dans sa version</td></tr>
<tr><td><cite class='oc'>nocaseglob</cite></td><td>gestion de la casse dans le matching </td><td>conserver le matching ne confondant pas majuscules et minuscules</td></tr>
<tr><td><cite class='oc'>nocasematch</cite></td><td>gestion de la casse dans le matching </td><td>conserver le matching ne confondant pas majuscules et minuscules</td></tr>
</table>
