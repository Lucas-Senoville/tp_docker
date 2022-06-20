# TP DOCKER

## INSTALLATIONS

### Installation de Docker sur Debian

Pour débuter l’installation de docker sur Debian, on commence par une mise à jour :

`sudo apt update && apt full-upgrade -y`

Puis l’installation des dépendances :

`sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release`

Ajout de la clé GPG officielle de Docker :

`curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg`

Ajout du repository Docker dans les sources : 

`echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`

Mise à jour des sources :

`sudo apt update`

Téléchargement de docker depuis les sources :

`sudo apt install docker-ce docker-ce-cli containerd.io`

Vérification de l’installation de Docker :

docker run hello-world

Quelques commandes utiles :

`systemctl start/stop docker          # Démarrer/arrêter docker service
systemctl enable docker               # Activer docker au démarrage de l'os
docker pull                                    # Télécharger une image Docker 
docker ps                                       # Liste tous les Containers actifs
docker ps -a                                  # Liste tous les Containers 
docker start/stop CONTAINER ID # Démarrer/arrêter Container            
docker rm CONTAINER ID            # Supprimer Container par ID
docker kill CONTAINER ID            # Eteindre un Container par ID
docker images                              # Liste toutes les images Docker qui ont étés téléchargés`

## LE TP :

Commencer par cloner le dépôt git où se trouve le code source python :
'git clone https://github.com/Lucas-Senoville/tp_docker.git'

# Création d'un dockerfile 
**Cours**
Un dockerfile est un simple fichier texte, qui ne possède pas de format spécifique lors de sa création, contenant les instructions nécessaires afin de construire (build) une image docker.

Les instructions dans un dockerfile :
- FROM => permet de spécifier l'image que vous allez utiliser, image qui est présente sur **Docker Hub**. Exemple : FROM nginx
- WORKDIR => permet de spécifier le répertoire dans lequel seront basées les instructions qui suivront son appel.
- ADD => permet de copier un fichier ou un dossier venant d’un répertoire interne ou externe vers un chemin de destination contenant le système de fichiers de l’image. Exemple : `ADD test.txt path/`
- RUN => permet d’exécuter des commandes supplémentaires à l’intérieur du build du dockerfile. L’argument qu’elle prend est identique à une commande Shell ordinaire.
- CMD => sert à mentionner les instructions qui seront exécutées en premier au moment du lancement du conteneur créé à partir de l’image obtenue avec le dockerfile. Exemple : `CMD [echo ‘hello world’]`

**Exercice : ** Ecriture dans un dockerfile 
- Utiliser la version 3.8 de python
- Ajouter le fichier main.py
- Installer les packages requests et beautifulsoup4
- Lancer la commande python3 ./main.py

Une fois cela fait, il faut build l'image :
`docker build -t python-imdb`

Lancer l'image :
`docker run python-imdb`

Décommenter de la ligne 38 à 40 afin de lancer un input, puis la lancer la commande run modifiée :
`docker run -t -i python-imdb`
-t => nous donne accès à un terminal avec sudo 
-i => interactive mode 

