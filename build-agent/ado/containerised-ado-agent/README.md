# Build and run ado agent in a container

```bash
docker build --tag azp-agent:linux .\build-agent\ado\containerised-ado-agent\

docker run -e AZP_URL="<Azure DevOps instance>" -e AZP_TOKEN="<Personal Access Token>" -e AZP_POOL="<Agent Pool Name>" -e AZP_AGENT_NAME="Docker Agent - Linux" --name "azp-agent-linux" azp-agent:linux
```
