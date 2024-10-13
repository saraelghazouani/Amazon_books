# Amazon Books Data Pipeline
This project is an ETL (Extract, Transform, Load) pipeline built using Apache Airflow. It extracts book data from Amazon, processes it, and loads it into a PostgreSQL database. The goal is to automate the process of fetching book data from Amazon, cleaning the data, and storing it in a relational database for further analysis or reporting.
## Project Structure
```
├── dags
│   └── dag.py       # DAG definition
├── docker-compose.yml            # Docker Compose file to setup Airflow and PostgreSQL
├── requirements.txt              # Python dependencies for the project
└── README.md                     # Project documentation
```
## Components
### Apache Airflow
Apache Airflow is used to manage and schedule the ETL tasks. A Directed Acyclic Graph (DAG) is defined to run tasks in sequence:

Extract: Fetch Amazon book data (e.g., book titles, authors, prices).
Transform: Clean and preprocess the fetched data.
Load: Insert the cleaned data into a PostgreSQL database.
### PostgreSQL
A PostgreSQL instance is used as the destination to store the transformed data. A table named books will be created in the database, where each row corresponds to a book and its details.

### Docker
This project uses Docker Compose to set up the Airflow environment and PostgreSQL. Docker containers include:

- Airflow Scheduler
- Airflow Webserver
- Airflow Worker
- PostgreSQL
- pgAdmin: For PostgreSQL database management.

## Prerequisites
- Docker and Docker Compose
- Python 3.11 or later
- Airflow 2.10.2
- PostgreSQL 13

  ## Run project
### . Clone the repository
```
git clone https://github.com/saraelghazouani/amazon_books_pipeline.git
cd amazon_books_pipeline
```
### . Install Dependencies
```
pip install -r requirements.txt
```
### . Set up Docker Environment
```
docker-compose up
```
This will start the following services:

-Airflow Web UI: Accessible at http://localhost:8080

-pgAdmin (for PostgreSQL management): Accessible at http://localhost:5050

-PostgreSQL database: Accessible on port 5432

### . Configure PostgreSQL in pgAdmin

 #### -Open pgAdmin at http://localhost:5050.

 #### -Create a new server in pgAdmin using the following connection details:

  - Host: amazon_books-postgres-1

  - Port: 5432

  - Username: airflow

  - Password: airflow

  - Database: postgres
  
### . DAG Overview
The DAG is defined in the file dags/dag.py. It contains the following tasks:

- Fetch Amazon Data: Uses a Python script to scrape book data from Amazon.

- Clean Data: A PythonOperator task to process and clean the raw data.

- Store Data: Loads the cleaned data into PostgreSQL using the PostgresOperator.

The DAG is scheduled to run daily.

### . Running the DAG
   
   1- Open the Airflow web UI at http://localhost:8080.
   
   2- Activate the DAG named fetch_and_store_amazon_books.
   
   The DAG will automatically start fetching, processing, and storing Amazon book data.

### . Files
  - dag.py: Contains the DAG definition and task logic for the ETL pipeline.
   
  - docker-compose.yml: Configures the Docker containers for Airflow and PostgreSQL.

  - requirements.txt: Specifies the Python libraries needed for this project.
