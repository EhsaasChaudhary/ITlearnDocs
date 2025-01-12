# Docker Basics

Docker is an open-source platform that allows you to automate the deployment of applications inside lightweight, portable containers. Containers include everything an application needs to run, such as libraries, dependencies, and configuration files.

## Why Use Docker?
1. **Consistency Across Environments:** Eliminates the "works on my machine" problem by ensuring applications run the same everywhere.
2. **Resource Efficiency:** Containers are lightweight compared to virtual machines.
3. **Speed:** Containers start quickly as they do not boot up an operating system.
4. **Portability:** Docker containers can run on any system with Docker installed.
5. **Scalability:** Simplifies scaling applications across distributed systems.

---

## Key Components of Docker

### 1. **Docker Engine**
   - The core component that runs and manages containers.

### 2. **Docker Images**
   - Immutable, lightweight, and self-sufficient packages containing an application and its environment.

### 3. **Docker Containers**
   - Instances of Docker images running as separate processes on the host machine.

### 4. **Dockerfile**
   - A script with instructions to build a Docker image.

### 5. **Docker Compose**
   - A tool to define and manage multi-container applications.

---

### Verify installation:
```bash
docker --version
```

### Common Docker Commands

#### **Images**
- `docker pull <image>`: Download an image from Docker Hub.
- `docker images`: List all downloaded images.
- `docker rmi <image>`: Remove an image.

#### **Containers**
- `docker run <image>`: Run a container.
- `docker ps`: List running containers.
- `docker ps -a`: List all containers (including stopped ones).
- `docker stop <container>`: Stop a running container.
- `docker rm <container>`: Remove a container.

#### **Build and Logs**
- `docker build -t <tag> .`: Build an image from a Dockerfile.
- `docker logs <container>`: View logs of a container.

#### **Other Commands**
- `docker exec -it <container> <command>`: Run a command inside a running container.
- `docker network ls`: List Docker networks.

---

## Dockerfile

A `Dockerfile` is used to create a custom Docker image. Below is an example:

```dockerfile
# Use an official Node.js runtime as a base image
FROM node:18

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json ./
RUN npm install

# Copy the application source code
COPY . ./

# Expose the application port
EXPOSE 3000

# Command to run the application
CMD ["npm", "run", "dev"]
```

Build the image and run the container:
```bash
docker build -t my-node-app .
docker run -p 3000:3000 my-node-app
```

---

## Docker Compose

Docker Compose allows you to define and run multi-container applications. A `docker-compose.yml` file specifies the services.

### Example: Node.js and MongoDB

```yaml
services:
  development:
    build:
      context: .
      dockerfile: Dockerfile.prod
      target: development
    ports:
      - "3000:3000"
    volumes:
      - .:/app 
      - /app/node_modules  
    environment:
      - NODE_ENV=development

```

Start the application:
```bash
docker-compose up
```

Stop and remove containers:
```bash
docker-compose down
```

---

## Additional Resources

- [Docker Documentation](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)
- [Docker Cheatsheet](https://github.com/wsargent/docker-cheat-sheet)
