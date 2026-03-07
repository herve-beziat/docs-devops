```mermaid
flowchart LR
    U[Client]
    T[Traefik Router]
    M[Middleware]
    S[Service]

    U --> T
    T --> M
    M --> S
```
