# Docker

That’s a **great and fundamental question** — and one every DevOps engineer or developer needs to understand deeply.
Let’s break it down from **basic → real-world → industry-level** so you’ll never forget it. 🚀

---

## 🧩 The Simple Answer:

> You use **Docker** not because EC2 can’t run your app,
> but because **Docker makes it predictable, portable, and scalable** — across any environment (your laptop, EC2, ECS, EKS, etc.).

---

## 🧠 1. Without Docker — What Happens?

If you directly host your app on an EC2 instance:

- You must install dependencies manually (`node`, `python`, `nginx`, etc.)
- Environment may differ between instances
- Hard to replicate same setup (dev/staging/prod)
- Deployment takes longer (rebuilding from scratch)
- Hard to rollback if something breaks
- Scaling means repeating setup on every instance

### 🧍Example:

Let’s say you deploy a Node.js app on EC2:

```bash
sudo yum install nodejs
npm install
npm start
```

Now you must repeat all this for staging, production, or new servers — and risk version mismatches (Node v14 vs v18, etc.).
This leads to _“it works on my machine”_ problems 😅

---

## 🐳 2. With Docker — What Changes?

With Docker, you **package your app + dependencies + OS libraries** into one **image**.
Then you can run that **same image anywhere** — EC2, ECS, EKS, or even your laptop.

### 🧱 Example:

You create a Dockerfile:

```Dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "start"]
```

Now build and run:

```bash
docker build -t my-node-app .
docker run -p 80:3000 my-node-app
```

✅ This runs **exactly the same way** on any EC2, ECS, or even in your colleague’s system.

---

## ⚙️ 3. Real-World Example (Industry)

Imagine you have a **4-tier application**:

- React Frontend
- Node.js Backend
- Redis Cache
- MySQL Database

If you deploy this manually on EC2s:

- You’ll configure 4 EC2 instances separately
- Install everything manually
- Manage dependencies & updates separately
- Hard to scale or migrate

With Docker:

- You containerize each service → 4 containers
- Define them in `docker-compose.yml`
- Deploy anywhere (ECS, EKS, or even local machine) with **no setup issues**

---

## ⚡ 4. Key Advantages of Docker over Plain EC2

| Feature                     | Without Docker                        | With Docker                           |
| --------------------------- | ------------------------------------- | ------------------------------------- |
| **Environment consistency** | Manual setup differs across instances | Same image everywhere                 |
| **Deployment speed**        | Manual or scripts                     | Just pull & run image                 |
| **Scaling**                 | Slow & error-prone                    | Fast with ECS/K8s                     |
| **Rollback**                | Hard                                  | Easy (use older image tag)            |
| **Portability**             | EC2 only                              | EC2, ECS, EKS, Fargate, any cloud     |
| **Isolation**               | One app per EC2                       | Multiple apps per instance (isolated) |
| **Automation**              | Partial                               | Full CI/CD ready                      |

---

## 🏭 5. Industry-Standard Workflow (EC2 + Docker)

In companies, EC2 + Docker are often used **together**, not instead of each other.

Here’s how:

1. Build Docker image locally or via CI/CD (GitHub Actions, Jenkins)
2. Push image to **Amazon ECR**
3. ECS (with EC2 launch type) pulls the image from ECR
4. EC2 runs the container inside Docker

So EC2 becomes a **container host**, not a manually configured app server.

---

## 🔍 6. Analogy (in DevOps terms)

| Concept     | Without Docker                    | With Docker                       |
| ----------- | --------------------------------- | --------------------------------- |
| **EC2**     | A raw VM (like bare metal server) | Acts as a container host          |
| **Docker**  | Not used, app tied to VM          | Encapsulates app in container     |
| **Scaling** | Need to configure new EC2         | ECS/EKS can auto-scale containers |
| **CI/CD**   | Harder                            | Standardized with image tags      |

---

## 🚀 7. Summary

| Reason      | Why Docker Helps                        |
| ----------- | --------------------------------------- |
| Consistency | Same runtime everywhere                 |
| Isolation   | Keeps apps separated on same EC2        |
| Portability | Run anywhere (AWS, Azure, GCP, On-prem) |
| Speed       | Fast build, deploy, rollback            |
| Scalability | Works natively with ECS/EKS             |
| Efficiency  | Run multiple apps per EC2 instance      |

---

### 🔧 Final Thought:

> **Docker doesn’t replace EC2 — it makes EC2 better.**
>
> EC2 gives you the compute power,
> Docker gives you the consistency, portability, and scalability to actually use that power efficiently.

---

Would you like me to show you a **real-world comparison** — same app deployed once **directly on EC2** and once **using Docker on EC2** — to see the operational difference step-by-step?

## Basic Commands

---

### Docker Run

