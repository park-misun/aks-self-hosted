# az-devops-k8s-agent
Self-Hosted Azure Devops Agent for kubernetes

## docker connection test (by local console)
docker run -d -p 80:80 docker/getting-started 

## 1. Create Docker Base & Golden Image 
### 01. build base image
(https://docs.microsoft.com/ko-kr/azure/devops/pipelines/agents/docker?view=azure-devops)

        docker image build -t agentbaseimage .
        
        docker image build -t <acr url>/<image name> .(Dockerfile)


### 02. build golden image (java, python, .net)
        (install & set env param)
        
        
## 2. Config AKS
### 01. create namespace for sh agent
       kubectl create namespace <insert-namespace-name-here>
### 02. AKS deoployment agent)
        (Env. Parameter)
        . AZP_URL=<DevOps URL>
        . AZP_TOKEN=<Token>
        . AZP_AGENT_NAME=<AgentName>
        . AZP_POOL=<PoolName> 
        
        kubectl create secret generic azdevops --from-literal=AZP_URL=<URL> --from-literal=AZP_TOKEN=<Token> --from-literal=AZP_POOL=<PoolName> -n azure-devops-agents
        
        
## Setup via pre-built image
Docker Image : shubhamranjan/az-devops-k8s-agent:latest

1. Modify `sample/create_secret.sh` with the required Azure Devops Organisation URL, PAT and Agent Pool Name.

2. Run the script or the command directly in the required namespace.

        sh ./sample/create_secret.sh

3. Apply `sample/deployment.yml` after making any required changes like namespace (if modified in the previous step).

        kubectl apply -f sample/deployment.yml
