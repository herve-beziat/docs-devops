```mermaid
graph TD
    subgraph APRES[Après - réseaux isolés]
        NF[réseau frontend]
        NB[réseau backend]
        NF --- FRONT2[Frontend]
        NF --- TR2[Traefik]
        NB --- BACK2[Backend]
        NB --- TR3[Traefik]
        NB --- DB2[PostgreSQL]
        NB --- RED2[Redis]
        NB --- MAIL2[MailHog]
        NB --- ADM2[Adminer]
    end

    subgraph AVANT[Avant - 1 seul réseau]
        N1[réseau devops]
        N1 --- FRONT1[Frontend]
        N1 --- BACK1[Backend]
        N1 --- DB1[PostgreSQL]
        N1 --- RED1[Redis]
        N1 --- MAIL1[MailHog]
        N1 --- ADM1[Adminer]
        N1 --- TR1[Traefik]
    end

    
