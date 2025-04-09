# Quick Docker Compose Deployment Guide

This guide shows how to use a basic `docker-compose.yml` file to build and run your cloned Git project as a Docker container. This often simplifies the build and run steps, especially for single-service applications common in competitions.

**Estimated Time:** 10-20 minutes (assuming `Dockerfile` exists and is correct)

## Prerequisites

1.  **Git:** Installed.
2.  **Docker:** Installed and running.
3.  **Docker Compose:** Installed.
    *   *Note:* Docker Compose V2 (`docker compose`) is standard with Docker Desktop. Older versions use `docker-compose`. Use `docker compose` first; if it fails, try `docker-compose`.
4.  **GitHub Repository URL:** The URL of the project.
5.  **Project with a Dockerfile:** The target repository *must* contain a correctly configured `Dockerfile` for the application's technology (Node.js, Python, Go, etc.). If not, you'll need to create one first.

## Step 1: Clone the Project Repository

(Same as before)

1.  **Navigate** to your workspace:
    ```bash
    cd /path/to/your/workspace
    ```
2.  **Clone** the repository:
    ```bash
    git clone <repository_url>
    # Example: git clone https://github.com/username/project-name.git
    ```
3.  **Change Directory** into the cloned project folder:
    ```bash
    cd project-name
    # (Replace 'project-name' with the actual folder name)
    ```

## Step 2: Verify the Dockerfile Exists and Note Port

(Crucial for the `build` step and port mapping)

1.  **Check** for the `Dockerfile` in the project root:
    ```bash
    ls -a
    ```
    *   **If it doesn't exist, STOP.** Docker Compose needs it to build the image. You must create a suitable `Dockerfile` first (refer to previous examples if needed).
2.  **If it exists, view its contents** (e.g., `cat Dockerfile`) and **find the `EXPOSE` instruction**. Note the `<container_port>` number (e.g., `3000`, `5000`, `8080`). You *need* this for the `docker-compose.yml`.
3.  Also, quickly check the `CMD` or `ENTRYPOINT` in the `Dockerfile` to ensure it looks correct for starting the application.

## Step 3: Create the `docker-compose.yml` File

This file tells Docker Compose how to build and run your application container.

1.  **Create** a new file named exactly `docker-compose.yml` in the **root directory** of your project (the same directory where the `Dockerfile` is).

2.  **Choose ONE** of the following examples based on the project's technology (Node.js, Python, or Go) and **copy its content** into your `docker-compose.yml` file.

3.  **Customize** the chosen example, especially the `ports` section.

    ---

    **Example 1: Node.js Application (`Dockerfile` EXPOSEs 3000)**

    ```yaml
    # File: docker-compose.yml (for Node.js project)
    version: '3.8'

    services:
      # Service name (can be anything, e.g., 'app', 'web')
      node-app:
        # Build the image using the Dockerfile in the current directory (.)
        build: .
        # Name the resulting container (optional, but helpful)
        container_name: my-node-app-container
        ports:
          # Map port <host_port> on your machine to container port 3000
          # CHOOSE a free <host_port> (e.g., 8080)
          - "<host_port>:3000"
          # Example: - "8080:3000"
        # Optional: Define environment variables if needed by the Node app
        # environment:
        #   - NODE_ENV=production
        #   - API_KEY=your_api_key_here
    ```

    ---

    **Example 2: Python Application (`Dockerfile` EXPOSEs 5000)**

    *Make sure the `CMD` in your Python `Dockerfile` is correct (e.g., using Gunicorn on `0.0.0.0:5000` or `python manage.py runserver 0.0.0.0:8000`)*

    ```yaml
    # File: docker-compose.yml (for Python project)
    version: '3.8'

    services:
      python-app:
        build: .
        container_name: my-python-app-container
        ports:
          # Map port <host_port> on your machine to container port 5000
          # (Adjust container port if your Dockerfile/CMD uses a different one, e.g., 8000)
          # CHOOSE a free <host_port> (e.g., 8081)
          - "<host_port>:5000"
          # Example for Flask/Gunicorn on 5000: - "8081:5000"
          # Example for Django runserver on 8000: - "8081:8000"
        # Optional: Define environment variables if needed by the Python app
        # environment:
        #   - FLASK_ENV=production
        #   - DATABASE_URL=your_db_connection_string
    ```

    ---

    **Example 3: Go Application (`Dockerfile` EXPOSEs 8080)**

    *Make sure your Go `Dockerfile` is complete (including the final stage) and correctly builds/copies/runs your binary, and that the `EXPOSE` matches the port your Go app listens on.*

    ```yaml
    # File: docker-compose.yml (for Go project)
    version: '3.8'

    services:
      go-app:
        build: .
        container_name: my-go-app-container
        ports:
          # Map port <host_port> on your machine to container port 8080
          # (Adjust container port if your Dockerfile/Go app uses a different one)
          # CHOOSE a free <host_port> (e.g., 8082)
          - "<host_port>:8080"
          # Example: - "8082:8080"
        # Optional: Define environment variables if needed by the Go app
        # environment:
        #   - GIN_MODE=release
        #   - LISTEN_PORT=8080
    ```

    ---

