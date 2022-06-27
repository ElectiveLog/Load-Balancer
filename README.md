# Load-Balancer et routes

Cette configuration se fait dans le fichier nginx.conf. 

## Première partie du fichier (ligne 1-14)

Nous avons deux blocs de serveur défini avec l'attribut "upstream". Le premier bloc "sqlserver" correspond aux services permettant d'accéder à la base de données SQL. Le deuxième bloc "mongoserver" permet d'accéder aux services de la base de données mongo. 

Le Load-Balancing est réalisé dans ces blocs grâce à la ligne "least_conn". C'est le serveur avec le moins de connexion qui est choisi pour effectuer la requête entrante. 

Deux serveurs sont en fonctionnements pour chaque bloc mais il est possible d'en rajouter si besoin "server <adresse serveur>:<port serveur>"

## Deuxième partie du fichier (ligne 17-58)

Nous avons le serveur nginx, en fonction de la requête qui arrive sur le serveur, nous lui appliquons différents champs dans le header afin de satisfaire les exigences de cors. 

En fonction de la valeur du paramètre "X-Server-Select", nginx redirige la requête vers le bon bloc de serveurs. 

Enfin nous activons différents paramètres pour autoriser les requêtes qui transitent.

# Services

Cette configuration se fait dans le fichier docker-compose.yml.

La configuration permet de lancer tous les dockers en même temps, si nous regardons le fonctionnement d'un service comme par example nginx (ligne 4). 
- "container_name" : nom du conteneur.
- "image" : nom de l'image pour créer le conteneur.
- "ports" : <port de sortie du conteneur>:<port de l'intérieur du docker>


Ces informations sont présentes pour le service nginx et pour les 4 serveurs mongo et sql. 

Les deux derniers dockers correspondent aux bases de données mongo et sql et fonctionnent comme pour les services précédents. 

Pour rajouter un nouveau service, il suffit de créer un nouveau docker avec les bonnes informations. Faire attention à donner un nom unique pour chaque conteneur, vérifier que l'image existe bien et que le port de sortie n'est pas déjà utilisé.

