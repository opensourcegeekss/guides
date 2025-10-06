# Offline ollama using open web-ui -

```bash
# Install necesarry packages
sudo dnf install podman -y

# Pull ollama image from dockerhub
podman pull ollama/ollama
mkdir -p ollama

# Run podman ollama image
podman run \
--name ollama \
--rm \
--detach \
--privileged \
-p 11434:11434 \
-v $PWD/ollama:/root/.ollama \
ollama/ollama

# Check logs of ollama
podman logs -f ollama

# Set alias
alias ollama='podman exec ollama ollama'

# Pull deepseek r1 1.5b model
ollama pull deepseek-r1:1.5b

# Pull opwn-webui image from ghcr.io
podman pull ghcr.io/open-webui/open-webui:main

# Run open-webui image
podman run \
--rm \
--network host \
-p 8080:8080 \
-e WEBUI_AUTH=false \
-e OLLAMA_BASE_URL=http://127.0.0.1:11434 \
--name openwebui \
ghcr.io/open-webui/open-webui:main

# Open browser and visit,
# sometimes it take 2-3 mins to up
http://127.0.0.1:8080/
```



