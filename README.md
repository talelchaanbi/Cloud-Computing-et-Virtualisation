# Cloud Computing et Virtualisation

Ce dépôt rassemble deux supports pédagogiques sur Docker, pensés pour un usage éducatif et partagé avec d’autres étudiants.

## Contenu

| Support | Sujet | Fichier principal |
|---|---|---|
| 1 | Initiation à Docker | [TP1_Docker.md](TP1%3A%20Initiation%20%C3%A0%20Docker/TP1_Docker.md) |
| 2 | Conteneurisation d’une application Web | [TP2_Docker.md](TP2%3A%20Conteneurisation%20d%E2%80%99une%20application%20Web/TP2_Docker.md) |

## Organisation du dépôt

```text
.
├── README.md
├── TP1: Initiation à Docker/
│   ├── TP1_Docker.md
│   └── images/
└── TP2: Conteneurisation d’une application Web/
    ├── Dockerfile
    ├── start.sh
    ├── TP2_Docker.md
    ├── images/
    └── sources/
        ├── app/
        └── db/
```

## Objectif pédagogique

- Montrer les bases de Docker: images, conteneurs et commandes essentielles.
- Illustrer la conteneurisation d’une application Web avec Apache, PHP et MariaDB.
- Présenter la persistance des données avec les volumes Docker.
- Servir de support clair, simple et réutilisable pour d’autres étudiants.

## Comment naviguer

- Commencer par [TP1_Docker.md](TP1%3A%20Initiation%20%C3%A0%20Docker/TP1_Docker.md) pour les bases de Docker.
- Lire ensuite [TP2_Docker.md](TP2%3A%20Conteneurisation%20d%E2%80%99une%20application%20Web/TP2_Docker.md) pour l’exemple complet de stack LAMP.
- Dans le dossier TP2, le fichier [Dockerfile](TP2%3A%20Conteneurisation%20d%E2%80%99une%20application%20Web/Dockerfile) décrit la construction de l’image.

## Pour une publication GitHub/LinkedIn

- Garder ce README comme page d’accueil du dépôt.
- Utiliser des messages courts et pédagogiques dans la description du dépôt.
- Mettre en avant les compétences démontrées: Docker, conteneurisation, volumes, réseau et stack LAMP.

## Auteur

- **Réalisé par :** Talel Chaanbi