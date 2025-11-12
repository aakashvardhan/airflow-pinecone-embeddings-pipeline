# Pinecone + Sentence Transformers Integration with Airflow

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
