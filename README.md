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

### Get Bot ID
```
docker exec -it $(docker ps --format "{{.Names}}" | grep "mattermost" | head -n 1) mmctl --local bot list --json | jq '.[] | select(.username=="<bot-name>") | .user_id'
```

### Get User ID
```
docker exec -it $(docker ps --format "{{.Names}}" | grep "mattermost" | head -n 1) mmctl --local user search <EMAIL_ADDRESS>
```

### Add Bot to a team
```
docker exec -it $(docker ps --format "{{.Names}}" | grep "mattermost" | head -n 1) mmctl --local team users add <team> <bot-username>
```

### Create Private Channel with User and Bot, and get Channel ID
```
docker exec -it $(docker ps --format "{{.Names}}" | grep "mattermost" | head -n 1) mmctl --local channel create --team "bob1" --name "caas-user01" --display-name "Claw-as-a-Service - User01" --private

docker exec -it $(docker ps --format "{{.Names}}" | grep "mattermost" | head -n 1) mmctl --local channel users add bob1:caas-user01 user01

docker exec -it $(docker ps --format "{{.Names}}" | grep "mattermost" | head -n 1) mmctl --local channel users add bob1:caas-user01 bob1-claw-01
```

### Search for Channel
```
docker exec -it $(docker ps --format "{{.Names}}" | grep "mattermost" | head -n 1) mmctl channel search --team <team-name> <channel-name>
```
