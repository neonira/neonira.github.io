---
layout: post
title: XML - Faites du X!
category: linuxverse
summary: Tirez profit du X de XML ... 
image: images/linux/xml.png
# comments: true
permalink: lv-xml-1
---

Comprenons nous bien, je ne suis promotteur des activités pornographiques. Je veux parler du <cite class="kw">X</cite> de <cite class="kw">XML</cite>!
Au delà du méta langage, comment utilisez vous la caractéristique d'extensibilité
dans vos fichiers <cite class="kw">XML</cite>? Autrement dit, que faites vous du <cite class="kw">X</cite>? 

L'inutilisation de cette caractéristique conduit à des fichiers
<cite class="kw">XML</cite>, équivalent à des <cite class="kw">structures C</cite> ou des <cite class="kw">copies Cobol</cite>. De ce fait,
la valeur du langage <cite class="kw">XML</cite> est négative, car il n'y a pas d'avantage à
utiliser <cite class="kw">XML</cite>, en lieu et place d'autres mécanismes plus directs, plus
simples, et moins onéreux à maintenir. 

La caractéristique d'extensibilité peut être mise en oeuvre de
plusieurs manières 

### Multiplicité des entrées
Si l'utilisation des balises est certes un préalable à la mise en
oeuvre du méta langage, elle demeure insuffisante pour
exploiter réellement le méta langage. Cette exploitation requiert la
mise en oeuvre de schémas (ou type de document), afin de définir un
modèle, qui structure le méta langage et ces instances. Nous nous
plaçons dorénavant dans ce cas. 

La caractéristique d'extensibilité peut être comprise comme la capacité à
accepter un nombre indéterminé d'entrées pour la composition
d'un type. Il s'agit alors de l'utilisation combinée d'une définition
d'un modèle de groupe <cite class='comment'>e.g. <cite
class="kw">sequence</cite>, <cite class="kw">choice</cite>, <cite
class="kw">any</cite></cite>, et de l'indétermination de ses bornes limites <cite
class="kw">minOccurs</cite> et <cite class="kw">maxOccurs</cite>
dans ce modèle de groupe. Bien entendu, cela est stipulé dans le
schéma. Généralement, l'usage du mot clef <cite
class="kw">unbounded</cite> pour la borne <cite
class="kw">maxOccurs</cite> suffit pour gérer cette multiplicité. 


### Polymorphisme des entrées
La caractéristique d'extensibilité peut <cite class='comment'>et doit</cite> être comprise comme la capacité à
accepter un type dérivé en lieu et place d'un type de base. L'usage
conjoint de <cite class="kw">xsd:extension</cite> dans la définition d'un type et de l'attribut <cite
class="kw">subtitutionGroup</cite> dans une élément permet la mise
en oeuvre propre et cohérente de ce polymorphisme. 

Nous aurions pu également utiliser le type générique <cite class="kw">anyType</cite>
mais au détriment du contrôle de type, ce qui est rarement souhaité. 

Notez que l'usage explicite de la définition
d'un modèle de groupe <cite class="kw">choice</cite> permet ce
polymorphisme avec un niveau de contrôle élevé des différents
choix. Cette méthode directe est souvent suffisante. Réservez là pour
les cas de choix réels entre alternatives disjointes mettant en oeuvre
des types hétérogènes sans parties commune. Par exemple, fournir ses
informations bancaires par <cite class="kw">RIB</cite> ou <cite
class="kw">IBAN</cite> entre bien dans cette catégorie car chacune de
ces entrées est supportée par une norme spécifique, disjointe de sa
concurrente.

Une autre moyen d'arriver à du polymorphisme de type est de
jongler avec les espaces de noms. Supposez que vous deviez documenter
un élément du genre <cite class="kw">&lt;xsd:element
name="bankAccountInfo" type="bai:bankAccountInfo"&gt;</cite>, qui
exige l'import de l'espace de nom <cite class="kw">bai</cite>. Si
vous différez cet import, jusqu'à la création d'un fichier instance,
alors vous avez la possibilité de fixer l'import qui vous convient. On
peut ainsi avoir un fichier d'import pour le développement, un autre
pour l'intégration et encore un autre pour la production. L'avantage
est que chaque fichier sera optimisé pour son domaine. L'inconvénient
est que l'aspect ultra dynamique risque d'engendrer de nombreux
problèmes à moins d'avoir du personnel, bon connaisseur de la logique
<cite class="kw">XML</cite>?.

Au début, faire du X semble compliqué. Essayez et les atouts de
cette approche vous séduiront. Au fait, combien de fichier <cite class="kw">XML</cite> avez vous créé, qui mettent en oeuvre le <cite class="kw">X</cite> d'<cite class="kw">XML</cite>?
