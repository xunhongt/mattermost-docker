# mattermost-docker
Docker Compose setup for Mattermost

## Setup

1. Run the following commands after cloning the project. 

```
cp ./docker/env.example .docker/.env

mkdir -p ./docker/volumes/app/mattermost/{config,data,logs,plugins,client/plugins,bleve-indexes}

sudo chown -R 2000:2000 ./volumes/app/mattermost

docker compose -f docker/docker-compose.yml -f docker/docker-compose.without-nginx.yml up -d
```
