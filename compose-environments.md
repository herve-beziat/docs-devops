```mermaid
graph TD
    subgraph Fichiers
        BASE["📄 docker-compose.yml
        Configuration de base
        ─────────────────
        • Services définis
        • Réseaux
        • Variables d'env
        • Labels Traefik"]

        OVERRIDE["📄 docker-compose.override.yml
        Environnement DEV
        ─────────────────
        • Ports exposés debug
        • Volumes hot-reload
        • Logs verbeux
        ⚡ Chargé automatiquement"]

        PROD["📄 docker-compose.prod.yml
        Environnement PROD
        ─────────────────
        • Restart policies
        • Limites CPU/RAM
        • Logs structurés
        🔒 Chargé manuellement"]
    end

    subgraph Commandes
        CMD_DEV["💻 Développement
        docker compose up -d
        ─────────────────
        Fusionne automatiquement
        docker-compose.yml
        +
        docker-compose.override.yml"]

        CMD_PROD["🚀 Production
        docker compose
        -f docker-compose.yml
        -f docker-compose.prod.yml
        up -d
        ─────────────────
        Fusionne manuellement
        docker-compose.yml
        +
        docker-compose.prod.yml"]
    end

    subgraph Résultat
        DEV_RESULT["🖥️ Stack DEV
        • Debug activé
        • Ports accessibles
        • Reload automatique"]

        PROD_RESULT["⚙️ Stack PROD
        • Auto-redémarrage
        • Ressources limitées
        • Logs structurés"]
    end

    BASE --> CMD_DEV
    OVERRIDE --> CMD_DEV
    BASE --> CMD_PROD
    PROD --> CMD_PROD

    CMD_DEV --> DEV_RESULT
    CMD_PROD --> PROD_RESULT
