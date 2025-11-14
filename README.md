# Ollama GPU on Windows using Docker

This guide explains how to run **Ollama with GPU support inside Docker on Windows**, install AI models, and execute them inside the container.

## Prerequisites
Make sure the following are installed and configured:
- Windows 10 / 11
- Docker Desktop (WSL2 backend enabled)
- NVIDIA GPU with CUDA drivers
- NVIDIA Container Toolkit (Docker must detect GPU)

---

## 1. Pull Ollama Docker Image
```bash
docker pull ollama/ollama:latest
2. Start Ollama Container with GPU Support
bash
Copy code
docker run -d --name ollama-gpu ^
  --gpus=all ^
  -v ollama-data:/root/.ollama ^
  -p 11434:11434 ^
  ollama/ollama:latest
When running, the Ollama API will be available at:

arduino
Copy code
http://localhost:11434
3. Enter the Running Container
bash
Copy code
docker exec -it ollama-gpu bash
4. Pull an AI Model
Replace <model> with any available model (example: deepseek-r1, mistral, llama3).

bash
Copy code
ollama pull <model>
Example:

bash
Copy code
ollama pull deepseek-r1
5. List Installed Models
bash
Copy code
ollama list
6. Run a Model
bash
Copy code
ollama run <model>
Example:

bash
Copy code
ollama run deepseek-r1
Optional Docker Commands
Stop the container:

bash
Copy code
docker stop ollama-gpu
Start the container again:

bash
Copy code
docker start ollama-gpu
Remove the container:

bash
Copy code
docker rm -f ollama-gpu
Notes
All downloaded models are stored in the Docker volume ollama-data, so they persist even if the container is removed.

To verify GPU access inside container, run:

bash
Copy code
nvidia-smi
