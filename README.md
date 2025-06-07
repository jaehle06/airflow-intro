# Airflow Intro Project - User Processing DAG

This repository contains a beginner-friendly Airflow project that demonstrates building a simple ETL pipeline using the new **Airflow 3 SDK syntax**.  
It extracts fake user data from a public API, processes it, stores it as CSV, and finally loads it into a PostgreSQL table.

---

## 📦 Stack

- Apache Airflow 3.x
- Docker (Airflow Dev environment)
- PostgreSQL (via Docker)
- Python 3.11
- Airflow SDK (`@dag`, `@task`)
- CSV & HTTP APIs

---

## 💡 Concepts Practiced
- Airflow SDK (@dag, @task, @task.sensor)
- XCom data passing
- DAG dependency graph using Bitshift (>>)
- Sensors and API integration
- File I/O with CSV
- PostgresHook (data ingestion)

---

## 🧪 What the DAG Does

### DAG ID: `user_processing`

| Step             | Description |
|------------------|-------------|
| `create_table`   | Creates `users` table in PostgreSQL if not exists |
| `is_api_available` | Sensor that checks if the user API is reachable |
| `extract_user`   | Extracts user data (id, firstname, lastname, email) from JSON |
| `process_user`   | Adds `created_at` timestamp and writes user data to `/tmp/user_info.csv` |
| `store_user`     | Loads the CSV data into the `users` table using `PostgresHook.copy_expert()` |

---

## 🔁 DAG Flow

create_table
     ↓
is_api_available
     ↓
extract_user
     ↓
process_user
     ↓
store_user
