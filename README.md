# Docker Project with Backend, Frontend, and Database

### Course name: ST2SAS - Docker Containers
### Teacher: Ilyes Jenhani

## Team Members
- Martin Kang
- Rayan Houfani
- Clement Leveque
- Tom Klajn

## Project Overview

This project is an application composed of three main services:
- **Backend**: A REST API service that handles the application logic and communicates with the database.
- **Frontend**: A user interface (UI) that allows interaction with the backend API.
- **Database (MySQL)**: A MySQL database for storing application data.

### Project Structure

```
.
├── .idea/                 # IDE configuration
├── backend/               # Code and Dockerfile for the backend
│   ├── controllers/       # Controllers for application logic
│   ├── models/            # Data models
│   ├── routes/            # API route definitions
│   ├── .dockerignore      # File to ignore certain files during Docker build
│   ├── app.js             # Entry point for the backend application
│   ├── db_connexion.js    # Database connection configuration
│   ├── Dockerfile         # Dockerfile for the backend
│   ├── package.json       # Node.js dependencies and scripts
│   └── package-lock.json  # Dependency lock file
├── frontend/              # Code and Dockerfile for the frontend
│   ├── public/            # Public static files
│   ├── src/               # Source code for the frontend application
│   ├── .dockerignore      # File to ignore certain files during Docker build
│   ├── Dockerfile         # Dockerfile for the frontend
│   ├── index.html         # Main HTML file
│   ├── package.json       # Node.js dependencies and scripts
│   ├── package-lock.json  # Dependency lock file
│   └── vite.config.js     # Vite configuration
├── .gitignore             # File to ignore certain files in Git
├── docker-compose.yml     # Docker Compose configuration
├── README.md              # Project documentation
└── schema.sql             # Script for creating tables and schemas in MySQL
```

## System Configuration

- **Operating System**: (specify based on the system used, e.g., Ubuntu 20.04, macOS Monterey)
- **Hypervisor**: Docker (version 3.8)
- **Docker Version**: (specify, e.g., Docker 20.10.8)
- **Docker Compose**: version 3.8

## Installation Instructions

1. Clone the project and navigate to the main directory.
2. Start the services using Docker Compose by running:

   ```bash
   docker-compose up --build
   ```

## Running Services

- **Backend**: Accessible at [http://localhost:3000](http://localhost:3000)
- **Frontend**: Accessible at [http://localhost:8080](http://localhost:8080)
- **Database**: MySQL, available on port `3306`

## Docker Compose Functionality

The `docker-compose.yml` file uses three services:

- **backend**:
    - Built from the `./backend` directory
    - Exposes port 3000
    - Communicates with the MySQL database service
    - Environment variables:
        - `DB_HOST`, `DB_USERNAME`, `DB_PASSWORD`, `DB_DATABASE`
        - `JWT_SECRET`: Secret for handling JWT tokens
    - Volume `backend-images` for storing application images.

- **frontend**:
    - Built from the `./frontend` directory
    - Exposes port 8080
    - Depends on the backend to function.

- **db**:
    - Image `mysql:latest`
    - Exposes port 3306
    - Initializes the database with the `schema.sql` file in the `db-data` volume to persist data.

### Volumes

- `db-data`: Stores MySQL data persistently.
- `backend-images`: Stores images used by the backend.

---
