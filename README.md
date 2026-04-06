# Stock Market Pipeline

![Snowflake](https://img.shields.io/badge/Snowflake-29B5E8?logo=snowflake&logoColor=white)
![DBT](https://img.shields.io/badge/dbt-FF694B?logo=dbt&logoColor=white)
![Apache Airflow](https://img.shields.io/badge/Apache%20Airflow-017CEE?logo=apacheairflow&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![Kafka](https://img.shields.io/badge/Apache%20Kafka-231F20?logo=apachekafka&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?logo=powerbi&logoColor=black)

## Project Overview

This repository contains an end-to-end real-time stock market data pipeline built with a modern data stack. The flow captures live stock data from an external API, streams it through Kafka, lands it for ingestion, orchestrates loading with Airflow, transforms it in Snowflake with dbt, and prepares it for analytics and dashboarding.

![Architecture](https://github.com/user-attachments/assets/6b49eb4d-4bf7-473d-9281-50c20b241760)

## Tech Stack

- Snowflake for warehousing
- dbt for SQL transformations
- Apache Airflow for orchestration
- Apache Kafka for streaming
- Python for ingestion scripts
- Docker for local services
- Power BI for analytics

## Key Features

- Live stock market data ingestion from an API
- Real-time event streaming with Kafka
- Automated orchestration using Airflow
- Bronze, silver, and gold data modeling with dbt
- Snowflake-ready analytical outputs
- Power BI reporting support

## Repository Structure

```text
stock-market-pipeline/
|-- producer/                     # Kafka producer
|   `-- producer.py
|-- consumer/                     # Kafka consumer
|   `-- consumer.py
|-- dbt_stocks/models/
|   |-- bronze/
|   |   |-- bronze_stg_stock_quotes.sql
|   |   `-- sources.yml
|   |-- silver/
|   |   `-- silver_clean_stock_quotes.sql
|   `-- gold/
|       |-- gold_candlestick.sql
|       |-- gold_kpi.sql
|       `-- gold_treechart.sql
|-- dag/
|   `-- minio_to_snowflake.py
|-- docker-compose.yml
|-- airflow_initial.txt
|-- requirements.txt
`-- README.md
```

## Getting Started

1. Clone the repository.
2. Configure the required environment variables and service credentials.
3. Start the local services with Docker.
4. Run the producer to publish stock events.
5. Run the consumer and Airflow pipeline.
6. Build transformations in dbt and connect your reporting layer.

## Pipeline Flow

1. The producer fetches live stock data from the Finnhub API.
2. Kafka carries the streaming events.
3. The consumer persists the events for downstream ingestion.
4. Airflow moves the data into Snowflake staging tables.
5. dbt builds bronze, silver, and gold models.
6. Power BI reads analytics-ready outputs for dashboards.
<img width="1860" height="920" alt="Screenshot 2026-04-06 170904" src="https://github.com/user-attachments/assets/68f0f9fd-fbee-4cdc-a9aa-a67065827964" />

<img width="1907" height="875" alt="Screenshot 2026-04-06 194310" src="https://github.com/user-attachments/assets/451e3501-dc4b-4d69-966e-0803cd526682" />


## Main Components

### Producer

`producer/producer.py` fetches live stock prices and publishes them into Kafka as JSON events.

### Consumer

`consumer/consumer.py` consumes Kafka messages and stores them in the landing layer for further processing.

### Airflow

`dag/minio_to_snowflake.py` orchestrates ingestion into Snowflake on a schedule.

### dbt

The `dbt_stocks/models` directory contains:

- bronze models for staged raw data
- silver models for cleaned and validated records
- gold models for analytics outputs such as KPI, candlestick, and tree map views

## Requirements

Install Python dependencies with:

```bash
pip install -r requirements.txt
```

Start the local services with:

```bash
docker compose up -d
```
