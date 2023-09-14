# Apache Airflow Data Pipeline for API to Google BigQuery Transfer

## Overview

This repository hosts a robust Apache Airflow data pipeline designed to seamlessly transfer data from an API source to Google BigQuery, providing a scalable, automated, and reliable solution for data integration. The pipeline is powered by Apache Airflow and orchestrated using the Celery Executor.

## Key Features

- Apache Airflow orchestration for ETL (Extract, Transform, Load) processes.
- Data extraction from a RESTful API source.
- Data transformation and cleansing using custom-defined tasks.
- Bulk loading of processed data into Google BigQuery tables.
- Docker Compose for simplified deployment and scalability.
- Detailed documentation and setup instructions.

## Table of Contents

### 1. Introduction

### 2. Prerequisites

- Install Docker
- Install Docker Compose
- Install Docker Desktop on Windows
- Environment Setup

### 3. Getting Started

- Running Docker Build for Custom Images

### 4. Repository Structure

### 5. Project

### 6. Usage

### 7. Contributing

### 8. License

## Introduction

Apache Airflow and Apache Spark are powerful tools for orchestrating and processing data workflows. This repository provides a straightforward way to set up Airflow and Spark using Docker Compose, making it easy to begin working with different executor configurations.

## Prerequisites

Before you can effectively use this repository, you need to set up Docker and Docker Compose on your system.

### Install Docker

Docker is a containerization platform that allows you to package and distribute applications as containers. Follow the installation guide for your operating system:
[Install Docker on Windows](https://docs.docker.com/desktop/install/windows-install/)

### Install Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. Install Docker Compose by following the official guide:
[Install Docker Compose](https://docs.docker.com/compose/install/)

### Install Docker Desktop on Windows

If you are using Windows, it's recommended to use Docker Desktop, which provides an integrated environment for Docker on Windows. Follow the instructions to install [Docker Desktop for Windows](https://docs.docker.com/desktop/install/windows-install/).

### Environment Setup: GOOGLE_APPLICATION_CREDENTIALS

- Create a Google Cloud Service Account and download client json file with name `Service_Account_Credentials.json`: <https://www.youtube.com/watch?v=gb0bytUGDnQ>
  - To interact with Google BigQuery, create a Google Cloud Service Account with appropriate permissions.
  - Download the JSON key file associated with the service account. This file will be used for authentication.
- Move json file to `project/config/` folder

## Getting Started

To begin using this repository and set up Apache Airflow and Apache Spark with various executors, follow these steps:

### 1. Clone this repository to your local machine

```bash
git clone https://github.com/truongcaoxuan/airflow-bigquery-docker-compose.git
```

### 2. Navigate to the repository directory

```bash
cd airflow-bigquerry-docker-compose
```

Explore the examples and usage instructions in the respective sections below to configure and run Apache Airflow with your preferred executor.

### Running Docker Build for Custom Images

So we need to create custom Docker images for Airflow, Spark, or MongoDB and add dependencies via a requirements.txt file, follow these steps:

Navigate to the respective directory for the custom image you want to build.

Ensure that the custom image is added to your docker-compose.yml file.

Run Docker Compose to set up your environment as per the examples provided.

### Build the Airflow image

```bash
cd docker/airflow-dag
docker build -t airflow-bigquery:2.6.2-python3.8 .
```

## Repository Structure

The repository is organized as follows:

- docker/: Contains Dockerfile to build docker images: airflow-dag, spark-cluster, mongodb
- project/: Contains airflow dag examples Data pipeline - COVID-19 - Celery Executor.
  - docker-compose.yml: The Docker Compose configuration file for setting up Airflow and related services.
  - dags/: Directory to store your Apache Airflow DAGs (workflow definitions).

- README.md: This README file with instructions and descriptions.

## Project

The project will include a scheduled data pipeline for transferring data from an API to Google BigQuery.

## Usage

Detailed usage instructions for each executor type and examples can be found in their respective subdirectories within the examples directory.

## Contributing

If you'd like to contribute to this repository, please follow the standard GitHub workflow:

- Fork the repository.
- Create a new branch for your feature or bug fix: git checkout -b feature-name
- Make your changes and commit them with clear messages.
- Push your changes to your fork: git push origin feature-name
- Create a Pull Request (PR) from your fork to the main repository.
- Please ensure your code adheres to best practices and includes appropriate documentation.

## License

This repository is licensed under the MIT License. See the LICENSE file for details.

---
By following this guide and using the provided examples, you can set up Apache Airflow and Apache Spark data pipelines with different executors using Docker Compose. Whether you need a simple sequential executor for development or a scalable Celery executor for production, this repository offers a flexible solution. Enjoy building your data pipelines!
