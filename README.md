# mattermost-docker
Docker Compose setup for Mattermost

## Setup

1. Run the following commands after cloning the project. 

```
cp env.example .env

mkdir -p ./volumes/app/mattermost/{config,data,logs,plugins,client/plugins,bleve-indexes}

sudo chown -R 2000:2000 ./volumes/app/mattermost

docker compose -f docker-compose.yml -f docker-compose.without-nginx.yml up -d
```

## Using Mattermost

### Create new user
```
docker exec -it $(docker ps --format "{{.Names}}" | grep "mattermost" | head -n 1) mmctl --local user create --email <EMAIL_ADDRESS> --username <USERNAME> --password '<PASSWORD>'
```

### Delete user
```
docker exec -it $(docker ps --format "{{.Names}}" | grep "mattermost" | head -n 1) mmctl --local user delete <EMAIL_ADDRESS>
```


### Get User ID
```
docker exec -it $(docker ps --format "{{.Names}}" | grep "mattermost" | head -n 1) mmctl --local user search <EMAIL_ADDRESS>
```

