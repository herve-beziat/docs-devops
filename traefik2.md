```mermaid
graph TD
    Client([🌐 Client])

    subgraph Traefik
        EP80[Entrypoint :80<br/>web]
        EP443[Entrypoint :443<br/>websecure]
        
        subgraph Middlewares
            REDIRECT[https-redirect<br/>HTTP → HTTPS 301]
            SECURITY[security-headers<br/>X-Frame, HSTS, XSS...]
            GZIP[gzip-compress<br/>Compression brotli/gzip]
            RATE[rate-limit<br/>100 req/min]
        end
    end

    subgraph Services
        FRONTEND[🖥️ Frontend<br/>app.localhost]
        BACKEND[⚙️ Backend<br/>api.localhost]
        ADMINER[🗄️ Adminer<br/>db.localhost]
        MAILHOG[📧 MailHog<br/>mail.localhost]
        DASHBOARD[📊 Dashboard<br/>traefik.localhost]
    end

    Client -->|HTTP :80| EP80
    EP80 --> REDIRECT
    REDIRECT -->|301 HTTPS| Client

    Client -->|HTTPS :443| EP443
    EP443 --> SECURITY
    SECURITY --> GZIP

    GZIP -->|app.localhost| FRONTEND
    GZIP --> RATE
    RATE -->|api.localhost| BACKEND

    EP443 -->|db.localhost| ADMINER
    EP443 -->|mail.localhost| MAILHOG
    EP443 -->|traefik.localhost| DASHBOARD
