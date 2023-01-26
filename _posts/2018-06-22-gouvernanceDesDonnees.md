---
layout: post
title: Architecture d'Entreprise - gouvernance des données
category: enterprise
summary: Principales problématiques, solutions pertinentes et erreurs qu'il vaut mieux éviter.
image: images/data-gov.jpg
# comments: true
permalink: ew-ae-data-gov-1
---

Les entreprises font face à de nombreux challenges en matière de gouvernance des données. Petit tour d'horizon des principales problématiques, des solutions pertinentes et des erreurs à ne pas commettre. 

## Les principaux challenges de la gouvernance des données

La gouvernance des données est l'ensemble des processus et des pratiques de gestion des données de l'entreprise <cite class='comment'>et non pas des données d'entreprise</cite>. En conséquence, toutes les données manipulées par l'entreprise entrent dans le périmètre de la gouvernance des données
- que leur usage soit généralisé ou restreint, 
- que les données soient confidentielles ou non, 
- que les données soient stratégiques, tactiques ou opérationnelles, 
- qu'elles soient internes ou externes <cite class='comment'>réseaux sociaux, partenaires, ...</cite>,
- qu'elles soient gratuites ou payantes,
- qu'elles soient réelles ou générées.  

### Challenge n°1 - unifier les données

Être doté de <cite class='kw'>référentiels</cite> uniques, gérant des <cite class='kw'>objets métier</cite>. uniques, disponibles partout dans l'entreprise, reste une vision idéale, encore inaccessible pour de nombreuses entreprises. La plupart des systèmes d'informations sont issus d'une juxtaposition de plusieurs systèmes d'informations qui collaborent à des périmètres et profondeurs variables dans le temps. La gestion historique des données en silo, demeure une réalité pour de nombreuses entreprises. 

#### challenge n°1.1 - établir le modèle d'information métier de l'entreprise

Au bout de 25 ans de carrière, et plusieurs centaines de missions de conseil, je n'ai pas rencontré une seule entreprise qui connaisse et maîtrise sont propre modèle d'information métier. A ceci plusieurs raisons,
- une absence de modèle d'information métier global. La logique suivie est généralement empirique, basée sur une réalité opérationnelle, et le modèle actuel d'information de l'entreprise, est issu de son histoire, de sa culture, et de ses préférences,
- une dichotomie forte, trop prononcée, entre vision métier, et vision IT, aboutissant à des concepts similaires mais différents, souvent sous le même vocable. Cette difficulté de compréhension sémantique est aggravée par des périmètres incompatibles et irréconciliables,
- les logiques de développement des projets métiers et informatiques en mode incrémental, qui confinent à de nombreuses duplications de données, sous l'égide de la sacro-sainte règle de non impact collatéral d'un projet sur l'autre. A trop vouloir découpler, les projets sont autonomes et non collaboratifs, notamment en matière de données, 
- une protection abusive des savoirs et savoirs-faire internes, qui conduisent à un faible partage, voire à de la rétention d'information. Se protéger est louable, entraver l'évolutivité de ses applicatifs, de ses systèmes d'informations, et allonger la durée de ses projets de transformation est à la fois malvenu et dispendieux :alien:. Notez bien que cette protection est encore accentuée naturellement, par la logique foncièrement humaine des internes à l'entreprise, visant à protéger leur poste par la détention et la conservation de savoirs internes spécifiques. L'évolutivité systémique est alors compromise,
- une incapacité chronique à gérer distinctement un <cite class='kw'>modèle conceptuel</cite>, un <cite class='kw'>modèle logique</cite> et un <cite class='kw'>modèle physique</cite> de données. L'historique <cite class='kw'>SQL</cite> est ici lourd et générateur de mauvaises habitudes, fortement ancrées. Les conséquences néfastes sont,
    - l'incapacité à distinguer les évolutions selon leur nature: métier, réglementaire, technique, ou technologique, 
    - des difficultés notables à changer d'instance et d'infrastructure: une base originellement SQL, qui aurait du être une base graphe, ne deviendra probablement pas une base graphe
    - une gestion ardue de la performance applicative nominale et globale, des statistiques d'usage des applicatifs et des données manipulées, 
    - l'identification hasardeuse des sources de <cite class='comment'>sur</cite>sollicitation

#### challenge n°1.2 rendre évolutifs les objets métier

Les <cite class='kw'>objets métiers</cite> évoluent dans le temps. Leur périmètre varie. Structurellement, certains attributs disparaissent, d'autres apparaissent. Or l'objet métier se doit d'être permanent. Comment résoudre ce besoin simultané d'évolutivité et de permanence ?  Que faire, lorsque des relations inter objets étaient externes, et deviennent internes, sous un changement de design ou par la législation ?   

Tout changement de structure ou de relation, impacte l'implémentation et nécessite une révision applicative. Ceci est coûteux, chronophage, et impactant. Les conséquences sur les flux, en terme de contenu, de nombre, et de versionnement s'avèrent généralement invisibles et in-étudiées jusqu'à l'apparition de dysfonctionnements non fonctionnels <cite class='comment'>failles, contre performance, engorgement, limites capacitaires, ...</cite>. 


