# Docker Setup for FastStats

This document provides instructions for running the FastStats application using Docker.
The setup includes both the backend and frontend services, along with their required databases.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Components

The Docker setup consists of the following services:

1. **Backend**: Java/Kotlin application running on port 5000
2. **Frontend**: Next.js application running on port 3000
3. **PostgreSQL**: Database for frontend

## Getting Started

### Building and Running the Application

1. Clone the repository:
   ```bash
   git clone https://github.com/fastStats-org/faststats.git
   cd faststats
   ```

2. Start all services using Docker Compose:
   ```bash
   docker compose up --build
   ```

   This command will:
    - Build the backend and frontend images
    - Start all services defined in the docker-compose.yml file
    - Set up the necessary networking between containers
    - Mount volumes for data persistence

3. To run the services in the background (detached mode):
   ```bash
   docker compose up --build -d
   ```

4. To stop the services:
   ```bash
   docker compose down
   ```

### Accessing the Application

- **Frontend**: Access the web interface at http://localhost:3000
- **Metrics**: The metrics service is accessible at http://localhost:5000

## Data Persistence

The setup includes data persistence through Docker volumes:

- **PostgreSQL data**: Stored in the `postgres_data` volume (used by frontend)
- **Backend data**: Mounted from `./backend/data` on the host to `/app/data` in the container
  (contains SQLite database files)

## Environment Variables

### Frontend Environment Variables

- `NEXT_PUBLIC_BACKEND_URL`: URL to connect to the backend service (default: `http://backend:5000`)

## Customization

You can customize the Docker setup by modifying the following files:

- `docker-compose.yml`: Main configuration file for all services
- `backend/Dockerfile`: Dockerfile for the backend service
- `frontend/Dockerfile`: Dockerfile for the frontend service

## Troubleshooting

### Common Issues

1. **Port conflicts**: If you already have services running on ports 3000 or 5000, you may need to modify the
   port mappings in the docker-compose.yml file.

2. **Database connection issues**: Ensure that the environment variables for database connections are correctly set.

3. **Container startup order**: The docker-compose.yml file includes dependencies and health checks to ensure services
   start in the correct order. If you experience issues, you may need to restart the services.

### Viewing Logs

To view logs for all services:

```bash
docker compose logs
```

To view logs for a specific service:

```bash
docker compose logs [service-name]
```

For example:

```bash
docker compose logs backend
```

## Additional Information

For more information about the FastStats application,
refer to the documentation in the backend and frontend directories.