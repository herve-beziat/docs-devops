```mermaid
flowchart LR
Browser --> HTTPS:443
HTTPS:443 --> Traefik
Traefik --> Frontend
Traefik --> Backend
