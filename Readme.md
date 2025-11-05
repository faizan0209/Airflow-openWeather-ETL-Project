# 🌤️ Airflow OpenWeather ETL Project

## 📘 Overview
This project automates the process of **Extracting**, **Transforming**, and **Loading (ETL)** weather data from the **OpenWeather API** into **PostgreSQL** and **Amazon S3** using **Apache Airflow**.  
It is deployed on an **AWS EC2 instance** using **Docker Compose**.

---

## 📊 Data Flow Diagram

![Data Flow Diagram](./Arch%20Diagram.png)

## ⚙️ Tech Stack
- **Apache Airflow** – Workflow orchestration  
- **Python (pandas)** – Data transformation  
- **OpenWeather API** – Data source  
- **PostgreSQL** – Database  
- **Amazon S3** – Data storage  
- **Docker & Docker Compose** – Containerization  
- **AWS EC2** – Deployment  

---

## 🔁 ETL Flow
1. **Extract:** Airflow fetches weather data from OpenWeather API.  
2. **Transform:** Converts temperature from Kelvin → Fahrenheit and formats timestamps.  
3. **Load:**  
   - Uploads CSV to **Amazon S3**  
   - Inserts structured records into **PostgreSQL**

---

## 🧩 DAG Tasks

| Task ID | Description |
|----------|--------------|
| `is_weather_api_ready` | Checks if OpenWeather API is reachable |
| `extract_weather_data` | Fetches live weather data |
| `transform_load_weather_data` | Transforms data and loads it into S3 & PostgreSQL |

---

## 📂 Folder Structure
Airflow-OpenWeather-Pipeline/
│
├── docker-compose.yaml # Defines Airflow, Postgres, Redis, PgAdmin containers
├── Dockerfile # Custom Docker build for Airflow
├── weather_dag-modify.py # Airflow DAG for ETL process
└── Readme.md # Project documentation

## 🗃️ Airflow Connections Setup

### 1️⃣ OpenWeather API Connection
- **Conn Id:** `weathermap_api`  
- **Conn Type:** HTTP  
- **Host:** `https://api.openweathermap.org`

### 2️⃣ PostgreSQL Connection
- **Conn Id:** `postgres_default`  
- **Conn Type:** Postgres  
- **Host:** `postgres`  
- **Schema:** `airflow`  
- **Login:** `airflow`  
- **Password:** `airflow`  
- **Port:** `5432`

---

##  AWS Credentials
In your DAG file, add your AWS temporary credentials:
```python
aws_credentials = {
    "key": "<YOUR_AWS_ACCESS_KEY>",
    "secret": "<YOUR_AWS_SECRET_KEY>",
    "token": "<YOUR_SESSION_TOKEN>"
}


Start Airflow & Dependencies

docker-compose up -d
Username: airflow
Password: airflow
Enable the DAG

In Airflow UI, search for weather_dag

Turn it ON (toggle)

Click Trigger DAG
