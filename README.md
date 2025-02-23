# Automated-Text-Extraction

## Overview

This project automates the extraction of text from PDF files using two different approaches and builds a client-facing application for interacting with the extracted data. The system processes PDFs using open-source tools and Unstructured API, enabling users to interactively explore the results through a Streamlit interface.

---

## Project Resources

- **Google Codelab**: [Codelab Link](https://codelabs-preview.appspot.com/?file_id=1-5QP7m-QK3vR2Jtv8-lNfvdp06IYvoHcKmNlVWzhRqU#0)
- **App (Deployed on AWS EC2)**: [Streamlit Link](http://18.188.86.27:8501/)
- **Airflow (Deployed on AWS EC2)**: [Airflow Link](https://18.188.86.27:8080/)

---

## Technologies

![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)
![AWS](https://img.shields.io/badge/Amazon%20AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![S3](https://img.shields.io/badge/Amazon%20S3-569A31?style=for-the-badge&logo=amazon-s3&logoColor=white)
![RDS](https://img.shields.io/badge/Amazon%20RDS-527FFF?style=for-the-badge&logo=amazon-rds&logoColor=white)
![Hugging Face](https://img.shields.io/badge/Hugging%20Face-FFD43B?style=for-the-badge&logo=huggingface&logoColor=black)
![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![AWS Parameter Store](https://img.shields.io/badge/AWS%20Parameter%20Store-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=JSON-web-tokens&logoColor=white)
![Airflow](https://img.shields.io/badge/Airflow-017CEE?style=for-the-badge&logo=apache-airflow&logoColor=white)

---

## Architecture Diagram

![flow_diagram](https://github.com/aniket-afk/Automated-Text-Extraction/blob/main/ArchitectureDiagram/final_architecturediagram.png)

---

## Project Flow

### Step 1: PDF Processing

- The system processes PDF files using two approaches:
  - **Open-Source Tools** (PyMuPDF): Converts PDFs into markdown and extracts images.
  - **Unstructured API**: Processes large PDFs using a custom pipeline with high concurrency, capable of handling complex document structures.

### Step 2: Data Storage and Management

- **S3 Buckets**: Stores the original PDFs and the processed outputs (markdown, images, JSON).
- **RDS (MySQL)**: Manages the metadata for the PDFs and processed files, allowing efficient querying and updates.

### Step 3: Client Interaction via Streamlit

- Users access the processed data through the Streamlit interface, which provides features to:
  - Upload new PDFs.
  - View and download extracted content.
  - Analyze the metadata and processed data.

### Step 4: API Development with FastAPI

- **FastAPI**: Serves as a backend framework to create and manage API endpoints for the application. It handles requests for PDF processing and data retrieval, ensuring efficient communication between the client interface and the underlying services.
  - Provides endpoints for:
    - **User Authentication**:
      - **Login**: Endpoint for user login to authenticate users and initiate sessions.
      - **Registration**: Endpoint for new users to create accounts, storing their credentials securely in the database.
    - Fetching extracted data and metadata.
    - **Downloading PDF Files**: API endpoints to facilitate the download of original PDF files.
    - Integrating with the OpenAI API for further insights.

### Step 5: AI Integration

- **OpenAI GPT Model**: Used to handle natural language queries on the extracted data, providing insights based on the document content.

## How to Run the application

```bash
git clone https://github.com/aniket-afk/Automated-Text-Extraction.git

# UPDATE PARAMETER STORE WITH YOUR KEYS AND SETUP  IAM ACCESS
ACCESS_KEY_ID_AWS: <your-access-key-id>
SECRET_ACCESS_KEY_AWS: <your-secret-access-key>
OPEN_AI_API_KEY: <your-open-ai-api-key>

# Dockerize the application

docker build -t aniket-afk/airflow-image:latest .

#create tage and then push
docker push aniket-afk/airflow-image:latest

# Create an EC instance and do the below pre requisities

sudo apt-get update
sudo apt-get install docker.io
sudo systemctl start docker
sudo systemctl enable docker

docker login
docker pull aniket-afk/airflow-image:latest .


# To run the application
docker run -d -p 8080:8080 aniket-afk/airflow-image:latest

```

Access the Application
http://75.101.133.31:8080 for Airflow
http://75.101.133.31:8501 for Streamlit

---

## Contact

For Any questions or support, please contact [Aniket Patole](mailto:aniketpatole6@gmail.com).
