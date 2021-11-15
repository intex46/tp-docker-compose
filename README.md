# tp-docker-compose
tp docker compose

# UC :
mettre en prod une application "vote" qui permet de faire un sondage entre "chien et chat"

# L'arborescence de votre repertoire :

```bash
.
├── result/             # permet d'afficher le resultat des votes
├── vote/               # l'API 
├── docker-compose-vote.yaml             # docker compose qui permet de lancer votre application
```

# Etapes:
* Créer un dockerfile dans le repertoire vote qui permet de lancer votre API vous devez:

1- partir d'une image python ( slim de preference)

2- ajouter curl:
```bash
apt-get update \
    && apt-get install -y --no-install-recommends \
    curl \
    && rm -rf /var/lib/apt/lists/*
```  

3- se placer dans le repertoire /app

4- copier le fichier requirements.txt dans le repertoire app

5- installer les packages python à l'aide du fichier requirements `pip install -r requirements.txt`

6- copier le repretoire vote dans /app

7- exposer le port 80

8- lancer notre api gunicron : `"gunicorn", "app:app", "-b", "0.0.0.0:80", "--log-file", "-", "--access-logfile", "-", "--workers", "4", "--keep-alive", "0"`

* Créer votre fichier docker-compose-vote, il doit contenir : 

1- un service vote, l'image sera construite à la montée de vos service , il faudra executer le script app.py et mapper le port 5000 de votre machine hote au port 80, votre service dependra de la montée du service redis 

2- un service redis qui part d'une image redis:alpine

3- un service worker qui va build l'image à la montée de votre application, il dependra du service redis egalement

4- un service db, on partira sur une image postgres:9.4, on definira 2 variables d'environnments POSTGRES_USER et POSTGRES_PASSWORD qui prendrons comme valeur "postgres", on definira un volume db_data qui sera mappe sur le repretoire "/var/lib/postgresql/data"

5- tout les services devrons communiquer à travers d'un réseau de typer "bridge" nommé "netproxy", la création du network est prise en compte dans votre fichier docker compose

* Votre application tournera sur  http://localhost:5000, et le résultat sur http://localhost:5001.