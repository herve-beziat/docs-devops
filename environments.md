```mermaid 
graph TD
    BASE[docker-compose.yml<br/>Configuration de base<br/>commune à tous les envs]

    BASE --> DEV
    BASE --> PROD

    subgraph DEV[Environnement Dev]
        OVERRIDE[docker-compose.override.yml<br/>Chargé automatiquement]
        OVERRIDE --> D1[Volumes montés<br/>hot reload]
        OVERRIDE --> D2[Ports exposés<br/>pour debug]
        OVERRIDE --> D3[Logs verbeux]
    end

    subgraph PROD[Environnement Prod]
        PRODFILE[docker-compose.prod.yml<br/>Chargé manuellement]
        PRODFILE --> P1[Restart policies<br/>auto-redémarrage]
        PRODFILE --> P2[Limites ressources<br/>CPU et RAM]
        PRODFILE --> P3[Logs structurés<br/>json-file driver]
    end

    DEV --> CMD1[docker compose up -d]
    PROD --> CMD2[docker compose -f docker-compose.yml<br/>-f docker-compose.prod.yml up -d]
