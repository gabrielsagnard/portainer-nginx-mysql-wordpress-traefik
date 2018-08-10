# portainer-nginx-mysql-wordpress-traefik

### Conditions préalables:

* Un VPS sous Ubuntu 16.04.
* Un utilisateur non-root, compatible avec sudo. 
* Une installation fonctionnelle de Docker 

### Etape N°1. Installer Docker

Pour installer Docker proprement, utilisez cette commande : 

    $ sudo curl -sS https://get.docker.com/ | sh
    
Cette commande va mettre à jour votre système et installer la dernière version stable de Docker.

Autoriser Docker et le démarrer :

    sudo systemctl enable docker
    sudo systemctl start docker
    
### Etape N°2. Installer Traefik via docker-compose

Tout d'abord, vous devez installer docker-compose si vous ne l'avez pas déjà fait.

    curl -L https://github.com/docker/compose/releases/download/1.16.1/docker-compose-`uname -s`-`uname -m` > ./docker-compose
    sudo mv ./docker-compose /usr/bin/docker-compose
    sudo chmod +x /usr/bin/docker-compose
    
Pour exécuter Traefik en utilisant docker-compose : 

    git clone https://github.com/gabrielsagnard/portainer-nginx-mysql-wordpress-traefik
    
Une fois ceci fait modifier les deux fichiers, traefik.toml et docker-compose.yml en y ajoutant vos informations personnelles.

    sudo nano docker-compose.yml
   
et :

    sudo nano traefik.toml
    
Il faut modifier toutes les lignes où vous trouverez "youremail" ou "yourdomain".

Puis à la racine du projet : 

    touch /root/acme.json
    chmod 600 /root/acme.json
  
Et enfin on lance le tout avec :

    docker network create Traefik
    
Et :

    docker-compose up -d 
  
Résultat vous trouverez portainer à l'adresse https://monitor.yourdomain.com, Nginx à l'adresse https://site.yourdomain.com, Wordpresse à l'adresse https://blog.yourdomain.com et traefik à l'adresse http://site.yourdomain.com:8080



