# Docker

# Check Version

`docker --version`
`docker version`
`docker info`

# Image Management

- `docker images`
- `docker image ls`

# Pull Image

- `docker pull nginx`
- `docker pull image nginx:latest`

# Remove Images

`docker rmi nginx`
`docker image rm nginx`
`docker image rm -f nginx`

# Inspect Image

`docker inspect nginx`
`docker image inspect nginx`

# Image History (Layers)

`docker history nginx`

# Tag Image

`docker tag nginx myrepo/nginx:v1`

# build Image

`docker build -t myapp .`
`docker build -f Dockerfile.prod -t myapp:prod .`

# Save / Load Images (Offline transfer)

`docker save nginx > nginx.tar`
`docker load < nginx.tar`

# Container Lifecycle (Core)

# Run Container

`docker run nginx`
`docker run -d nginx`
`docker run -it ubuntu bash`
`docker run --name web nginx`

# List Containers

`docker ps`
`docker ps -a`
`docker container ls`

# Stop / Start / Restart

`docker stop web`
`docker start web`
`docker restart web`

# Remove Containers

`docker rm web`
`docker rm -f web`
`docker container prune`

# Inspect container

`docker inspect web`

# Logs

`docker logs web`
`docker logs -f web`

# Execute Inside Container

`docker exec -it web bash`
`docker exec web ls`

# Attach to Container

`docker attach web`

# List Networks

`docker network ls`

# Create Network

`docker network create mynet`

# Inspect Network

`docker network inspect mynet`

# Connect Container

`docker network connect mynet web`

# Remove Network

`docker network rm mynet`
`docker network prune`

# PART 5 — Volume & Storage

# List Volumes

`docker volume ls`

# Create Volume

`docker volume create myvol`

# Inspect Volume

`docker volume inspect myvol`

# Use Volume

`docker run -v myvol:/data nginx`
`docker run -v $(pwd):/app nginx`

# Remove Volumes

`docker volume rm myvol`
`docker volume prune`

# PART 6 — Resource Management

# Stats (Real-time CPU/MEM)

`docker stats`

# Limit Resources

`docker run -m 512m --cpus="1.5" nginx`

# Disk Usage

`docker system df`

# System Cleanup

`docker system prune`
`docker system prune -a`

# PART 7 — Docker Registry (Push/Pull Pro)

# Login

`docker login`
`docker login myregistry.com`

# Push Image

`docker push myrepo/myapp:v1`

# Logout

`docker logout`

# PART 8 — Debugging & Troubleshooting

# Top (Processes inside container)

`docker top web`

# Events (Live system events)

`docker events`

# Diff (File changes)

`docker diff web`

# Port Mapping

`docker port web`

# PART 9 — Docker Compose (Industry Mandatory)

# Start Services

`docker compose up`
`docker compose up -d`

# Stop

`docker compose down`

# Build

`docker compose build`

# Logs

`docker compose logs`

# Execute

`docker compose exec app bash`

# PART 10 — Swarm & Orchestration

# Init Swarm

`docker swarm init`

# Nodes

`docker node ls`

# Services

`docker service ls`
`docker service create nginx`
`docker service scale web=5`

# PART 11 — Security & Secrets

# Secrets

`docker secret create db_pass file.txt`
`docker secret ls`
`docker secret rm db_pass`

# Configs

`docker config create app_conf conf.txt`
`docker config ls`

# PART 12 — Advanced Build (Pro Level)

# Multi-stage Build

'''
FROM node AS build
FROM nginx

Build Cache
docker build --no-cache .

Build Platform
docker buildx build --platform linux/amd64 .
'''

# PART 13 — Hidden Pro Commands

Command. | Purpose
docker cp Copy files
docker rename Rename container
docker pause Freeze container
docker unpause Resume
docker wait Wait for exit
docker export Export FS
docker import Import FS
docker commit Snapshot container

# PART 14 — The Nuclear Cleanup

`docker kill $(docker ps -q)`
`docker rm $(docker ps -aq)`
`docker rmi $(docker images -q)`
`docker volume rm $(docker volume ls -q)`

The Real Industry Truth

In real DevOps life, 95% of your work uses only these 25 commands:

run
ps
logs
exec
build
pull
push
rm
rmi
inspect
stats
system df
system prune
network ls
volume ls
compose up
compose down

Everything else is situational power.
