# Docker Project

### Course: ST2SAS - Docker Containers
### Instructor: Ilyes Jenhani

## Team Members
- Martin Kang
- Rayan Houfani
- Clement Leveque
- Tom Klajn

## Project Overview

This project is an application composed of three main services:

1. **Backend**: A REST API service that handles application logic and communicates with the database.
2. **Frontend**: A user interface (UI) that allows interaction with the backend API.
3. **Database (MySQL)**: A MySQL database for storing application data.

### Project Structure

The project is organized into three main parts:
- **backend/**: Contains the backend code, application logic, database connection configuration, and Dockerfile.
- **frontend/**: Contains the frontend code, static resources, and Dockerfile.
- **docker-compose.yml**: Docker Compose configuration to orchestrate the three services.

## System Configuration

- **Docker Version**: 4.33.0
- **Docker Compose Version**: 3.8.

## Installation Instructions

1. Start the services using Docker Compose by running:

   ```bash
   docker-compose up --build
   ```

## Running Services

- **Backend**: Accessible at [http://localhost:3000](http://localhost:3000)
- **Frontend**: Accessible at [http://localhost:8080](http://localhost:8080)
- **Database**: MySQL, available on port `3306`

## Docker Compose Functionality

The `docker-compose.yml` file defines three services:

- **backend**:
    - Built from the `./backend` directory
    - Exposes port 3000
    - Communicates with the MySQL database service
    - Environment variables: `DB_HOST`, `DB_USERNAME`, `DB_PASSWORD`, `DB_DATABASE`, `JWT_SECRET`
    - Volume `backend-images` for storing application images.

- **frontend**:
    - Built from the `./frontend` directory
    - Exposes port 8080
    - Depends on the backend to function.

- **db**:
    - Image `mysql:latest`
    - Exposes port 3306
    - Initializes the database with the `schema.sql` file in the `db-data` volume to persist data.

### Docker Compose Configuration

```yaml
version: '3.8'

services:
  backend:
    build: ./backend # Build the backend service
    ports:
      - "3000:3000" # Map port 3000 on the host to container
    depends_on:
      - db # Database must start before backend
    environment:
      - DB_HOST=db
      - DB_USERNAME=user
      - DB_PASSWORD=password
      - DB_DATABASE=database
      - JWT_SECRET=your_jwt_secret
    volumes:
      - backend-images:/usr/src/app/images # Persist image files

  frontend:
    build: ./frontend # Build the frontend service
    ports:
      - "8080:8080" # Map port 8080 on the host to container
    depends_on:
      - backend

  db:
    image: mysql:latest # Use latest MySQL image
    ports:
      - "3306:3306" # Map port 3306 on the host to container
    environment:
      - MYSQL_ROOT_PASSWORD=password
      - MYSQL_DATABASE=database
      - MYSQL_USER=user
      - MYSQL_PASSWORD=password
    volumes:
      - db-data:/var/lib/mysql # Persist MySQL data
      - ./schema.sql:/docker-entrypoint-initdb.d/schema.sql # Initialize database

volumes:
  db-data:
  backend-images:
```

### Volumes

- `db-data`: Stores MySQL data persistently.
- `backend-images`: Stores images used by the backend.

---
