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
