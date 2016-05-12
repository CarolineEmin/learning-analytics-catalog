# Echantillonnage au sein d’une séquence pédagogique

## Description courte du scénario d'analyse

Il est fréquent que les utilisateurs d’un dispositif ne suivent pas de manière linéaire la séquence pédagogique prescrite et « sautent » une activité prescrite, quelle qu’elle soit. Exemple d’activités prescrites : visionnage d’une vidéo, rendu d’un devoir, réalisation d’un quiz, etc. On dira d’une activité prescrite qu’elle a été ignorée ou évitée si elle n’a pas été réalisée alors même qu’elle était prescrite. Exemples : sur une séquence de 10 vidéos à visionner, l’utilisateur ne visionne pas les vidéos 1, 2, et 5. L’objet de ce package est de visualiser l’échantillonnage du point de vue du dispositif et du point de vue des utilisateurs. 

### Tags

Echantillonnage, évitement

## Cas d’utilisation

### Orientés concepteurs

#### Identification des ressources peu utilisées, en réingénierie

Afin d’alléger un dispositif de formation, un concepteur souhaite supprimer d’une itération sur l’autre les ressources qui ne sont pas utilisées par la plupart des utilisateurs. Il lui faut identifier les ressources les moins utilisées. On cherche à établir un score pour chaque ressource.


#### Identification des utilisateurs peu assidus

On cherche à identifier pour une formation donnée les participants qui ont obtenu le certificat de la formation sans pour autant avoir visionné les ressources prescrites. Plusieurs applications possibles : pénaliser les participants qui laissent de côté trop de ressources prescrites, les relancer de manière personnalisée pour leur préciser quelles ressources qu'ils doivent revoir. 

### Orientés chercheurs

#### Typologie des comportements d’échantillonnage

Création d’une typologie des utilisateurs sur la base de leur comportement d’échantillonnage : nature et nombre de ressources sautées. On peut orienter l’analyse sur la catégorisation des utilisateurs, on pourra s’intéressera à la distinction entre différents cas : celui où l’utilisateur réalise la quasi-totalité des activités prescrites et n’ignore que quelques-unes d’entre elles ; celui où l’utilisateur ne réalise qu’une minorité des activités prescrites. On pourra identifier le premier pattern comme « skipping », et le second comme « cherry-picking ». On pourra définir les utilisateurs comme skippers ou cherry-pickers sur la base de ces patterns. On peut chercher à identifier selon une typologie d’utilisateurs identifiée (skipper, cherry-picker par exemple) les scores d’échantillonnage de telle ou telle ressource.


## Inputs
### Flat

### logdata
Données de logs, où l’on a défini la fenêtre temporelle d’intérêt

