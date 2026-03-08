# Docker Compose - Resource Limits

## Justification des limites de ressources par service

| Service | CPU | RAM | Justification |
|---|---|---|---|
| **traefik** | 0.5 | 128M | Reverse proxy léger — se contente de router les requêtes, pas de traitement lourd |
| **postgres** | 1.0 | 512M | Base de données — a besoin de RAM pour le cache des requêtes et les index |
| **redis** | 0.5 | 128M | Cache en mémoire — stocke les données en RAM mais les données sont légères |
| **mailhog** | 0.25 | 64M | Outil de dev — faux serveur SMTP très léger, pas prévu pour la prod |
| **adminer** | 0.25 | 64M | Interface web légère — simple UI PHP sans traitement lourd |
| **backend** | 0.5 | 256M | API Node.js — a besoin de RAM pour le runtime Node et les connexions |
| **frontend** | 0.25 | 64M | Nginx statique — sert uniquement des fichiers statiques, très léger |

## Comprendre les unités

| Unité | Signification |
|---|---|
| `0.25` CPU | 25% d'un cœur CPU |
| `0.5` CPU | 50% d'un cœur CPU |
| `1.0` CPU | 100% d'un cœur CPU |
| `64M` | 64 mégaoctets de RAM |
| `256M` | 256 mégaoctets de RAM |
| `512M` | 512 mégaoctets de RAM |

## Pourquoi limiter les ressources ?

Sans limites, un service peut consommer toute la RAM ou le CPU du serveur
et faire tomber les autres services. Par exemple :

- Une requête SQL mal optimisée peut faire exploser la consommation de PostgreSQL
- Une fuite mémoire dans le backend Node.js peut saturer le serveur
- Avec des limites, Docker garantit que chaque service reste dans son couloir

## Commande pour surveiller la consommation en temps réel
```bash
docker stats
```
