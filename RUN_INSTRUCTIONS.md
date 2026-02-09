# Running Dash with Docker

## Prerequisites

**Yes, you MUST start Docker Desktop first.**
Docker Desktop provides the Docker Engine that runs the containers. If it is not running, the commands below will fail with an error like `error during connect: This error may indicate that the docker daemon is not running`.

---

## 1. Start the Application

Open your terminal (PowerShell or Command Prompt) in this directory (`dash`) and run:

```powershell
docker compose up -d --build
```

- `up`: Starts the containers.
- `-d`: **Detached mode**. Runs containers in the background so they don't block your terminal.
- `--build`: Forces a rebuild of the images (useful if you've changed code).

## 2. Verify It's Running

Check the status of your containers:

```powershell
docker ps
```

You should see two containers listed:

- `dash-api` (Port 8000)
- `dash-db` (Port 5432)

## 3. Access the Application

Once running, you can access:

- **API Documentation (Swagger UI)**: [http://localhost:8000/docs](http://localhost:8000/docs)
- **API Redoc**: [http://localhost:8000/redoc](http://localhost:8000/redoc)
- **Database**: `localhost:5432` (User/Pass/DB: `ai` / `ai` / `ai`)

## 4. View Logs (Debugging)

If something isn't working or you want to see the agent's output:

```powershell
# Follow logs for the API service
docker compose logs -f dash-api
```

_(Press `Ctrl+C` to stop following logs)_

## 5. Stop the Application

To stop and remove the containers (preserve data in volumes):

```powershell
docker compose down
```

To stop and **delete all data** (clean slate):

```powershell
docker compose down -v
```
