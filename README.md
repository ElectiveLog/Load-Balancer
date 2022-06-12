# Load-Balancer

Dans un premier temps il faut créer et lancer les dockers de notre backend si ce n'est pas encore fait :

Il faut se positionner à la racine du backend 

docker build -t load-balanced-app .

docker run -e "MESSAGE=First instance" -p 3001:3000 -d load-balanced-app
docker run -e "MESSAGE=Second instance" -p 3002:3000 -d load-balanced-app

Puis faire la même chose avec notre load balancer :

docker build -t load-balance-nginx .
docker run -p 8080:80 -d load-balance-nginx

Le backend est ensuite accessible à partir de http://localhost:8080/