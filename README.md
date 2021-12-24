# Infrastructure

## Table of Contents

- [Setup](#setup)
  - [Install Docker](#install-docker)
  - [Install Docker Compose](#install-docker-compose)
  - [Setup SSH](#setup-ssh)
  - [Login to the GitHub Container Registry](#login-to-the-github-container-registry)
  - [Clone the Repository](#clone-the-repository)
  - [Start Docker Compose](#start-docker-compose)

## Setup

### Install Docker

```shell
sh <(curl -fsSL https://get.docker.com)
```

### Install Docker Compose

```shell
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

### Setup SSH

Copy the generated public key and add it as a deploy key: https://github.com/{{your-github-username-here}}/{{your-github-repository-name-here}}/settings/keys

```shell
ssh-keygen -t ed25519 -f ~/.ssh/github -N ''
printf "Host github.com\n\tIdentityFile ~/.ssh/github\n" >> ~/.ssh/config
cat ~/.ssh/github.pub
```

### Login to the GitHub Container Registry

Generate a new personal access token: https://github.com/settings/tokens

```shell
docker login ghcr.io -u {{your-github-username-here}}
```

### Clone the Repository

```shell
git clone git@github.com:{{your-github-username-here}}/{{your-github-repository-name-here}}.git
```

### Start Docker Compose

```shell
cd {{your-github-repository-name-here}}
mkdir -p ./data/letsencrypt
docker-compose up -d && docker-compose logs
```
