Parfait ! Je vais te donner **la version corrigée complète de ton Dockerfile** avec un script `start.sh` intégré. Cette version est robuste, Docker-friendly, et prête à builder.

---

### **1️⃣ Créer le script `start.sh`**

Dans le même dossier que ton Dockerfile, crée un fichier `start.sh` :

```bash
#!/bin/bash
# start.sh - démarrage LAMP

# Démarrer MariaDB
service mariadb start

# Attendre que MariaDB initialise
sleep 5

# Importer la base de données si elle n'a pas encore été importée
if [ ! -f /var/lib/mysql/.db_initialized ]; then
    mysql < /articles.sql
    touch /var/lib/mysql/.db_initialized
fi

# Démarrer Apache en premier plan pour garder le container actif
apache2ctl -D FOREGROUND
```

Puis rends-le exécutable :

```bash
chmod +x start.sh
```

---

### **2️⃣ Dockerfile corrigé**

```dockerfile
# --------------- DÉBUT COUCHE OS -------------------
FROM ubuntu:latest
# --------------- FIN COUCHE OS ---------------------

# MÉTADONNÉES DE L'IMAGE
LABEL version="1.0" maintainer="CHAANBI Talel <talel.chaanbi@etudiant-isi.utm.tn>"

# VARIABLES TEMPORAIRES
ARG APT_FLAGS="-q -y"
ARG DOCUMENTROOT="/var/www/html"

# --------------- DÉBUT COUCHE APACHE ---------------
RUN apt-get update -y && DEBIAN_FRONTEND=noninteractive apt-get install ${APT_FLAGS} apache2
# --------------- FIN COUCHE APACHE -----------------

# --------------- DÉBUT COUCHE MYSQL ----------------
RUN apt-get install ${APT_FLAGS} mariadb-server
COPY sources/db/articles.sql /
# --------------- FIN COUCHE MYSQL ------------------

# --------------- DÉBUT COUCHE PHP ------------------
RUN DEBIAN_FRONTEND=noninteractive apt-get install ${APT_FLAGS} \
    php-mysql \
    php && \
    rm -f ${DOCUMENTROOT}/index.html && \
    apt-get autoclean -y

COPY sources/app ${DOCUMENTROOT}
# --------------- FIN COUCHE PHP --------------------

# OUVERTURE DU PORT HTTP
EXPOSE 80

# RÉPERTOIRE DE TRAVAIL
WORKDIR ${DOCUMENTROOT}

# COPIER LE SCRIPT DE DÉMARRAGE
COPY start.sh /start.sh
RUN chmod +x /start.sh

# DÉMARRAGE DES SERVICES LORS DE L'EXÉCUTION DE L'IMAGE
ENTRYPOINT ["/start.sh"]
```

---

### **3️⃣ Construire et lancer le container**

```bash
# Construire l'image
docker build -t my_lamp .

# Lancer le container
docker run -p 80:80 my_lamp
```

---

### ✅ Avantages de cette version

1. MariaDB démarre avant l’import SQL → pas d’erreur de connexion.
2. L’import SQL ne se répète pas à chaque restart.
3. Apache tourne en premier plan → Docker garde le container actif.
4. ENTRYPOINT en JSON array → Docker gère les signaux correctement (CTRL+C, docker stop).
5. Ton Dockerfile reste clair et maintenable.

---

Si tu veux, je peux te montrer **une astuce pour que MariaDB et Apache démarrent encore plus proprement**, sans `sleep 5`, pour un container quasi “production-ready”.

Veux‑tu que je fasse ça ?
