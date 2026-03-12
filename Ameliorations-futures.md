# Améliorations futures — devops-foundations

> Ce fichier recense les pistes d'amélioration identifiées mais non implémentées dans le projet.
> À compléter au fil du temps.

---

## Docker Hardened Images (DHI)

### C'est quoi ?
Les DHI sont des images Docker renforcées côté sécurité, disponibles via le registre `dhi.io`.
Elles sont **gratuites** depuis peu (sans abonnement, sans restriction d'usage).

### Pourquoi ce serait pertinent ici ?
Les images actuelles du projet viennent de Docker Hub (ex: `node:alpine`, `python`, etc.)
et peuvent contenir des dizaines de CVE (failles de sécurité connues).

Les DHI offrent :
- **Zéro ou quasi-zéro CVE** — Docker maintient un patch très rapide
- **Images beaucoup plus légères** — ex: Python passe de 412 MB à 35 MB
- **Moins de packages** — surface d'attaque réduite
- **Compatibilité drop-in** — on change juste le nom de l'image de base

### Ce que ça changerait concrètement
Remplacer dans les Dockerfiles :
```dockerfile
# Avant
FROM node:alpine

# Après
FROM dhi.io/node:22
```

### Où s'appliquerait-on en priorité ?
- **Image finale du backend** → fort intérêt, c'est ce qui tourne en prod
- **Image finale du frontend** → idem
- **Images de build (multi-stage)** → moins utile, on a besoin de tous les outils

### Limite à garder en tête
Les DHI sont **minimalistes** : pas de shell, pas de package manager, pas d'outils de debug.
En cas de problème en prod, le diagnostic se fait via Traefik, les logs et les healthchecks
plutôt qu'en entrant dans le conteneur.

### Ressources
- [Doc officielle DHI](https://docs.docker.com/dhi/)
- [Catalogue des images disponibles](https://hub.docker.com/hardened-images/catalog)
- [Guide de migration](https://docs.docker.com/dhi/migration/)

---

*À compléter : multi-stage build, Docker Build Cloud, ...*
