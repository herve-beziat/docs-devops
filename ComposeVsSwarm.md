```mermaid
graph TB
    subgraph Compose["🖥️ Docker Compose (développement)"]
        direction TB
        ENV[".env\nPOSTGRES_PASSWORD=xxx"]
        NET1["Réseau bridge\n(une machine)"]
        SCALE["--scale backend=2"]
    end

    subgraph Swarm["🐳 Docker Swarm (production)"]
        direction TB
        SECRET["Docker Secrets\nchiffrés dans Raft"]
        NET2["Réseau overlay\n(multi-machines)"]
        REPLICAS["replicas: 2\n(zero downtime)"]
        
        subgraph Nodes["Cluster"]
            MANAGER["Manager Node\nTraefik, DB, Redis..."]
            WORKER1["Worker Node\nBackend.1, Frontend.1"]
            WORKER2["Worker Node\nBackend.2"]
        end
    end
