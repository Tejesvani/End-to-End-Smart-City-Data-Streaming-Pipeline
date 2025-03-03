# End-to-End Smart City Data Streaming Pipeline

## Project Overview

The **Smart City Data Streaming Pipeline** project is designed to capture and process real-time data streams from various IoT devices deployed in a smart city environment. It processes data from different sources, including vehicle data, GPS coordinates, emergency incidents, weather conditions, and camera footage, which are streamed in real time across various platforms. 

The pipeline integrates Apache Kafka, Apache Spark, Docker, and AWS services to ensure efficient data ingestion, transformation, storage, and analysis. The system’s design and execution are optimized for scalability, reliability, and performance, which are critical for smart city applications.

## Architecture Overview


### Architecture Diagram
<img width="1194" alt="image" src="https://github.com/user-attachments/assets/d1255667-bd9d-4a09-bde6-dc2de8c1c907" />

Picture: Diagram showing the flow of data between various systems, such as IoT devices, Kafka, Spark, AWS S3, Glue, Athena, Redshift

### Technologies Used

- **IoT Devices**: Collect real-time data streams from sensors (e.g., vehicle sensors, cameras).
- **Apache Kafka**: Handles real-time data ingestion, stream processing, and topic management.
- **Apache Spark**: Real-time data processing and streaming engine used for data transformation and computation.
- **Docker**: Used for containerizing and orchestrating Kafka and Spark services.
- **Python**: Scripting for data transformation, integration with AWS services, and Spark job submissions.

#### AWS Services:

- **S3**: Stores processed data as Parquet files.
- **Glue**: Extracts and catalogs data stored in S3.
- **Athena**: Queries the cataloged data in S3.
- **IAM**: Manages roles and permissions to access AWS services.
- **Redshift**: Data warehousing solution for advanced analytics.
- **QuickSight**: Data visualization and dashboarding service for creating reports.

## Project Workflow

### 1. Data Ingestion
- **IoT Devices** capture real-time data, which includes GPS, vehicle diagnostics, weather, and emergency incidents.
- Data is streamed to **Apache Kafka** topics for further processing.

### 2. Data Processing
- **Apache Spark** reads and processes the real-time data from Kafka topics.
- The processed data is written to **AWS S3** as Parquet files.
- Spark Streaming is employed to handle real-time data and includes **checkpointing** for fault tolerance.

### 3. Data Storage & Cataloging
- Processed data is stored in **AWS S3**.
- **AWS Glue** crawlers automatically catalog the data for easier querying.

### 4. Data Warehousing & Querying
- **Amazon Redshift** is used for data warehousing to support advanced analytics.
- **Amazon Athena** allows querying of S3 stored data wthout the need for a database.
  


## Getting Started

### Prerequisites

Before starting, ensure you have the following:

- **Docker** and **Docker Compose** installed on your machine.
- **AWS Account** with S3, Glue, Redshift, and Athena configured.
- **Python 3.x** installed along with required Python libraries.
- A working **Apache Kafka** and **Apache Spark** setup.

### Setup Instructions

#### 1. Clone the Repository
- Clone the repository to your local machine:
```
git clone https://github.com/Tejesvani/End-to-End-Smart-City-Data-Streaming-Pipeline.git
cd End-to-End-Smart-City-Data-Streaming-Pipeline
```

#### 2. Configure Docker
- Edit the `docker-compose.yml` file to configure Kafka and Spark.
- Start the services using:
```
docker-compose build
docker compose up -d
```

#### 3. AWS Configuration
- **IAM Roles:** Set up IAM roles with the necessary permissions for accessing S3, Glue, Athena, and QuickSight.
- Create **S3 Buckets** for storing data.
- **Update Configuration:** In `jobs/config.py`, update with your AWS Access Key and Secret Key.
```
configuration = {
    "AWS_ACCESS_KEY": "your-access-key",
    "AWS_SECRET_KEY": "ypur-secret-key"
}
```

#### 4. Run Data Ingestion:
- Start producing data to Kafka topics using IoT data simulators.
```
python jobs/main.py
```

#### 5. Spark Streaming:
- Submit the Spark job to process and stream data to S3:
```
docker exec -it smartcitydatastreaming-spark-master-1 spark-submit --master "spark://spark-master:7077" --packages "org.apache.spark:spark-sql-kafka-0-10_2.12:3.5.0,org.apache.hadoop:hadoop-aws:3.3.1,com.amazonaws:aws-java-sdk:1.11.469" jobs/smart-city.py
```

## Project Folder Structure
```
End-to-End-Smart-City-Data-Streaming-Pipeline/
│
├── jobs/                      # Data processing and transformation scripts
│   ├── __pycache__/           # Compiled Python files (to be ignored)
│   └── config.py              # AWS configuration (credentials, Keys)
|   └── main.py                # Python script to simulate IoT data and send it to Kafka
|   └── smart-city.py          # Spark application that consumes data from Kafka topics
│
├── venv/                      # Virtual environment (ignored in git)
├── .gitignore                 # Ensures that sensitive files are not tracked in the Git
├── docker-compose.yml         # Docker configuration for Kafka & Spark
├── requirements.txt           # Python dependencies
└── README.md                  # Overview of the project and its setup
```


## Conclusion
The End-to-End Smart City Data Streaming Pipeline project successfully integrates multiple real-time data streams, simulating vehicle movement, GPS tracking, traffic camera monitoring, weather data, and emergency incident reporting. Leveraging Kafka for data ingestion and Spark Structured Streaming for processing, the pipeline demonstrates an efficient way to collect, process, and store vast amounts of data from various sources. The data is streamed and processed in real time, with outputs saved to Amazon S3 in Parquet format, ensuring scalability and easy access for analysis. This project is a solid foundation for future smart city applications, enabling real-time monitoring and decision-making.

## Key Highlights:
- **Detailed Setup**: Clear instructions for setting up Docker, AWS, and running the data pipeline.
- **Technology Stack**: Clearly outlines all the technologies used in the project.
- **Project Workflow**: Describes the end-to-end flow of the data pipeline, from ingestion to visualization.
- **Folder Structure**: Provides an easy-to-understand layout of the project directory.
- **Git Ignore and Sensitive Files**: Ensures that configuration files containing sensitive information (like AWS credentials) are ignored by Git.
  


