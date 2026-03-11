```mermaid
gitGraph LR:
   commit id: "release v1.0 (main)"

   branch develop
   checkout develop

   branch feature/bonus-portainer
   checkout feature/bonus-portainer
   commit id: "add portainer service"
   commit id: "expose via traefik portainer.localhost"
   commit id: "docs: portainer setup"
   checkout develop
   merge feature/bonus-portainer

   branch feature/bonus-monitoring
   checkout feature/bonus-monitoring
   commit id: "add prometheus + cadvisor"
   commit id: "configure traefik metrics scraping"
   commit id: "add grafana service"
   commit id: "provision datasource + dashboards"
   commit id: "expose monitor.localhost via traefik"
   checkout develop
   merge feature/bonus-monitoring

   branch feature/bonus-watchtower
   checkout feature/bonus-watchtower
   commit id: "add watchtower service"
   commit id: "configure container labels include/exclude"
   commit id: "setup webhook notifications"
   commit id: "docs: watchtower config"
   checkout develop
   merge feature/bonus-watchtower

   branch feature/bonus-security-scan
   checkout feature/bonus-security-scan
   commit id: "install trivy"
   commit id: "scan backend image"
   commit id: "scan frontend image"
   commit id: "docs: vulnerability report"
   checkout develop
   merge feature/bonus-security-scan

   branch feature/bonus-swarm
   checkout feature/bonus-swarm
   commit id: "create docker-stack.yml"
   commit id: "configure replicas + rolling update"
   commit id: "configure rollback policy"
   commit id: "demo rolling update no downtime"
   commit id: "docs: swarm deployment"
   checkout develop
   merge feature/bonus-swarm

   checkout main
   merge develop id: "release v2.0 (bonuses)"
