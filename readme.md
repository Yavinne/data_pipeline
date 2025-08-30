🚀 Pipeline ETL - Open Data (Batch Processing)
📌 Objectif du projet

Ce projet illustre la mise en place d’un pipeline ETL complet (Extract – Transform – Load) permettant d’ingérer, transformer et charger des données ouvertes dans une base de données relationnelle.
L’objectif est de fournir un exemple concret et réutilisable d’ingénierie de données pour des cas d’analyse ultérieurs (dashboards, APIs, etc.).

🛠️ Stack Technique

Langage : Python 3.10+

Orchestration : Apache Airflow

Stockage : PostgreSQL (peut être remplacé par MySQL ou BigQuery)

Transformation : Pandas / SQL

Containerisation : Docker & Docker Compose

Tests : Pytest

📂 Sources de données

Pour ce projet, les données proviennent de l’API Open Data de la qualité de l’air :
👉 https://opendata.paris.fr/explore/dataset/

📌 Exemple :

Données brutes : niveaux de pollution journaliers par ville

Format : JSON / CSV

Volume : quelques Mo par jour

🔄 Architecture du pipeline
flowchart LR
    A[API Open Data] --> B[Airflow Extract Task]
    B --> C[Transform (Pandas)]
    C --> D[Load into PostgreSQL]
    D --> E[Analytical Queries / BI Tools]


Extract : récupération des données depuis l’API (ou fichier CSV).

Transform : nettoyage (valeurs nulles, typage), enrichissement (calculs de moyennes, agrégations).

Load : insertion dans une table PostgreSQL normalisée.

🚀 Lancement du projet
1️⃣ Cloner le repo
git clone https://github.com/username/pipeline-etl-opendata.git
cd pipeline-etl-opendata

2️⃣ Lancer les services
docker-compose up -d

3️⃣ Accéder aux outils

Airflow UI → http://localhost:8080

PostgreSQL → localhost:5432 (user/password définis dans .env)

4️⃣ Lancer le DAG

Activer le DAG etl_air_quality dans Airflow et exécuter le pipeline.

📊 Exemple de schéma PostgreSQL
CREATE TABLE air_quality (
    id SERIAL PRIMARY KEY,
    city VARCHAR(255),
    date DATE,
    pm10 FLOAT,
    no2 FLOAT,
    o3 FLOAT,
    created_at TIMESTAMP DEFAULT NOW()
);

✅ Résultats attendus

Données brutes extraites quotidiennement

Données transformées (format homogène, colonnes nettoyées)

Base PostgreSQL prête pour l’analyse (requêtes SQL, BI, dashboards).

🔮 Améliorations possibles

Ajouter un contrôle qualité avec Great Expectations

Automatiser les tests unitaires avec CI/CD (GitHub Actions)

Déployer le pipeline sur GCP/AWS/Azure

Créer un dashboard Streamlit/Metabase branché sur PostgreSQL