# 🌦️ Weather ETL Pipeline avec Apache Airflow

## 🎯 Objectif

Ce projet met en place un pipeline ETL pour extraire, transformer et charger des données météorologiques en temps réel à partir de l’API [Open-Meteo](https://open-meteo.com/), à l’aide d’Apache Airflow et PostgreSQL.

---

## ⚙️ Architecture

```
[Open-Meteo API] --> [Airflow DAG: extract -> transform -> load] --> [PostgreSQL Database]
```

---

## 🛠️ Technologies utilisées

- Apache Airflow 2.10.3
- PostgreSQL 13
- Docker & Docker Compose
- Python 3.12
- Open-Meteo API
- Redis (backend Airflow)

---

## 📁 Structure du projet

```
.
├── dags/
│   └── weather_etl_pipeline.py       # Le DAG principal avec les tâches ETL
├── docker-compose.yaml               # Conteneurisation de l’environnement Airflow
├── requirements.txt                  # Dépendances Python
└── README.md                         # Documentation du projet
```

---

## 🔄 Fonctionnement du pipeline

1. **Extraction** : appel HTTP à l’API Open-Meteo avec latitude/longitude.
2. **Transformation** : sélection des données pertinentes (température, vent, etc.).
3. **Chargement** : insertion dans une table PostgreSQL (`weather_data`).

---

## 🐳 Déploiement avec Docker

```bash
# Lancer les conteneurs
docker-compose up -d

# Initialiser Airflow
docker-compose run airflow-webserver airflow db init

# Créer un utilisateur admin
docker-compose run airflow-webserver airflow users create \
  --username admin --firstname Meryem --lastname Admin \
  --role Admin --email admin@example.com --password admin

# Accéder à l'interface Airflow
http://localhost:8080
```

---

## 🧪 Test du DAG

- Aller sur l’interface Airflow (`http://localhost:8080`)
- Activer le DAG `weather_etl_pipeline`
- Lancer une exécution manuelle ou planifier avec `schedule_interval="* * * * *"` (chaque minute)

---

## 🗃️ Exemple de données insérées dans PostgreSQL

| latitude | longitude | temperature | windspeed | timestamp           |
|----------|-----------|-------------|-----------|---------------------|
| 51.5074  | -0.1278   | 18.5        | 13.2      | 2025-05-13 14:00:00 |

---

## 📊 Visualisation des données avec Power BI
Après l'extraction et la transformation des données météorologiques via Apache Airflow, celles-ci sont visualisées à l'aide de Power BI pour une analyse approfondie et interactive.

**🔹 Objectifs de la visualisation**
- **Suivi des températures :** Affichage des températures maximales et minimales sur une période donnée.

- **Analyse de la vitesse du vent :** Visualisation des vitesses moyennes et maximales du vent.

- **Cartographie :** Représentation géographique des données météorologiques pour Londres , UK.

- **Tendances temporelles :** Observation des variations météorologiques au fil du temps.
   
## 🔹 Aperçu du tableau de bord


## 🚀 Améliorations possibles

- Ajout de tests unitaires pour chaque tâche.
- Gestion des erreurs réseau ou d’API.
- Intégration avec Grafana pour visualiser les données.

---

## 📝 Auteur

Meryem — 19/05/2025
