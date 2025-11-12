# Medium Article Search Engine using Airflow, Pinecone & Sentence Transformers

This demonstrates how to integrate **Pinecone** vector database and **Sentence Transformers** with **Apache Airflow** to build an end-to-end text embedding and search pipeline.

---

## Setup Instructions:

### Modify `docker-compose.yaml`

- Added the following dependencies in the Airflow Docker Image:
  - `sentence-transformers`
  - `pinecone-client`

![docker](https://raw.githubusercontent.com/aakashvardhan/airflow-pinecone-embeddings-pipeline/main/screenshots/docker-compose-modify.png)

### Restart Containers

```bash
docker compose down
docker compose up airflow-init
```

Makes sure all Airflow services (`webserver`, `scheduler`, `worker`, `postgres`, `redis`) are running.

### Pinecone Setup

1. Create a Pinecone account [here](https://www.pinecone.io/)

![l](https://raw.githubusercontent.com/aakashvardhan/airflow-pinecone-embeddings-pipeline/main/screenshots/pinecone-main-page.png)

2. Get your API key and environment

![l](https://raw.githubusercontent.com/aakashvardhan/airflow-pinecone-embeddings-pipeline/main/screenshots/pinecone-api-key.png)

3. In Airflow, go to Admin -> Variable -> Create and add:
   - Key: `pinecone_api_key`
   - Value: your API token.

![l](https://raw.githubusercontent.com/aakashvardhan/airflow-pinecone-embeddings-pipeline/main/screenshots/airflow-variables.png)

### Airflow DAG: `Medium_to_Pinecone`

**Key Tasks**

1. `download_data()` -> Downloads a public Medium dataset from S3 and stores it in `/tmp/medium_data`.

![l](https://raw.githubusercontent.com/aakashvardhan/airflow-pinecone-embeddings-pipeline/main/screenshots/download_data_log.png)

2. `preprocess_data(data_path)` -> Cleans titles and subtitles, merges them into metadata, and saves the processed CSV.

![l](https://raw.githubusercontent.com/aakashvardhan/airflow-pinecone-embeddings-pipeline/main/screenshots/preprocess_data_log.png)
