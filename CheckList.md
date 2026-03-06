# DevOps Foundations – Project Checklist

Cette checklist permet de suivre l'avancement des différentes parties du projet.

---

# Partie 2 — Développement & Conteneurisation

## Livrable 2.1 — Services applicatifs

### Backend

- [x] Route `/health`
- [x] Route `/`
- [x] Route `/db`
- [x] Route `/cache`
- [x] Route `/contact`
- [x] Connexion PostgreSQL
- [x] Connexion Redis
- [x] Envoi d’email via MailHog

### Frontend

- [x] Interface frontend fonctionnelle
- [x] Appel API `/health`
- [ ] Dashboard de statut plus complet (backend / db / cache / mail)

---

# Livrable 2.2 — Dockerfiles optimisés

## Backend

- [x] Multi-stage build
- [x] Stage builder (installation dépendances)
- [x] Stage production minimal
- [x] Utilisateur non-root avec UID/GID explicite
- [x] Variables d’environnement (pas de secrets dans l’image)
- [x] `.dockerignore`
- [x] Ordre des instructions optimisé pour le cache
- [x] Labels OCI (`org.opencontainers.image.*`)
- [x] Healthcheck intégré
- [x] Comparatif taille image avant / après optimisation

## Frontend

- [x] Multi-stage build
- [x] Build Vite → dossier `dist`
- [x] Image finale nginx minimal
- [x] `.dockerignore`
- [x] Labels OCI
- [x] Comparatif taille image avant / après optimisation
- [ ] Utilisateur non-root explicite
- [ ] Healthcheck frontend fonctionnel

---

# Livrable 2.3 — Docker Compose multi-environnements

## Configuration actuelle

- [x] `docker-compose.yml`
- [x] `.env.example` documenté
- [x] `.env` ignoré par Git
- [x] Volume nommé PostgreSQL

## À implémenter

### Fichiers compose

- [ ] `docker-compose.override.yml` (environnement développement)
- [ ] `docker-compose.prod.yml` (environnement production)

### Configuration services

- [ ] Restart policies
- [ ] Logging driver configuré
- [ ] Limites ressources en production (`deploy.resources.limits`)

### Réseaux

- [ ] Réseau frontend
- [ ] Réseau backend
- [ ] Isolation DB (non accessible depuis le réseau frontend)

### Volumes

- [x] Volume PostgreSQL
- [ ] Volume Redis

---

# Partie 3 — Reverse Proxy Traefik

## Configuration Traefik

- [x] Traefik v3
- [x] Docker provider activé
- [x] Configuration statique (`traefik.yml`)
- [x] Dashboard Traefik fonctionnel
- [x] Routage frontend via Traefik
- [x] Routage backend via Traefik

## Routing par hostnames

- [ ] `app.localhost` → Frontend
- [ ] `api.localhost` → Backend
- [ ] `db.localhost` → Adminer
- [ ] `mail.localhost` → MailHog
- [ ] `traefik.localhost` → Dashboard Traefik

## HTTPS local

- [ ] Entrypoint `web` (:80)
- [ ] Entrypoint `websecure` (:443)
- [ ] Redirection automatique HTTP → HTTPS
- [ ] Certificats locaux via mkcert

## Middlewares Traefik

- [ ] Rate limiting sur l’API (100 req/min)
- [ ] Headers de sécurité
- [ ] Basic Auth dashboard Traefik
- [ ] Basic Auth Adminer
- [ ] Compression gzip

## Load Balancing

- [ ] 2 replicas du backend
- [ ] Démonstration du load balancing via Traefik
