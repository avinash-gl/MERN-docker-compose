# 🚢 Dockerized MERN Stack App

This project is a full-stack MERN (MongoDB, Express, React, Node.js) application containerized using Docker and orchestrated with Docker Compose.


**Tech Stack Used**

- **Application**: MERN
- **Containerization**: Docker, Docker Compose

**Note:** This project was built to practice Docker and Docker Compose by containerizing a MERN stack application and setting up multi-service orchestration.


## 🛠️ Learnings

- Writing Dockerfiles for frontend (React) and backend (Node.js)
- Creating and using a custom Docker bridge network
- Using Docker Compose to orchestrate multi-container apps
- Connecting Node backend to MongoDB container
- Mapping ports between host and containers
- Using `volumes` for MongoDB data persistence
- Running and debugging containers with `docker-compose logs`

**Docker and Docker Compose File**

- Frontend:

```text
FROM node:18.9.1

WORKDIR /app

COPY package*.json .

RUN npm install 

COPY . /app

EXPOSE 5173

CMD ["npm", "run", "dev"]
```

- Backend:

```text
FROM node:18.9.1

WORKDIR /app

COPY package*.json .

RUN npm install

COPY . .

EXPOSE 5050

CMD ["npm", "start"]
```

- docker-compose.yml

```text
version: "3.8"

services:

  frontend:
    build:
      context: ./mern/frontend
    ports:
      - "5173:5173"
    networks:
      - mern-docker-network
  
  backend:
    build:
      context: ./mern/backend
    ports:
      - "5050:5050"
    networks:
      - mern-docker-network
    depends_on:
      - db


  db:
    image: mongo:latest
    container_name: mongo_db
    ports:
      - "27017:27017"
    networks: 
      - mern-docker-network
    volumes:
      - db_data:/data/db

volumes:
  db_data:

networks:
  mern-docker-network:
  ```


## Usage

**Note** - To run this project using `docker compose`, follow the below steps.

1. Clone the Repository
```bash
git clone https://github.com/avinash-gl/MERN-docker-compose.git
cd MERN-docker-compose
```

2. Build and Run using Docker Compose

```bash
docker compose up --build
```


## Screenshots

<img width="1790" alt="Screenshot 2024-08-31 at 11 07 58 PM" src="https://github.com/user-attachments/assets/f414230b-8bd6-4393-b8de-6a10444a8dfd">