- `docker run <image>` is used to run a docker container from an Image
- Running the docker run nginix will run the instance of nginix application on the docker host if it already exist. if the image not present on the host it will go to docker hub and pull the image down but this is only done for the first time.

---

### Docker ps

- `docker ps` command will list all the running containers and some basic info about the like container id, name, image
- `docker ps -a` all running as well as previously stopped.

---

### Docker Stop

- `docker stop <containerId>` used to stop the container

---

### Docker rm

- `docker rm <containerId/containerName>` will remove the stopped container from memory.

---

### Docker Images

- `docker images` is used to list all the images presentes in the host.

---

### Docker rmi

- `docker rmi <image>` is used to remove the image from the host

---

### Docker pull

- `docker pull <image>` will pull the image from registry and stores the image.

---

### Exec

- To run a command in a running container we use Exec command
- `docker exec <containerId> <command_to_run_in_the_container>`

---

## Port Mapping

- Basically let say the container IP is 10.5.6.8 and this container has an application listening to port 8080.
- We can access the container with its IP only inside the host. So to access it from out side we can use the Host IP.
- let say it as 172.286,43.56 and we have to port map a free port let say 80 in the host to the application listen post
- `docker run -d -p 80:8080 mysql`

---

## Volume Mapping

- Let say you host a mysql inside the container.
- All the data you store in the db is stored in side the container. so if the container is destroyed the data is lost.
- So we use data mapping, and map data to a directory outside the container.
- `docker run -v /opt/datadir: /var/lib/mysql mysql`

---

## Docker Inspect

- To get more info about the docker container we use `docker inspect <container>`

---

## Docker Logs

- To get logs we use `docker log <containerName>`

---

## Build Docker file

- Let say that file name is "Dockerfile" so `docker build .` or if we want tag `docker build . -t my-app:1.0`
- If the name is other than Dockerfile then `docker build -f my-docker-file -t my-app:1.0`

---

## Example docker file

```t
FROM ubuntu
RUN apt-get update -y
RUN apt-get install  python3 -y && \
    apt-get install  python3-pip && \
    apt-get install python3-venv -y
RUN python3 -m venv /opt/venv/ && \
    /opt/venv/bin/pip install --upgrade pip && \
    /opt/venv/bin/pip install flask
copy app.py /opt/app.py
ENV PATH="/opt/venv/bin:$PATH"
ENV FLASK_APP=/opt/app.py

```

---

## Docker Environmental variables

- `docker run -e <NameOfVariable>=<value> <imageName>`

---

## Docker CMD && EntryPoint

| Feature          | `CMD`                                        | `ENTRYPOINT`                                            |
| ---------------- | -------------------------------------------- | ------------------------------------------------------- |
| **Purpose**      | Sets **default arguments**                   | Sets the **main command** to run                        |
| **Overridable?** | ✅ Yes — `docker run <override>` replaces it | 🚫 Not easily overridable (unless using `--entrypoint`) |
| **Used for**     | Arguments passed to a default program        | Defining the actual program to run                      |

Imagine:
You’re ordering a pizza.

ENTRYPOINT = Pizza shop (always used to make the pizza)

CMD = Default toppings (you can change them if you want)

```t
ENTRYPOINT ["pizza-maker"]
CMD ["cheese", "tomato"]

```

This makes a cheese + tomato pizza by default.

But you can change toppings like this:

```t
`docker run my-pizza chicken olives`

```

- Simply let say that we want a command that is constant and have to execute on start so will have it in ENTRYPOINT.
- And the command that is dynamic will be in CMD.

```t
ENTRYPOINT ["sleep"]
CMD [10]

```

- Here the sleep wont change but the time can be overriden using `docker run my-img <timeYouWant>`

---

## Docker Compose

- REPO : - `https://github.com/docker/awesome-compose`

- Docker Compose is a configuration file written in YAML.
- It is mixture of different docker files
- Let say you have 3 tier application and 3 docker file instead of running them individually we can manage those three configs into a single file and manage the single file that file in Docker Compose File.

```t

Example Docker-compose:

redis:
    image: redis

vote-app:
    image: vote-app
    ports:
        8080:80
    links:
        -redis:redis

```

But there are some limitions in above version-1 so we have version-2 below

- In version-2 we dont need link because in v2 the docker create a specific bridge n/w and attach the containers to it, so they will communicat directly with their host name.

```t

service:
    redis:
        image: redis
        networks:
            - back-end

    vote-app:
        image: vote-app
        ports:
            8080:80
        depends_on: # This indicated that first redis container have to start before vote-app container
            redis
        networks:
            - front-end
            - back-end
netwroks:
    front-end:
    back-end:

```

---

## Link Command

- `docker run -d --name=xyz --link def:ghi abc`

