# PySpark Data Cleaning with Google Cloud Storage (GCS)

## Overview

This project demonstrates data cleaning using PySpark. It reads a raw CSV file from a Google Cloud Storage (GCS) bucket, performs various cleaning and transformation operations, and writes the cleaned data back to another GCS bucket in Parquet format. The entire process is containerized using Docker for easy setup and execution.

## Features

*   Connects a local PySpark session to Google Cloud Storage.
*   Reads raw data in CSV format from a GCS bucket.
*   Performs data quality and standardization tasks:
    *   Standardizes string casing and removes extra whitespace.
    *   Parses multiple date formats into a single, consistent format.
    *   Corrects data types (e.g., string to float for monetary values).
    *   Handles missing values by imputing the median for the `amount` column.
    *   Removes duplicate records based on `transaction_id`.
*   Writes cleaned data to GCS in the efficient Parquet format.

## Project Structure

```plaintext
.
├── notebooks/          # Jupyter notebooks for data cleaning(cleaning_data.ipynb)
├── cred/               # GCP credentials (e.g., credentials.json)
├── docker-compose.yaml # Docker Compose file for running services
└── README.md           # This file
```

## Setup Instructions

### Prerequisites

-   Docker and Docker Compose
-   Git
-   A Google Cloud Platform (GCP) account.
-   A GCP Service Account with permissions for GCS (`Storage Admin`).

### Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/pyspark-gcs.git
    cd pyspark-gcs
    ```

2.  **Add GCP Credentials:**
    Download the JSON key for your GCP Service Account and place it in the `cred/` directory with the filename `credentials.json`.

3.  **Start Services:**
    Start services (PySpark on Jupyter Notebook) in detached mode.
    ```bash
    docker-compose up -d
    ```

4.  **Access Jupyter Notebook:**
    To access the Jupyter Notebook, you'll need to retrieve the access token from within the running container.

    a. First, find the container ID by listing all running containers:
    ```bash
    docker ps
    ```
    b. Next, open an interactive shell inside the Jupyter container using its ID:
    ```bash
    docker exec -it <container_id> bash
    ```
    c. Once inside the container, run the following command to get the Jupyter server URL with the access token:
    ```bash
    jupyter server list
    ```
    d. Copy the URL (it will look like `http://73ee5dce97af:8888/?token=23af58e7decf4ad97920f5235941e6ea7110821e09843bf8`) and paste it into your web browser to open JupyterLab.

### Usage
1.  **Open the Notebook:**
    Open your browser and navigate to `http://localhost:8888`. You will be prompted for the token you retrieved in the previous step. Once JupyterLab is open, navigate into the `work/` directory and open the `cleaning_data.ipynb` notebook.

2.  **Configure Paths:**
    Inside the notebook, update the variables for your GCS bucket names and file paths for both the input CSV and the output Parquet data.

3.  **Run the Cells:**
    Execute the cells in the notebook sequentially to perform the data cleaning and transformation process.

4.  **Monitor Spark Jobs:**
    You can monitor the progress of your Spark jobs by opening the Spark UI in your browser at `http://localhost:4040`.

5.  **Verify the Output:**
    After the notebook has finished running, navigate to your output GCS bucket to confirm that the cleaned data has been successfully written in Parquet format.

These additions provide a clear, step-by-step guide for running the project's core logic, making your README.md much more complete and user-friendly.
