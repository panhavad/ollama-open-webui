# ollama-open-webui
This is the docker compose of ollama, and open webui.
Create docker-compose.yml
```
version: '3.8'

services:
  open-webui:
    image: ghcr.io/open-webui/open-webui:cuda
    container_name: open-webui
    restart: always
    ports:
      - "3000:8080"
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: all
              capabilities: [gpu]
    volumes:
      - D:/Docker/Volumes/open-webui:/app/backend/data
    extra_hosts:
      - "host.docker.internal:host-gateway"

  ollama:
    image: ollama/ollama
    container_name: ollama
    restart: always
    ports:
      - "11434:11434"
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: all
              capabilities: [gpu]
    volumes:
      - D:/Docker/Volumes/ollama:/root/.ollama

volumes:
  open-webui:
  ollama:
```

When you want to install model in ollama.
Access to ollama docker and pull model you like as below:
```
docker exec -it ollama /bin/ollama pull deepseek-coder-v2:16b
```
Done.
Access open webui from `localhost:3000`
