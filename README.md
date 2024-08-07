# example
There are 2 simple applications doing similar thing. One is written in NodeJS and another in Golang.

Both require working Redis server to keep session & timestamp.


## Installation ##

## hello-1 ##

```
npm install express
npm install redis

export port=redis_port
export host=redis_host
export password=redis_password

node hello1/hello-1.js
```

## hello-2 ##

```
cd hello2

go mod download

export REDIS_HOST="localhost:6379"
export REDIS_PASSWORD="password"
export REDIS_DB="0"

go run main.go
```

# Hello App Deployment

This repository contains the code and configurations to deploy two services (`hello-1` and `hello-2`) using Docker and Kubernetes. The services interact with Redis for session management.

## Prerequisites

- Docker
- Kubernetes cluster
- kubectl configured to interact with the cluster
- DockerHub account
- GitHub repository for storing the code and actions

## Steps to Deploy

### 1. Build Docker Images (CI)


a. Manaully build, navigate to the root directory of each service and build the Docker images:

```bash
cd hello-1
docker build -t pepoolife/hello-1:latest .

cd ../hello-2
docker build -t pepoolife/hello-2:latest .
```

b. Autobuild by Github action, once commit new code to main branch, the build process will tricker.

### 2. Deploy process (CD)

a. Export Git repo and Token
```bash
export GIT_REPO=https://github.com/pepoolife/argopilot.git
export GIT_TOKEN=ghp_xxx
```

b. execute command to install Argopilot
```bash
argocd-autopilot repo bootstrap 
```