| Part             | Meaning                                                                                                             |
| ---------------- | ------------------------------------------------------------------------------------------------------------------- |
| `docker run`     | Start a new Docker container                                                                                        |
| `-d`             | Run in **detached mode** (in the background)                                                                        |
| `--name=xyz`     | Give the new container the name **`xyz`**                                                                           |
| `--link def:ghi` | Link the new container to an **existing container named `def`**, and **alias it as `ghi`** inside the new container |
| `abc`            | The Docker **image** to use for creating the container                                                              |

---

## Docker Engine

Docker Engine is the core software that runs Docker. It's a client-server application that allows you to build, run, and manage containers on your machine.

You can think of Docker Engine as the "brain" and "muscle" behind everything Docker does.

⚙️ Docker Engine Architecture
It has three main components:

Component Role
1️⃣ Docker Daemon (dockerd) The background service that actually creates, runs, and manages containers
2️⃣ Docker Client (docker) The command-line interface (CLI) you use to talk to the Docker Daemon
3️⃣ REST API A programmatic way for tools and apps to interact with Docker (what the CLI uses internally)

---

## Docker Volumes

- Docker to maintain data persistend it used volumes
- `docker volume ls` - to list vaolumes
- `docker volume rm <volID` - to remove volume
- `docker volume prune` - remove all the left over volumes that are not in use
- `docker volume create my-vol`
- `docker run -v myvol:var/lib/mysql mysql`
- New Version `docker run --mount source= my-vol target=var/lib/mysql mysql`
- `docker run -it --name myserver --mount source=<volume> destination=<mountPoint> <container>`

## Docker Namespace

- To create isolation b/w containers we use Namespaces in docker

## Docker Layer archetecture

- To facilitate sharing and modifing we use Layer Architecture

## Docker CGroups

- To manage resources we use cgroups(control groups)

## Docker N/W

- `docker network ls` - to list all n/w's
- `docker network inspect bridge` - inspect the bridge n/w

- There are three types of n/w
  1. bridge
  2. host
  3. none
  4. overlay

1. bridge

```t
docker network create my-bridge
docker run -d --name frontend --network my-bridge frontend-image
docker run -d --name backend --network my-bridge backend-image
docker run -d --name db --network my-bridge db-image

```

| Feature                       | Bridge Network                                          |
| ----------------------------- | ------------------------------------------------------- |
| IPs                           | Each container gets a **private IP** (e.g., 172.18.0.2) |
| Inter-container communication | ✅ Yes (via IP or name: `http://backend:port`)          |
| External access               | ❌ No (unless you **publish ports**)                    |
| Isolation                     | ✅ Isolated from other bridge networks                  |

🌐 Example
frontend can access backend via http://backend:5000

But outside browser can’t access frontend unless you run:

- `docker run -p 8080:80 --network my-bridge frontend`

2. host

```t
`docker run -d --network host --name frontend frontend-image`
```

| Feature                       | Host Network                                           |
| ----------------------------- | ------------------------------------------------------ |
| IPs                           | No container IP → uses host’s IP (e.g., EC2 public IP) |
| Inter-container communication | ✅ Yes (via `localhost:port`)                          |
| External access               | ✅ Yes (host IP + exposed port)                        |
| Isolation                     | ❌ No isolation between container and host             |

4. overlay

Setup (on Swarm Mode only)

```t
docker network create --driver overlay my-overlay
docker service create --name frontend --network my-overlay frontend-image
```

| Feature                       | Overlay Network                        |
| ----------------------------- | -------------------------------------- |
| IPs                           | Each container gets an IP across hosts |
| Inter-container communication | ✅ Yes, across multiple Docker hosts   |
| External access               | ✅ If port is published                |
| Isolation                     | ✅ Isolated per overlay network        |

- frontend (on host A) can talk to backend (on host B)

- Ideal for microservices on multiple EC2s or VMs

- create custom n/w

```t
 docker network create \
 -- driver bridge \
 -- subnet 82.18.0.0/16
 custom-isolated-network

```

- Inspect ` docker inspect <Containerame>` or `docker network inspect <n/wName>`

---

## Container Orchestration

### SWARM

- Creates replicas and manages them to manage the load
- `docker service --replicas=3 my-app`

## Troubleshoot

### Logs

- `docker logs <containerName>`

### Restart Policies

- "no" - it won't restart
- "always" - it will restart if container fails, unless you stopped it and also restart if the docker engine or demon get restart
- "unless-stopped" - the container will restart if it is stopped implicitly only.
- "on-failure" - restarts on failure

# Docker with AWS

# ECS

- ECS is a EC2 Container Service that runs the docker containers on EC2 or FARGATES

# ECR

- ECR is a Elastic Container Registry that stores the Images. It is like docker hub in AWS.

