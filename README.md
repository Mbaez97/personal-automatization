# personal-automatization

This repository contains the necessary configuration to run N8N service with Ollama, everything on your local machine.

## Prerequisites

- Docker installed on your machine
- Docker Compose installed on your machine
- (Optional) NVIDIA GPU support: Install the NVIDIA driver for your card and the [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html) so Docker can expose the GPU to containers

## Services

This setup includes two services:

- **n8n**: Workflow automation tool (accessible at http://localhost:5678)
- **Ollama**: Local LLM service (accessible at http://localhost:11434)

## Quick Start

### Starting the Services

To start both n8n and Ollama services, run:

```bash
docker compose up -d
```

The `-d` flag runs the containers in detached mode (in the background).

> **Note**: If you're using an older version of Docker, you may need to use `docker-compose` (with a hyphen) instead of `docker compose`.

### Stopping the Services

To stop the services:

```bash
docker compose down
```

To stop the services and remove volumes (this will delete all data):

```bash
docker compose down -v
```

### Viewing Logs

To view logs from all services:

```bash
docker compose logs -f
```

To view logs from a specific service:

```bash
docker compose logs -f n8n
# or
docker compose logs -f ollama
```

## GPU Acceleration

The `ollama` service is preconfigured to request NVIDIA GPUs via Docker Compose. Once the NVIDIA Container Toolkit is installed, starting the stack with `docker compose up -d` will automatically pass through all available GPUs to the container.

To verify GPU access:

```bash
docker exec -it ollama nvidia-smi
```

If the command prints the usual `nvidia-smi` table, the GPU is available to Ollama. If you see an error, double-check that your NVIDIA driver and the Container Toolkit are correctly installed.

## Volumes

The following volumes are configured for data persistence:

- **n8n_data**: Stores n8n workflows, credentials, and configuration
- **ollama_data**: Stores Ollama models and configuration

## Accessing the Services

- **n8n Web UI**: Open your browser and navigate to http://localhost:5678
- **Ollama API**: Available at http://localhost:11434

## Using Ollama

After starting the services, you can pull models using:

```bash
docker exec -it ollama ollama pull llama2
```

Or any other model available in the Ollama library.