id | user_id | ressource_id| viewed_date | ...
---|-------- | -----------|-------- | ---
identifiant unique de la trace (int | identifiant unique d'un utilisateur |identifiant unique d'une ressource |  timestamp
1 | 123456 | vidéo S1.1|'2016-01-01' 
2 | 123456 | vidéo S1.2|'2016-01-01' 
3 | 123456 | vidéo S1.4|'2016-01-01'
3 | 489456 | vidéo S1.1|'2016-01-01'

### Séquence pédagogique

L’analyste a besoin pour réaliser ce travail de connaître de manière précise la séquence pédagogique prescrite. Un travail de nettoyage de la séquence peut avoir été réalisé en amont par l’analyste pour filtrer des éléments qui ne doivent pas être pris en compte dans la séquence prescrite. Par exemple, on peut retirer dans une séquence de vidéos une vidéo n’ayant pas une visée pédagogique (vidéo d’animation: présentation d’un module, etc) pour ne conserver que les vidéos pédagogiques à proprement parler car l’on sait que la plupart des utilisateurs sautent la vidéo d’animation, ce qui risque de biaiser la détection des “skippers” proprement dits.

prescribed_sequence_of_interest

Séquence pédagogique sur laquelle doit être réalisée l’analyse. Contient l’identifiant et l’ordre des ressources. 

order | ressource_id| 
---|-------- |
Ordre dans la séquence | identifiant unique d'une ressource
1 | vidéo S1.1 |
2 | vidéo S1.2 |


### xApi
* event name 1
* event name 2
* event name 3
* ...

## Outputs
### user_video_mat
Matrice binaire 1/0. Tableau avec en ligne les utilisateurs, en colonne les ressources de la sequence_of_interest, prenant la valeur 1 quand une activité a été évitée par un utilisateur

user_id | ressource 1| ressource 2 | ...
------- | -----------|-------- | ---
123456 | 0|0 
123457 | 1|0



### activity_skipping_score
Identification des activités les plus fréquemment évitées par les utilisateurs, avec un rang et un score pour chaque ressource. Exemple : proportion des certifiés ayant évité la ressource.

ressource_id | score d'échantillonnage| 
---|-------- |
vidéo S1.1 | 0.58
vidéo S1.2 |0.41

### user_skipping_score
Calculer un score pour chaque utilisateur en fonction de sa propension à sauter une ressource

user_id | score d'échantillonnage| 
---|-------- |
123456 | 0.05
123457 |0.51


## Indicateurs recommandés
Indicateur 1 : Proportion des utilisateurs évitant plus de 10% des ressources prescrites
Indicateur 2 : Proportion des utilisateurs évitant plus de 80% des ressources prescrites

# Exemples

### Données factices
[Données factices] https://github.com/hubble-learning-analytics/learning-analytics-catalog/blob/master/echantillonnage-au-sein-d-une-sequence-pedagogique/example/Factice-data

### Données cas d'étude Hubble

Le MOOC Effectuation est constitué de cinq modules diffusés au rythme de un module par semaine, chaque module comprenant une demi-douzaine de vidéos et approximativement autant de quiz notés. Une étude de cas est proposée aux participants pour chacune des trois itérations ; l’obtention du certificat est inféodée au rendu d’un devoir portant sur cette étude de cas, devoir évalué par les pairs. 

[Données cas d'étude Hubble : le MOOC Effectuation] https://github.com/hubble-learning-analytics/learning-analytics-catalog/blob/master/echantillonnage-au-sein-d-une-sequence-pedagogique/example/logs.MOOC.Effectuation.Hubble.csv
[Algorithme R permettant de réaliser l'analyse de l'échantillonnage sur un cas d'étude de Hubble] https://github.com/hubble-learning-analytics/learning-analytics-catalog/blob/master/echantillonnage-au-sein-d-une-sequence-pedagogique/algorithms/R/EchantillonnageAuSeinDUneSequencePedagogique.r

## Bibliographie

Breslow, L., Pritchard, D., DeBoer, J., Stump, G., Ho, A., & Seaton, D. (2013). Studying learning in the worldwide classroom: Research into edX’s first MOOC. Journal of Research & Practice in Assessment, 8, 13–25.

## Légitimation de l'analyse

Citation d'un apprenant : "Ça m’arrive de sauter [des ressources] ; ça dépend du MOOC en fait. Il peut y avoir quelque chose qui ne m’intéresse pas mais si je sens que c’est là pour une bonne raison et que ça m’apportera quelque chose je le suis. Si je sens que je peux m’en passer, je zappe, ça arrive assez régulièrement. Ça dépend un peu de l’objectif de ce MOOC. Si c’est pour me former dans le domaine technique sur un point bien particulier, je vais m’accrocher et je vais essayer de bien creuser le truc. Si c’est juste pour apprendre de nouvelles choses, piocher des idées ou des connaissances, à droite, à gauche, c’est un peu le buffet où je me sers. Je ne suis pas obligé de suivre ce qui est proposé exactement. C’est ce que je trouve très sympa aussi, on peut faire un peu à sa sauce."
