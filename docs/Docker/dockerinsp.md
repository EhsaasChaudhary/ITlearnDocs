# Docker Inspection Commands Cheat Sheet

This guide lists common commands to inspect Docker images and containers. Use these to practice and understand the state of your Docker environment.

**Remember:**
*   Replace `<image_name_or_id>` with the actual image name (e.g., `my-app:latest`, `ubuntu`) or its unique ID (or the first few unique characters).
*   Replace `<container_name_or_id>` with the actual container name (e.g., `my-running-app`) or its unique ID (or the first few unique characters).
*   Many commands have `docker <noun> <verb>` structure (e.g., `docker image ls`, `docker container stop`). Older syntax often omits the noun (e.g., `docker images`, `docker stop`), but the newer form is generally recommended.

---

## Inspecting Images

Commands to view and understand the Docker images stored on your machine.

1.  **List Images:** Show all top-level images on your system.
    ```bash
    docker images
    # OR (newer syntax)
    docker image ls
    ```
    *   *Use `-a` to show intermediate image layers too:* `docker images -a`

2.  **Inspect Image Details:** Show detailed information about an image in JSON format (layers, commands, environment variables, etc.).
    ```bash
    docker image inspect <image_name_or_id>
    # Example: docker image inspect my-app:latest
    # Example: docker image inspect a2a15febcdf3
    ```

3.  **View Image History:** Show the layers that make up an image and how they were created. Useful for seeing the commands run in the Dockerfile.
    ```bash
    docker image history <image_name_or_id>
    # Example: docker image history python:3.9-slim
    ```

4.  **Remove an Image:** Delete an image from your local storage.
    ```bash
    docker rmi <image_name_or_id>
    # OR (newer syntax)
    docker image rm <image_name_or_id>
    ```
    *   *Use `-f` to force removal if the image is used by stopped containers:* `docker rmi -f <image_name_or_id>`

5.  **Remove Unused Images:** Delete dangling images (layers with no tag/reference) and optionally all unused images.
    ```bash
    # Remove dangling images
    docker image prune

    # Remove all unused images (not associated with any container)
    docker image prune -a
    ```
    *   *Use `-f` to skip confirmation:* `docker image prune -f`

---

## Inspecting Containers

Commands to view and interact with running or stopped Docker containers.

1.  **List Running Containers:** Show only the containers currently running.
    ```bash
    docker ps
    # OR (newer syntax)
    docker container ls
    ```

2.  **List All Containers:** Show all containers, including stopped ones.
    ```bash
    docker ps -a
    # OR (newer syntax)
    docker container ls -a
    ```

3.  **Inspect Container Details:** Show detailed information about a container in JSON format (state, network settings, volumes, environment variables, etc.).
    ```bash
    docker container inspect <container_name_or_id>
    # Example: docker container inspect my-running-app
    # Example: docker container inspect b1a9a7ecae0f
    ```

4.  **View Container Logs:** Fetch the logs (stdout/stderr) from a container. Essential for debugging.
    ```bash
    docker logs <container_name_or_id>
    # Example: docker logs my-running-app
    ```
    *   *Follow log output (like `tail -f`):* `docker logs -f <container_name_or_id>`
    *   *Show logs since a specific time:* `docker logs --since 10m <container_name_or_id>` (last 10 minutes)
    *   *Show last N lines:* `docker logs --tail 50 <container_name_or_id>` (last 50 lines)

5.  **View Processes in Container:** Show the processes running *inside* a specific container (like `top` on Linux).
    ```bash
    docker top <container_name_or_id>
    # Example: docker top my-running-app
    ```

6.  **View Container Resource Usage:** Live stream of container(s) resource usage statistics (CPU, Memory, Network I/O, Block I/O).
    ```bash
    # For specific containers
    docker stats <container_name_or_id> [another_container...]
    # Example: docker stats my-running-app

    # For all running containers (press Ctrl+C to stop)
    docker stats
    ```

7.  **Execute Command in Running Container:** Run a command inside an already running container. Often used to get an interactive shell.
    ```bash
    docker exec [options] <container_name_or_id> <command>
    # Example: Get an interactive shell (if the image has /bin/sh)
    docker exec -it <container_name_or_id> sh

    # Example: Get an interactive bash shell (if the image has /bin/bash)
    docker exec -it <container_name_or_id> bash

    # Example: List files in /app directory inside the container
    docker exec <container_name_or_id> ls /app
    ```
    *   `-i`: Interactive (keep STDIN open)
    *   `-t`: Allocate a pseudo-TTY (terminal)

8.  **Stop a Container:** Gracefully stop one or more running containers.
    ```bash
    docker stop <container_name_or_id> [another_container...]
    # Example: docker stop my-running-app
    ```

9.  **Start a Stopped Container:** Start one or more stopped containers.
    ```bash
    docker start <container_name_or_id> [another_container...]
    # Example: docker start my-running-app
    ```

10. **Remove a Container:** Delete one or more *stopped* containers.
    ```bash
    docker rm <container_name_or_id> [another_container...]
    # Example: docker rm my-stopped-app
    ```
    *   *Use `-f` to force remove a running container (use with caution!):* `docker rm -f <container_name_or_id>`

11. **Remove Stopped Containers:** Delete all stopped containers.
    ```bash
    docker container prune
    ```
    *   *Use `-f` to skip confirmation:* `docker container prune -f`

---

**Practice Tip:** Try running a simple image like `docker run -d --name hello-test nginx`, then use the inspection commands above on the `hello-test` container and the `nginx` image. Finally, practice stopping (`docker stop hello-test`), removing (`docker rm hello-test`), and cleaning up the image (`docker rmi nginx`).