# CLUSTER

- ECS cluster is a regional grouping of one or more container instances on which you can run task requests.When an instance launches, the ECS-agent software on the server registers the instance to an ECS Cluster. You can choose an existing VPC, or create a new one to spin up your container instances.

## Task Definition

- It is the complete definition of your tasks(in simple terms, your containers) and to describe how containers should be provisioned. Here You need to provide a link to ECR’s saved container images, CPU units, Memory, Container ports to expose, network type and many more. Simple terms, you are defining your containers and how to launch them via Task definitions.

## TASK

- It is nothing but “ A RUNNING CONTAINER “. The description you provided for your containers in TASK DEFINITION, TASKS are the result of that. It can be thought of as a “RUNNING INSTANCE” of a Task Definition.

## ECS Service

- ECS SERVICE allows you to run your container instances as defined in your task definition. It also allows you to run and maintain a specified number of instances by configuring the auto-scaling policies. If any of your tasks fail or stop for any reason, the Amazon ECS service scheduler launches another instance of your task definition to replace it and maintain the desired count of tasks. You can optionally run your service behind a load balancer, The load balancer distributes traffic across the tasks that are associated with the service

## Docker Volumes

- Basically the data inside the container is not persistent
- because the docker works on layer format. the images was build by layer by layer model.
- when we run a new container then there will be a new writable layer created and wvery thing that we modified will be on that layer..
- when we destroyed or restart the container then the writable layer will be deleted so the data stored on the writable layer will be deleted..

- when we create a file inside the container then:
- container creates file → stored in writable layer
- container deleted → writable layer deleted
- file gone

- Where Volumes are stored : /var/lib/docker/volumes/
- Each volume has its own directory:

- /var/lib/docker/volumes/my-volume/\_data

👉 This is where your actual data lives.

- Types of Volumes
  1. Named Volumes: Like `docker volume create myvol`
  - Docker Manages them
  - Easy to use
  - Best for production
  2. Anonymous Volumes: like `docker run -v /app nginx`
  - Docker randomly creates them. Hard to track

- Volume Demo
  1. `docker volume create demo-volume`
  2. `docker run -it --name vol-test -v demo-volume:/data ubuntu bash`
  3. create file and add some content.
  4. delete the container
  5. use the volume for new container
  6. we can see the old file that we created

- Binding Mounts
  - Similar to Volumes but we bind the host machine folder
  - Like `docker run -it -v $(pwd):/data ubuntu bash`
  - So all the changes are insync b/w host and the container
  - Read Only Mode
  - docker run -v $(pwd):/app:ro nginx

    👉 :ro = read-only

- Volume Backup's
  - ```docker run --rm \
      -v my-volume:/data \
      -v $(pwd):/backup \
      ubuntu tar czf /backup/backup.tar.gz /data
    ```

- Restore Volume
  - ```docker run --rm \
    -v my-volume:/data \
    -v $(pwd):/backup \
    ubuntu tar xzf /backup/backup.tar.gz -C /
    ```

- Volume Migration
  - Convert the data into tar
  - And copy the tar file to new server
  - And restore it same as above by binding the host machine folder to container

- Volume Driver
  - Driver is like a plugin that helps docker to store data in remote server
  - We have local driver by default that stores data within the host or container
  - We have NFS, EFS that heps to have shared Storage system...
  - Works across multiple host.
  - ```
      docker volume create \
    --driver local \
    --opt type=nfs \
    --opt o=addr=192.168.1.10,rw \
    --opt device=:/data \
    nfs-volume
    ```

## Docker N/W

- Flow

👉 Container starts
↓
Network namespace created
↓
veth pair created (Virtual cable)
↓
One end → container (eth0)
Other end → attached to docker0 bridge
↓
IP assigned

- here the docker0 manages the communication b/w the containers. it is like a router , that knows where the packets has to be sent...

- Q3: How does container get internet?

👉 Through NAT via host

- Connecting n/w to existig container
- docker network connect my-network container-name
- use disconnect to disconnect

- To see routing IP tables : `sudo iptables -t nat -L -n`

### Overlay N/w

- How Overlay Works (Core Concept 🔥)

Overlay uses:

👉 VXLAN (Virtual Extensible LAN)

🧠 What VXLAN Does

It wraps your packet like this:

Original Packet:
Container A → Container B

Encapsulated:
[Outer IP (Host1 → Host2)]
[Inner Packet (Container A → Container B)]

☀️ Step-by-Step Packet Flow (VERY IMPORTANT)

1. Container A sends packet to Container B
2. Docker encapsulates packet (VXLAN)
3. Packet travels via host network
4. Host 2 receives packet
5. Docker decapsulatesm
6. Delivered to Container B
