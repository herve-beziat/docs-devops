```mermaid
graph TD
    CMD1[docker compose up -d]
    CMD2[docker compose -f docker-compose.yml\n -f docker-compose.prod.yml up -d]
    
    CMD1 -->|charge automatiquement| BASE[docker-compose.yml]
    CMD1 -->|charge automatiquement| OVERRIDE[docker-compose.override.yml]
    CMD2 -->|charge manuellement| BASE
    CMD2 -->|charge manuellement| PROD[docker-compose.prod.yml]

    BASE --> DEV[Stack DEV\ncontainer_name fixes\nports exposés]
    OVERRIDE --> DEV
    BASE --> PRODSTACK[Stack PROD\nlimites ressources\nrestart policies]
    PROD --> PRODSTACK
