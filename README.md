# Dockerized React App

This project is a React application that runs inside a Docker container. It uses Docker Compose to manage services and supports live reloading for development. 

## Table of Contents

- [Prerequisites](#prerequisites)
- [Project Setup](#project-setup)
- [Docker Setup](#docker-setup)


## Prerequisites

Before you begin, ensure you have the following installed on your system:

- **Docker**: [Install Docker](https://docs.docker.com/get-docker/)
- **Docker Compose**: [Install Docker Compose](https://docs.docker.com/compose/install/)

## Project Setup

1. Clone the repository or create a new React app:

    ```bash
    npx create-react-app myapp
    cd myapp
    ```

2. Create a `Dockerfile` in the project root:

    ```Dockerfile
    FROM node:20

    WORKDIR /myapp

    COPY . .

    RUN npm install

    EXPOSE 3000

    CMD ["npm", "start"]
    ```

3. Create a `docker-compose.yml` file in the root directory:

    ```yaml
    version: "3"

    services:
      mywebapp:
        build: ./
        ports:
          - "8080:3000"
        container_name: 'mywebapp'
        volumes:
          - .:/myapp
          - /myapp/node_modules
        stdin_open: true
        tty: true
    ```

## Docker Setup

### Build the Docker Image

To build the Docker image for the project, run:

```bash
docker-compose build