### Challenge n°2 - s'organiser efficacement 

Actuellement, sous l'impact du règlement européen <cite class='kw'>RGPD</cite>, les entreprises s'organisent et se dotent d'un <cite class='kw'>data protection officer</cite><cite class='comment'>DPO</cite>. Sera-ce suffisant pour traiter la problématique de la gouvernance de données. Je prends le pari de l'insuffisance chronique de cette approche.  

S'organiser efficacement, requiert de traiter les éléments suivants dans une logique manageable
#### Limiter le nombre d'intervenants 
Le <cite class='kw'>DPO</cite> ne peut à lui seul tout traiter. Cependant, la logique actuellement soutenue par la plupart des éditeurs de solutions de <cite class='kw'>data governance</cite>, est une logique de généralisation et de démocratisation, qui leur permet d'accroitre leurs ventes, mais ne permet pas d'avancée significative dans la résolution des problématiques de gouvernance de données.  N'ai encore jamais vécu une seule situation, où la démocratisation d'un problème permettait une résolution plus rapide que par un spécialiste. Si tel était le cas, alors nous n'aurions plus besoin de médecin, auquel se substituerai une assemblée dont les résultats et la performance médicale serait bien entendue supérieure au-dit médecin. Ne vous laissez pas prendre à cette logique, nous avons besoins de médecins pour traiter des maladies, vous avez besoin de spécialistes de l'information pour traiter de la gouvernance de la données. 

Démultiplier les intervenants, conduit à une grande cacophonie, à être submergé d'une foultitude de conseils, tous individuellement pertinents, mais qui ne constituent pas une stratégie de gestion de l'information pour votre entreprise. Défiez vous des acteurs
nominés pour des raisons politiques, qui n'ont pas le minimum minimorum du cortège de compétences nécessaires et indispensables pour tenter de résoudre les problématiques de data gouvernance. 

#### Doter les intervenants de véritables pouvoirs dans l'entreprise
Si les personnes en charge de la gouvernance de données dans votre entreprise, ne sont pas munies des pouvoirs suivants, comment pouvez-vous escompter des résultats probants ? 

1. pouvoir de changer à tout moment, les modèles conceptuels, logique et physique des données, sans avoir à en référer à qui que ce soit
2. pouvoir de poser un véto sur une demande d'évolution, ou sur la perduration de mauvaises pratiques
3. pouvoir d'auditer à tout moment un projet, une application, un système d'information, une pratique métier, pour en vérifier les usages de données et recommander des évolutions impératives, conseillées, ou optionnelles.

Posséder ces pouvoirs garantit une capacité d'action réelle. Cela ne garantit pas les résultats, ni la mise en action, ni les abus qui pourraient en découler. 


#### Être concret dans les gains de transformation
La situation de départ en matière de gouvernance de donnée, est constituée essentiellement de dettes, et parfois de quelques crédits. Les dettes principales sont 

##### Une dette métier très conséquente, source de nombreuses souffrances
Très importante, généralement sous estimée voir sciemment ignorée. Le glossaire métier est inexistant pour la plupart des entreprises. J'évoque ici un véritable glossaire, avec définition des termes, incluant leur périmètre, leur exploitabilité et leur applicabilité. Je ne connais pas une seule entreprise qui soit capable de répondre à des questions classiques d'usage de ces référentiels, tels que le coût nominal d'usage d'une donnée, le coût marginal d'ajout d'un applicatif sur un référentiel, l'impact capacitaire d'une nouvelle application sur le système d'information auquel elle appartient.

##### Une dette architecturale qui se creuse
Les solutions <cite class='kw'>SQL</cite> ont été et demeurent viables. Le problème rencontré est plutôt celui de l'usage déviant du <cite class='kw'>SQL</cite>, utilisé pour tous les usages de données, même lorsque ceci fait peu de sens. Le nombre de types de base de données est en croissance, et savoir quel type utiliser pour quel usage est fondamental. Toute erreur engendre un système d'information difforme et donc des surcoûts de gestion opérationnel, des incapacités fonctionnelles, et des délais d'évolutions allongés. Vos équipes doivent apprendre à utiliser les bases SQL, NO-SQL, graphe et autres selon des critères objectifs de sélection qui contribuent à l'agilité de l'entreprise. Ne pas être doté des savoirs et savoirs-faire n'est pas un frein. Décider en fonction de ces 2 critères est une erreur profonde, qui conduit à des choix erronés, qui devront malheureusement perdurer. 


##### Une dette technique abyssale
La dette technique porte sur la définition, la structure, les attributs, le nommage, la valorisation, l'intégrité, les relations des différents objets métiers de l'entreprise. Elle est conséquente en raison des nombreuses duplications de données, et de l'absence de gestion de son origine <cite class='comment'><cite class='kw'>data lineage</cite></cite>. 


Adopter l'approche d'un assainissement par l'architecture, puis ensuite simultanément, par le métier et par la technique constitue un logique de progrès pour la grande majorité des entreprises. 

Nous verrons dans un prochain post, les solutions envisageables.



