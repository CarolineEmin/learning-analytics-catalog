# Echantillonnage au sein d’une séquence pédagogique

## Cas d’utilisation

### Orientés concepteurs

#### Identification des ressources peu utilisées, en réingénierie

Afin d’alléger un dispositif de formation, un concepteur souhaite supprimer d’une itération sur l’autre les ressources qui ne sont pas utilisées par la plupart des utilisateurs. Il lui faut identifier les ressources les moins utilisées. On cherche à établir un score pour chaque ressource.


#### Identification des utilisateurs peu assidus

On cherche à identifier pour une formation donnée les participants qui ont validé les acquis sans pour autant avoir visionné les ressources exigées. Plusieurs applications possibles : pénaliser les participants qui sautent trop de ressources, les relancer de manière personnalisée pour leur préciser quelles ressources ils doivent revoir. 

### Orientés chercheurs

#### Typologie des comportements d’échantillonnage

Création d’une typologie des utilisateurs sur la base de leur comportement d’échantillonnage : nature et nombre de ressources sautées. On peut orienter l’analyse sur la catégorisation des utilisateurs, on pourra s’intéressera à la distinction entre différents cas : celui où l’utilisateur réalise la quasi-totalité des activités prescrites et n’ignore que quelques-unes d’entre elles ; celui où l’utilisateur ne réalise qu’une minorité des activités prescrites. On pourra identifier le premier pattern comme « skipping », et le second comme « cherry-picking ». On pourra définir les utilisateurs comme skippers ou cherry-pickers sur la base de ces patterns. On peut chercher à identifier selon une typologie d’utilisateurs identifiée (skipper, cherry-picker par exemple) les scores d’échantillonnage de telle ou telle ressource.


## Inputs
### Flat

logdata
Données de logs, où l’on a défini la fenêtre temporelle d’intérêt

id | user_id | ressource_id| viewed_date | ...
---|-------- | -----------|-------- | ---
identifiant unique de la trace (int | identifiant unique d'un utilisateur |identifiant unique d'une ressource |  timestamp
1 | 123456 | vidéo S1.1|'2016-01-01' 
2 | 123456 | vidéo S1.2|'2016-01-01' 
3 | 123456 | vidéo S1.4|'2016-01-01'
3 | 489456 | vidéo S1.1|'2016-01-01'

# Séquence pédagogique

L’analyste a besoin pour réaliser ce travail de connaître de manière précise la séquence pédagogique prescrite. Un travail de nettoyage de la séquence peut avoir été réalisé en amont par l’analyste pour filtrer des éléments qui ne doivent pas être pris en compte dans la séquence prescrite. Par exemple, on peut retirer dans une séquence de vidéos une vidéo n’ayant pas une visée pédagogique (vidéo d’animation: présentation d’un module, etc) pour ne conserver que les vidéos pédagogiques à proprement parler car l’on sait que la plupart des utilisateurs sautent la vidéo d’animation, ce qui risque de biaiser la détection des “skippers” proprement dits.

prescribed_sequence_of_interest

Séquence pédagogique sur laquelle doit être réalisée l’analyse. Contient l’identifiant et l’ordre des ressources. 

order | ressource_id| 
---|-------- |
identifiant unique de la trace (int | identifiant unique d'une ressource (int)
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

### activity_skipping_score
Identification des activités les plus fréquemment évitées par les utilisateurs, avec un rang et un score pour chaque ressource.

### user_skipping_score
Calculer un score pour chaque utilisateur en fonction de sa propension à sauter une ressource

## Indicateurs recommandés
### Proportion des utilisateurs évitant plus de 90% des ressources prescrites

### Proportion des actions attendues (on attend d’un utilisateur qu’il réalise l’ensemble des activités de la séquence) ayant été effectivement réalisées

## Exemples
Analyse de données factices



## Publications

Breslow, L., Pritchard, D., DeBoer, J., Stump, G., Ho, A., & Seaton, D. (2013). Studying learning in the worldwide classroom: Research into edX’s first MOOC. Journal of Research & Practice in Assessment, 8, 13–25.
