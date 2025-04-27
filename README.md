

---

# 🧠 Local AI Chat App Setup Guide

This guide walks you through setting up a local AI chat application using Ollama and Open WebUI. The application allows you to run open-weight language models entirely offline, ensuring privacy and control over your AI interactions. ([GitHub - Pyenb/Ollama-models: A collection of zipped Ollama models for ...](https://github.com/Pyenb/Ollama-models?utm_source=chatgpt.com))

---

## 🛠️ Prerequisites

Ensure the following are installed on your system:

- **Docker Desktop**: Required to run Open WebUI in a containerized environment. ([Open WebUI Docker — Framework Repositories 1.0 documentation](https://frameworks.readthedocs.io/en/latest/ai/openWebuiDocker.html?utm_source=chatgpt.com))

- **Ollama**: Used to download and manage open-weight language models locally. ([Running large language models locally using Ollama - Blogger](https://bartwullems.blogspot.com/2024/04/running-large-language-models-locally.html?utm_source=chatgpt.com))

---

## 📥 Step 1: Install Ollama

Download and install Ollama from the official website: ([Step-by-Step Guide - How to use Ollama to run open-source LLM models ...](https://www.langchain.ca/blog/step-by-step-guide-how-to-use-ollama-to-run-open-source-llm-models-locally/?utm_source=chatgpt.com))

👉 [https://ollama.com](https://ollama.com)

Follow the installation instructions provided for your operating system.

---

## 📦 Step 2: Download a Language Model

Use Ollama to download the desired language model. For this setup, we'll use the `deepseek-coder-v2` model. ([library - Ollama](https://ollama.com/library?sort=popular&utm_source=chatgpt.com))

```bash
ollama pull deepseek-coder-v2
```


This command downloads the model and prepares it for local use.

---

## 🐳 Step 3: Install Docker Desktop

If you haven't already, install Docker Desktop from the official website:

👉 [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)

After installation, ensure Docker Desktop is running properly. ([Installing Docker | Open WebUI](https://docs.openwebui.com/tutorials/docker-install/?utm_source=chatgpt.com))

---

## 🚀 Step 4: Run Open WebUI

Open WebUI provides a user-friendly interface to interact with your local language models.

### Pull the Open WebUI Docker Image

Use the following command to pull the latest Open WebUI Docker image: ([⏱️ Quick Start | Open WebUI](https://docs.openwebui.com/getting-started/quick-start/?utm_source=chatgpt.com))

```bash
docker pull ghcr.io/open-webui/open-webui:main
```


### Run the Open WebUI Container

Start the Open WebUI container with the following command:

```bash
docker run -d \
  -p 3000:8080 \
  -v open-webui:/app/backend/data \
  --name open-webui \
  --restart always \
  ghcr.io/open-webui/open-webui:main
```


This command maps port 8080 of the container to port 3000 on your host machine and ensures data persistence. ([Anuraj - Running Open Web UI locally with Ollama - anuraj.github.io](https://anuraj.dev/blog/running-open-webui-locally-with-ollama/?utm_source=chatgpt.com))

---

## 💬 Step 5: Access the Chat Interface

Once the Open WebUI container is running, access the chat interface by navigating to:

👉 [http://localhost:3000](http://localhost:3000)

You can now interact with the `deepseek-coder-v2` model through the web interface. ([library - Ollama](https://ollama.com/library?sort=popular&utm_source=chatgpt.com))

---

## 🔄 Optional: Run Ollama in a Docker Container

If you prefer to run Ollama within a Docker container, you can set it up alongside Open WebUI using Docker Compose.

### Create a `docker-compose.yml` File

Create a `docker-compose.yml` file with the following content:

```yaml
version: '3'
services:
  ollama:
    image: ollama/ollama
    container_name: ollama
    volumes:
      - ollama:/root/.ollama
    restart: unless-stopped

  open-webui:
    image: ghcr.io/open-webui/open-webui:main
    container_name: open-webui
    ports:
      - "3000:8080"
    volumes:
      - open-webui:/app/backend/data
    depends_on:
      - ollama
    restart: unless-stopped

volumes:
  ollama:
  open-webui:
```


### Start the Services

Run the following command to start both services: ([How to setup Open WebUI with Ollama and Docker Desktop](https://dev.to/ajeetraina/how-to-setup-open-webui-with-ollama-and-docker-desktop-24f0?utm_source=chatgpt.com))

```bash
docker-compose up -d
```


This setup allows both Ollama and Open WebUI to run in separate containers, facilitating better management and isolation.

---

## 🧪 Testing the Setup

To verify that everything is working correctly:

1. Ensure both Docker containers (`ollama` and `open-webui`) are running: ([How to setup Open WebUI with Ollama and Docker Desktop](https://dev.to/ajeetraina/how-to-setup-open-webui-with-ollama-and-docker-desktop-24f0?utm_source=chatgpt.com))

   ```bash
   docker ps
   ```


2. Access the Open WebUI interface at [http://localhost:3000](http://localhost:3000).

3. Initiate a chat session and interact with the `deepseek-coder-v2` model. ([library - Ollama](https://ollama.com/library?sort=popular&utm_source=chatgpt.com))

---

## 📚 Additional Resources

- **Ollama Documentation**: [https://ollama.com](https://ollama.com) ([library - Ollama](https://ollama.com/library?sort=popular&utm_source=chatgpt.com))

- **Open WebUI Documentation**: [https://docs.openwebui.com](https://docs.openwebui.com)

- **Docker Desktop**: [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)

---

This setup provides a robust, local environment for interacting with open-weight language models, ensuring privacy and control over your AI applications.

--- 
