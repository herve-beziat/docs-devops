```mermaid
graph TD
    Client([🌐 Client])

    subgraph Traefik
        EP80[Entrypoint :80 web]
        EP443[Entrypoint :443 websecure]
        
        subgraph Middlewares
            REDIRECT[https-redirect\nHTTP → HTTPS 301]
            SECURITY[security-headers\nX-Frame, HSTS, XSS...]
            GZIP[gzip-compress\nCompression brotli/gzip]
            RATE[rate-limit\n100 req/min]
        end
    end

    subgraph Services
        FRONTEND[🖥️ Frontend\napp.localhost]
        BACKEND[⚙️ Backend\napi.localhost]
        ADMINER[🗄️ Adminer\ndb.localhost]
        MAILHOG[📧 MailHog\nmail.localhost]
        DASHBOARD[📊 Dashboard\ntraefik.localhost]
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
