# Ollama-GPU-on-Windows-using-Docker

This guide explains how to run **Ollama with GPU support inside Docker on Windows**, install AI models, and execute them through the container.

---

## ✔ Prerequisites
Before starting, ensure that the following are installed and working:
- Windows 10 / 11
- Docker Desktop with WSL2 backend enabled
- NVIDIA GPU + CUDA drivers
- NVIDIA Container Toolkit (Docker automatically detects GPU)

---

## 🔹 1. Pull Ollama Docker Image
```bash
docker pull ollama/ollama:latest
🔹 2. Start Ollama Container with GPU
bash
Copy code
docker run -d --name ollama-gpu ^
  --gpus=all ^
  -v ollama-data:/root/.ollama ^
  -p 11434:11434 ^
  ollama/ollama:latest
If started successfully, the API will be available at:

arduino
Copy code
http://localhost:11434
🔹 3. Enter the Running Container
bash
Copy code
docker exec -it ollama-gpu bash
🔹 4. Pull an AI Model
Replace <model> with the model you want (e.g., deepseek-r1, mistral, llama3).

bash
Copy code
ollama pull <model>
Example:

bash
Copy code
ollama pull deepseek-r1
🔹 5. Check Installed Models
bash
Copy code
ollama list
🔹 6. Run a Model
bash
Copy code
ollama run <model>
Example:

bash
Copy code
ollama run deepseek-r1
🔹 7. Stop or Remove the Container (Optional)
Stop container:

bash
Copy code
docker stop ollama-gpu
Start container again:

bash
Copy code
docker start ollama-gpu
Remove container:

bash
Copy code
docker rm -f ollama-gpu
📌 Notes
Models are stored persistently in the Docker volume ollama-data.

GPU must be detected by Docker — run docker info and verify NVIDIA is listed.

🎉 Done!
You now have Ollama with GPU running on Windows via Docker and can install/run any AI model inside the container.
