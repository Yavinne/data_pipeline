# Pipeline ETL - Open Data Qualité de l’air

## Table des matières
1. [Contexte & Objectifs](#contexte--objectifs)  
2. [Stack Technique](#stack-technique)  
3. [Sources de Données](#sources-de-données)  
4. [Architecture du Pipeline](#architecture-du-pipeline)  
5. [Installation & Lancement](#installation--lancement)  
6. [Modèle de Données](#modèle-de-données)  
7. [Résultats Attendus](#résultats)  
8. [Améliorations Possibles](#améliorations-possibles)  
9. [Licence](#licence)  
10. [Contacts](#contacts)  

---

## Contexte & Objectifs
L’entreprise fictive **GreenAir Analytics** aide les municipalités à analyser la qualité de l’air dans les grandes villes françaises afin de :  
- Détecter les pics de pollution (PM10, NO₂, O₃).  
- Produire des rapports journaliers pour les autorités locales.  
- Mettre à disposition une base de données fiable pour alimenter des dashboards BI.  

👉 Ce projet consiste à mettre en place un **pipeline ETL automatisé** permettant d’ingérer des données de qualité de l’air depuis une API Open Data, de les nettoyer et de les stocker dans une base PostgreSQL pour exploitation analytique.  

[🔝 Back to top](#table-des-matières)  

---

## Stack Technique
- **Langage** : Python 3.13  
- **Orchestration** : Apache Airflow  
- **Stockage** : PostgreSQL (extensible à MySQL ou BigQuery)  
- **Transformation** : Pandas / SQL  
- **Containerisation** : Docker & Docker Compose  
- **Tests** : Pytest  

[🔝 Back to top](#table-des-matières)  

---

## Sources de Données
- **Fournisseur** : [API Open Data - Qualité de l’air Paris](https://opendata.paris.fr/explore/dataset/)  
- **Format** : JSON / CSV  
- **Contenu** : mesures journalières des polluants (PM10, NO₂, O₃) par ville/zone géographique  
- **Volume estimé** : quelques Mo par jour  

[🔝 Back to top](#table-des-matières)  

---

## Architecture du Pipeline
```mermaid
flowchart LR
    A[API Open Data] --> B[Airflow Extract Task]
    B --> C[Transform (Pandas)]
    C --> D[Load into PostgreSQL]
    D --> E[Analytical Queries / BI Tools]
```

[🔝 Back to top](#table-des-matières)

---

## Installation & Lancement

### Cloner le repo
git clone https://github.com/username/pipeline-etl-air-quality.git
cd pipeline-etl-air-quality

### Lancer les services
docker-compose up -d

### Accéder aux outils

Airflow UI → http://localhost:8080

PostgreSQL → localhost:5432 (credentials dans .env)

### Lancer le DAG

Activer le DAG etl_air_quality dans Airflow et exécuter le pipeline.

[🔝 Back to top](#table-des-matières)

---

## Modèle de Données
```mermaid
CREATE TABLE air_quality (
    id SERIAL PRIMARY KEY,
    city VARCHAR(255),
    date DATE,
    pm10 FLOAT,
    no2 FLOAT,
    o3 FLOAT,
    created_at TIMESTAMP DEFAULT NOW()
);
```

[🔝 Back to top](#table-des-matières)

---

## Résultats
- Données brutes ingérées automatiquement chaque jour.
- Données nettoyées et standardisées (colonnes homogènes).
- Base PostgreSQL exploitable directement pour requêtes SQL et BI.

Exemple d’usage : un dashboard Power BI ou Metabase affichant l’évolution de la pollution par ville.

[🔝 Back to top](#table-des-matières)

---

## Améliorations Possibles

Ajouter des contrôles qualité avec Great Expectations.

Mettre en place du monitoring avec Prometheus + Grafana.

Déployer sur un cloud (GCP/AWS/Azure).

Créer une API REST pour exposer les données nettoyées.

[🔝 Back to top](#table-des-matières)

---

## Licence

Ce projet est sous licence MIT.

---

## Contacts

👤 Auteur : Vulfran NDONG
📧 Email : vianneyasog@gmail.com

💼 LinkedIn : linkedin.com/in/tonprofil

🐙 GitHub : github.com/Yavinne