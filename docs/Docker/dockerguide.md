# Quick Git & Docker Deployment Guide

This guide provides the basic steps to clone a Git repository and run it as a Docker container. Aimed for speed and simplicity during a competition.

**Estimated Time:** 10-30 minutes (depending on project complexity and download speeds)

## Prerequisites

1.  **Git:** Installed on your machine. ([https://git-scm.com/](https://git-scm.com/))
2.  **Docker:** Installed and *running* on your machine (Docker Desktop or Docker Engine). ([https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/))
3.  **GitHub Repository URL:** You need the HTTPS or SSH URL of the project repository you need to deploy. Example: `https://github.com/username/project-name.git`

## Step 1: Clone the Project Repository

Open your terminal or command prompt.

1.  **Navigate** to the directory where you want to store the project locally:
    ```bash
    cd /path/to/your/workspace
    ```

2.  **Clone** the repository using its URL:
    ```bash
    git clone <repository_url>
    # Example: git clone https://github.com/username/project-name.git
    ```

3.  **Change Directory** into the cloned project folder:
    ```bash
    cd project-name
    # (Replace 'project-name' with the actual folder name created by git clone)
    ```

## Step 2: Locate or Create the Dockerfile

A `Dockerfile` is a text file containing instructions to build a Docker image.

1.  **Check for an existing Dockerfile:** Look for a file named exactly `Dockerfile` (no extension) in the root directory of the project you just cloned.
    ```bash
    ls -a
    # Look for 'Dockerfile' in the output
    ```

2.  **If a `Dockerfile` exists:** Great! Proceed to review its contents quickly if you have time, especially the `EXPOSE` command (which tells you the port the application runs on inside the container) and the `CMD` or `ENTRYPOINT` (which tells you how the application starts).

3.  **If NO `Dockerfile` exists (CRITICAL):** You *might* need to create a basic one. This depends heavily on the project's technology. **If the competition rules imply the project *should* have one, double-check the repo or ask an organizer.** If you *must* create one, here are very basic *templates* you'd adapt:

    *   **Remember to replace placeholders** like `your-app-entrypoint.js`, `requirements.txt`, `your_main_module:app`, `main.go`, `your-app-binary`, and port numbers (`3000`, `5000`, `8080`) with the actual values for the project.

    ---

    **Example 1: Node.js Application**

    ```dockerfile
    # Use an official Node.js runtime as a parent image (Alpine versions are smaller)
    FROM node:18-alpine

    # Set the working directory in the container
    WORKDIR /usr/src/app

    # Copy package.json and package-lock.json (or yarn.lock) first
    # This leverages Docker's build cache
    COPY package*.json ./

    # Install app dependencies
    RUN npm install
    # Or: RUN yarn install

    # Bundle app source inside the Docker image
    COPY . .

    # What port the app runs on *inside* the container (check project docs/code)
    EXPOSE 3000

    # Define the command to run your app
    CMD [ "node", "index.js" ]
    ```

    ---

    **Example 2: Python Application (Flask/Django style)**

    ```dockerfile
    # Use an official Python runtime as a parent image (slim versions are good)
    FROM python:3.9-slim

    # Set the working directory in the container
    WORKDIR /app

    # Copy the requirements file first for caching
    COPY requirements.txt ./

    # Install any needed packages specified in requirements.txt
    RUN pip install --no-cache-dir -r requirements.txt

    # Copy the rest of the application code
    COPY . .

    # Make port 5000 available to the world outside this container (adjust if needed)
    EXPOSE 5000 # Common for Flask, Django might use 8000

    # Define the command to run your app (using gunicorn is common for production)
    # Replace 'your_main_module:app' with the actual module and Flask app variable
    # Or for Django: CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
    CMD ["gunicorn", "--bind", "0.0.0.0:5000", "your_main_module:app"]
    # Or a simpler version for development/basic apps:
    # CMD ["python", "./index.py"]
    ```

    ---

    **Example 3: Go Application (Multi-stage build)**

    ```dockerfile
    # --- Build Stage ---
    # Use an official Go image for building the binary
    FROM golang:1.19 as builder

    # Set the working directory inside the build stage
    WORKDIR /app

    # Copy Go modules manifests
    COPY go.mod go.sum ./

    # Download dependencies
    RUN go mod init
    # RUN go mod download

    # Copy the source code
    COPY . .

    # Build the Go app - creates a static binary
    # CGO_ENABLED=0 makes it fully static (no C dependencies)
    # -o /app/your-app-binary specifies the output path/name for the compiled app
    RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o /app/your-app-binary ./cmd/your-main-package/main.go
    # Adjust './cmd/your-main-package/main.go' to the actual entrypoint of your Go app

    # --- Final Stage ---
    # Use a minimal base image like Alpine or Scratch for the final container
    FROM alpine:latest
    # FROM scratch # Smallest possible, but no shell/tools

    # Alpine needs libc runtime library if not fully static build
    RUN apk --no-cache add ca-certificates

    # Set working directory
    WORKDIR /root/

    # Copy only the compiled binary from the build stage
    COPY --from=builder /app/your-app-binary .

    # What port the app listens on (check project code)
    EXPOSE 8080

    # Command to run the executable
    CMD ["./your-app-binary"]
    ```

    ---

    *   **Save the chosen template** (after adapting it) as a file named exactly `Dockerfile` (no extension) in the project's root directory.
    *   **You MUST customize** the template based on the project's specific structure, dependencies, entry point, and exposed port.

## Step 3: Build the Docker Image

Make sure you are still in the project's root directory in your terminal (the one with the `Dockerfile`).

1.  **Build the image** using the `docker build` command.
    *   The `-t` flag tags your image with a name (e.g., `my-app:latest`).
    *   The `.` indicates that the build context (including the `Dockerfile` and project files) is the current directory.

    ```bash
    docker build -t my-app:latest .
    ```
    *(You can replace `my-app` with a more descriptive name if you like.)*

2.  **Wait** for the build process to complete. It might download base images and run commands from the `Dockerfile`. Look for a `Successfully built <image_id>` and `Successfully tagged my-app:latest` message at the end.

## Step 4: Run the Docker Container

Now, run a container from the image you just built.

1.  **Run the container** using the `docker run` command:
    *   `-d`: Run in detached mode (in the background).
    *   `-p <host_port>:<container_port>`: Map a port on your host machine to a port inside the container.
        *   Replace `<host_port>` with a free port on your machine (e.g., `8080`).
        *   Replace `<container_port>` with the port the application *inside* the container listens on (the one specified in the `EXPOSE` instruction in the `Dockerfile`, e.g., `3000`, `5000`, `8080`).
    *   `--name <container_name>`: Give your container a memorable name (optional but helpful).
    *   `my-app:latest`: The name of the image you built.

    ```bash
    # Example for Node.js app exposing 3000
    docker run -d -p 8080:3000 --name my-running-app my-app:latest

    # Example for Python app exposing 5000
    # docker run -d -p 8080:5000 --name my-running-app my-app:latest

    # Example for Go app exposing 8080
    # docker run -d -p 8080:8080 --name my-running-app my-app:latest
    ```
    *   **Adjust the `-p` flag!** Match the `<container_port>` to the `EXPOSE` value in your Dockerfile. Use a different `<host_port>` if `8080` is already in use on your machine.

## Step 5: Verify the Deployment

1.  **Check running containers:**
    ```bash
    docker ps
    ```
    You should see your container (`my-running-app`) listed with its status as `Up`.

2.  **Access the application:** Open your web browser and go to `http://localhost:<host_port>` (using the `<host_port>` you specified in the `docker run -p` command).
    *   Example: `http://localhost:8080`

3.  **Check logs (if needed):** If the application isn't working, check the container's logs for errors:
    ```bash
    docker logs my-running-app
    ```

## Quick Cleanup (Optional)

*   **Stop the container:**
    ```bash
    docker stop my-running-app
    ```
*   **Remove the container:** (Must be stopped first)
    ```bash
    docker rm my-running-app
    ```
*   **Remove the image:**
    ```bash
    docker rmi my-app:latest
    ```
