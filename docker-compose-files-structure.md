```mermaid
graph LR
    subgraph BASE[docker-compose.yml]
        B1[Images / Build]
        B2[Variables d'env]
        B3[Labels Traefik]
        B4[Healthchecks]
        B5[Réseaux / Volumes]
    end

    subgraph OVERRIDE[override.yml DEV]
        O1[Ports exposés]
        O2[container_name]
    end

    subgraph PROD[prod.yml PROD]
        P1[restart policy]
        P2[CPU / RAM limits]
        P3[Logging driver]
    end
