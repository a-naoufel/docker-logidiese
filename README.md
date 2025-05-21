# Projet Logidiese avec Docker

Ce document explique comment configurer, exécuter, mettre à jour et maintenir l'application `logidiese` avec Docker sur une machine Ubuntu. L'application utilise un serveur web Apache/PHP et une base de données MySQL, orchestrés via Docker Compose.

## Table des matières
- [Structure du projet](#structure-du-projet)
- [Prérequis](#prérequis)
- [Configuration](#configuration)
- [Démarrer l'application](#démarrer-lapplication)
- [Mettre à jour la base de données](#mettre-à-jour-la-base-de-données)
- [Connexion à la base de données](#connexion-à-la-base-de-données)
- [Démarrage automatique](#démarrage-automatique)
- [Résolution des problèmes](#résolution-des-problèmes)
- [Commandes utiles](#commandes-utiles)

## Structure du projet

Le répertoire `~/tempdiese` contient :
- `docker-compose.yml` : Définit les services `web` (Apache/PHP) et `mysql` (base de données).
- `apache-php/` :
  - `Dockerfile` : Construit l'image pour le service web.
  - `logidiese.conf` : Configuration Apache.
  - `logidiese/` : Application avec `index.php`, `config/`, etc.
- `db_dump.sql` : Script SQL pour initialiser la base de données.

## Prérequis

- **Docker** ≥ 28.1.1  
  Vérifiez avec :
  ```bash
  docker --version

## Démarrer l'application

cd ~/tempdiese
docker compose up -d
docker compose ps

## Mettre à jour la base de données
- **Nouveau fichier db_dump.sql** 
cp ~/tempdiese/db_dump.sql ~/tempdiese/db_dump.sql.bak
mv /chemin/vers/nouveau_db_dump.sql ~/tempdiese/db_dump.sql
chmod 644 ~/tempdiese/db_dump.sql

docker compose down
docker volume rm tempdiese_mysql-data
docker compose up -d

docker compose exec mysql mysql -u root -prootpass logidiese -e "SHOW TABLES;"
- **Appliquer des mises à jour SQL**
docker compose exec mysql mysql -u root -prootpass logidiese

cp /chemin/vers/update.sql ~/tempdiese/update.sql
docker compose cp ~/tempdiese/update.sql mysql:/tmp/update.sql
docker compose exec mysql mysql -u root -prootpass logidiese < /tmp/update.sql

## Démarrage automatique
sudo systemctl enable docker
sudo systemctl enable docker.socket

sudo reboot
cd ~/tempdiese
docker compose ps