4.  **Customize the Ports:**
    *   Replace `<host_port>` in the chosen example with a port number that is **free** on your local machine (e.g., `8080`, `8081`, `8082`, `5000`, `80`). This is the port you will access via `localhost:<host_port>` in your browser.
    *   Ensure the `<container_port>` (the number *after* the colon, e.g., `3000`, `5000`, `8080`) **exactly matches** the port number specified in the `EXPOSE` instruction of your project's `Dockerfile` *and* the port the application inside the container actually listens on.

5.  **(Optional) Customize Service/Container Names:** You can change `node-app`, `python-app`, `go-app` or `my-node-app-container`, etc., if desired, but the defaults are usually fine for a competition.

6.  **Save** the `docker-compose.yml` file.

## Step 4: Build and Run with Docker Compose

Make sure you are in the project's root directory (where `docker-compose.yml` and `Dockerfile` are) in your terminal.

1.  **Build and Start:** This command builds the image using the `Dockerfile` (if needed) and starts the container defined in `docker-compose.yml`.
    *   `--build`: Forces Docker Compose to rebuild the image, ensuring your latest `Dockerfile` changes are used. Recommended for competitions.
    *   `-d`: Runs the containers in detached mode (in the background).

    ```bash
    docker compose up --build -d
    ```

2.  **Wait** for the command to complete. Building might take some time, especially the first time. Look for output indicating the container(s) were created and started.

## Step 5: Verify the Deployment

1.  **Check running Compose services:**
    ```bash
    docker compose ps
    ```
    You should see your service (e.g., `node-app`, `python-app`, `go-app`) listed with State/Status `Up` or `running`.

2.  **Check container logs:** Essential for debugging if the app doesn't work. Replace `<service_name>` with the name you used in `docker-compose.yml` (e.g., `node-app`, `python-app`, `go-app`).
    ```bash
    docker compose logs <service_name>
    # Example: docker compose logs node-app
    ```
    *   Use `-f` to follow the logs in real-time: `docker compose logs -f <service_name>`

3.  **Check all Docker containers (optional standard command):**
    ```bash
    docker ps
    ```
    You should see your container listed (e.g., `my-node-app-container` or a generated name like `project-name-node-app-1`).

4.  **Access the application:** Open your web browser and go to `http://localhost:<host_port>` (using the `<host_port>` you specified in the `ports:` section of your `docker-compose.yml`).
    *   Example if you used `"8080:3000"`: `http://localhost:8080`
    *   Example if you used `"8081:5000"`: `http://localhost:8081`
    *   Example if you used `"8082:8080"`: `http://localhost:8082`

## Step 6: Stop and Clean Up

When you're finished with the container:

1.  **Stop and remove containers, networks defined by Compose:** Execute this command from the *same directory* containing the `docker-compose.yml` file.
    ```bash
    docker compose down
    ```
    *   This stops and removes the containers created by `docker compose up`.
    *   To also remove named volumes (if you used any): `docker compose down -v`

2.  **(Optional) Remove the built image:** `docker compose down` does *not* remove the image. Use `docker images` to find the image name (often tagged like `<directory_name>-<service_name>`) and then remove it if needed.
    ```bash
    # 1. Find the image name/tag (e.g., project-name-node-app)
    docker images

    # 2. Remove the specific image
    docker rmi <image_name_tag>
    # Example: docker rmi project-name-node-app
    ```

This Docker Compose approach streamlines the build and run process into fewer commands, making it efficient for competitions. Good luck!
