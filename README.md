# Ollama-GPU-on-Windows-using-Docker

This guide explains how to run Ollama with GPU support inside Docker on Windows and how to install and use AI models inside the container.

---

## 1. Pull Ollama Docker Image

```sh
docker pull ollama/ollama:latest
2. Start the Ollama Container with GPU
sh
Copy code
docker run -d --name ollama-gpu ^
  --gpus=all ^
  -v ollama-data:/root/.ollama ^
  -p 11434:11434 ^
  ollama/ollama:latest
This will start Ollama and make the API available on:

arduino
Copy code
http://localhost:11434
3. Enter the running container
sh
Copy code
docker exec -it ollama-gpu bash
4. Pull a model inside the container
Replace <model> with the model name you want (examples: deepseek-r1, llama3, mistral, qwen2.5)

sh
Copy code
ollama pull <model>
Example:

sh
Copy code
ollama pull deepseek-r1
5. Check installed models
sh
Copy code
ollama list
6. Run a model
sh
Copy code
ollama run <model>
Example:

sh
Copy code
ollama run deepseek-r1
7. Test using curl from Windows (outside the container)
sh
Copy code
curl http://localhost:11434/api/generate -d "{
  \"model\": \"deepseek-r1\",
  \"prompt\": \"Hello, how are you?\"
}"
8. Stop / Start the container
Stop:

sh
Copy code
docker stop ollama-gpu
Start again:

sh
Copy code
docker start ollama-gpu
Data is preserved automatically because of the Docker volume:

bash
Copy code
-v ollama-data:/root/.ollama
Notes
Component	Status
GPU	enabled via --gpus=all
Model storage	persistent using Docker volume
API	exposed on port 11434

Useful Commands Summary
Task	Command
Enter container	docker exec -it ollama-gpu bash
List models	ollama list
Pull model	ollama pull <model>
Run model	ollama run <model>

Example of multiple models installation
sh
Copy code
ollama pull deepseek-r1
ollama pull llama3
ollama pull mistral
You're done — Ollama with GPU is running on Windows inside Docker. 🚀

yaml
Copy code

---

If you want, I can also create:

🔹 `docker-compose.yml` version  
🔹 README with screenshots  
🔹 a **script that auto-installs models on first run**

Just tell me. 💪
