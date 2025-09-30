# mcpgrid-infra

Infrastructure setup for the MCPGrid AI project using Docker Compose.

## Overview

This repository provides a complete local development environment for the MCPGrid AI project, including a PostgreSQL database and Google Cloud Pub/Sub emulator for testing and development purposes.

## Services

This infrastructure includes the following services:

### PostgreSQL Database
- **Image**: postgres:15
- **Container**: postgres
- **Port**: 5432
- **Database**: mydatabase
- **Username**: myuser
- **Password**: mypassword
- **Data persistence**: Uses Docker volume `postgres_data`

### Google Cloud Pub/Sub Emulator
- **Image**: google/cloud-sdk:latest
- **Container**: pubsub
- **Port**: 8085
- **Project ID**: mcpgrid-ai
- **Host**: 0.0.0.0:8085

## Quick Start

1. **Start all services**:
   ```bash
   npm run docker
   ```
   or
   ```bash
   docker-compose up -d
   ```

2. **Stop all services**:
   ```bash
   docker-compose down
   ```

3. **View logs**:
   ```bash
   docker-compose logs -f
   ```

## Service URLs

- **PostgreSQL**: `localhost:5432`
- **Pub/Sub Emulator**: `localhost:8085`

## Development

### Connecting to PostgreSQL
```bash
psql -h localhost -p 5432 -U myuser -d mydatabase
```

### Using Pub/Sub Emulator
Set the following environment variable:
```bash
export PUBSUB_EMULATOR_HOST=localhost:8085
```

## Data Persistence

PostgreSQL data is persisted in the `postgres_data` Docker volume. To reset the database:

```bash
docker-compose down -v
docker-compose up -d
```

## Troubleshooting

### Check service status
```bash
docker-compose ps
```

### View specific service logs
```bash
# PostgreSQL logs
docker-compose logs postgres

# Pub/Sub emulator logs
docker-compose logs pubsub
```

### Restart a specific service
```bash
docker-compose restart postgres
docker-compose restart pubsub
```

## Environment Variables

The following environment variables are used by the services:

- `POSTGRES_USER`: Database username (default: myuser)
- `POSTGRES_PASSWORD`: Database password (default: mypassword)
- `POSTGRES_DB`: Database name (default: mydatabase)
- `PUBSUB_PROJECT_ID`: Pub/Sub project ID (default: mcpgrid-ai)

## Requirements

- Docker
- Docker Compose
- Node.js (for npm scripts)

## License

This project is part of the MCPGrid AI infrastructure.