```mermaid
graph TD
    DEV[Developer<br/>local machine]
    GIT[GitHub<br/>repository]
    CI[CI/CD Pipeline<br/>GitHub Actions / Jenkins...]
    SERVER[Production Server<br/>VPS / Cloud...]

    DEV -->|git push| GIT
    GIT -->|trigger| CI
    CI -->|docker compose -f docker-compose.yml<br/>-f docker-compose.prod.yml up -d| SERVER
