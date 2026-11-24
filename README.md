# MyAppReact – Docker & Docker Compose

## 1. Project description

This project demonstrates how to containerize a React frontend and an Express backend using Docker, and how to orchestrate the services using Docker Compose.

## 2. Technologies used

- **Frontend:** React.js + Vite
- **Backend:** Node.js + Express.js
- **Database service:** MongoDB
- **Containerization:** Docker
- **Orchestration:** Docker Compose

## 3. Project architecture

The application contains three services:

| Service | Description | Port |
|---|---|---|
| Client | React frontend | 3000 |
| Server | Express REST API | 9000 |
| MongoDB | Database service | 27017 (internal) |

The services communicate through a Docker network created by Docker Compose.

## 4. Dockerfiles

Two Dockerfiles are used:

- `Client/Dockerfile`: installs dependencies, builds the React application, and serves the production build on port 3000.
- `Server/Dockerfile`: installs backend dependencies and starts the Express server on port 9000.

## 5. Docker Compose configuration

The `docker-compose.yml` file defines the three services:

- `mongodb`: runs the MongoDB image.
- `server`: builds the backend image and exposes port 9000.
- `client`: builds the frontend image and exposes port 3000.

The services are connected through the `mern-network` bridge network. The backend receives the MongoDB connection URI through the `MONGO_URI` environment variable.

**Note:** MongoDB is started as a service, but the current Express code does not yet establish a database connection.

## 6. Build and run the application

Open a terminal in the project root directory and execute:

```bash
docker compose up --build -d
```

Check the running containers:

```bash
docker compose ps
```

View service logs:

```bash
docker compose logs
```

## 7. Test the application

Open the following URLs in a browser:

- Frontend: http://localhost:3000
- Backend API: http://localhost:9000/api/health

Expected API response:

```json
{
  "message": "API is running"
}
```

The React frontend sends a request to the backend API and displays the returned message.

## 8. Stop the application

To stop and remove the containers and network created by Docker Compose:

```bash
docker compose down
```

## 9. Conclusion

This practical work demonstrates how to create Docker images for a React frontend and an Express backend, run services in separate containers, connect them through a Docker network, and manage the complete application using Docker Compose.