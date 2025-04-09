# AI chat using model hosted in local Ollama

[![Java CI with Gradle](https://github.com/andrei-punko/ai-chat-ollama/actions/workflows/gradle.yml/badge.svg)](https://github.com/andrei-punko/ai-chat-ollama/actions/workflows/gradle.yml)

## Requirements
- JDK 21
- Gradle isn't required because of embedded Gradle in the project
- Ollama (install locally or use it inside Docker container)
- Docker (recommended)
- NVIDIA GPU (recommended) (checked on GeForce RTX 3060 12Gb)

## Commands to communicate with Ollama inside Docker container

According to [instruction](https://ollama.com/blog/ollama-is-now-available-as-an-official-docker-image)

### Run Ollama inside a Docker container (using CPU)
```bash
docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```

### Run Ollama inside a Docker container (using NVIDIA GPU)
```bash
docker run -d --gpus=all -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```

### Pull an AI model into Docker container
```bash
docker exec -it ollama ollama pull gemma3:4b
```

### List Ollama models inside Docker container
```bash
docker exec -it ollama ollama list
```

## How to build application
```bash
./gradlew clean build
```

## How to start application

```bash
java -jar build/libs/ai-chat-ollama-0.0.1-SNAPSHOT.jar
```
or use [run.bat](run.bat) script

## How to ask question to AI

Send GET request to endpoint exposed by service with message inside `message` request param:
```
http://localhost:8090/ai/generate?message=<your-message>
```

For example:
```bash
curl -i -X POST http://localhost:8090/ai/generate?message=tell%20me%20about%20Belarus
```

```bash
curl -i http://localhost:8090/ai/generate?message=describe%20primitive%20types%20in%20Java
```
