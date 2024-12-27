# Developing with Docker and Docker-Compose

This repository demonstrates how to setup a Node.js application with MongoDB using Docker and Docker-Compose. The project includes a basic profile management application that allows users to view and edit their profile information.

## Project Structure
```
.
├── app/
│   ├── images/
│   │   └── profile.jpg
│   ├── index.html
│   ├── server.js
│   ├── package.json
├── docker-compose.yaml
├── Dockerfile
├── README.md
```

### File Descriptions
- **app/**: Contains the application files.
  - **images/**: Includes static images (e.g., `profile.jpg`).
  - **index.html**: The frontend HTML file for the user interface.
  - **server.js**: The Node.js backend server.
  - **package.json**: Node.js project dependencies and metadata.
- **docker-compose.yaml**: Configuration file to define and run multi-container Docker applications.
- **Dockerfile**: Instructions to build the Docker image for the Node.js application.
- **README.md**: Documentation for the project.

## Features
- Displays a user profile with a picture, name, email, and interests.
- Allows user to edit name, email and interests and save the resutl.
- Uses MongoDB as the database to store profile information.
- Includes a `mongo-express` interface for database management.

## Prerequisites
Ensure you have the following installed:
- [Docker](https://www.docker.com/get-started)
- [Docker-Compose](https://docs.docker.com/compose/)

## Setup Instructions

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd <repository-folder>
   ```

2. Create an `.env` file in the root directory and define the following environment variables:
   ```env
   MONGO_ADMIN_USER=admin
   MONGO_ADMIN_PASS=password
   ```

3. Build and run the Docker containers:
   ```bash
   docker-compose -f docker-compose.yaml -p docker up -d
   ```

4. Access the application:
   - **App**: Open [http://localhost:3000](http://localhost:3000) in your browser.
   - **Mongo-Express**: Open [http://localhost:8081](http://localhost:8081) for MongoDB management.

## Application Overview

### Frontend
- The `index.html` file provides a simple UI for the user profile.
- Users can view and edit their profile details (name, email, interests).

### Backend
- The `server.js` file implements API endpoints:
  - `GET /get-profile`: Fetch user profile information.
  - `POST /update-profile`: Update user profile information.

### Database
- MongoDB is used to store the user profile.
- Mongo-Express provides an easy way to manage the database.

## Docker-Compose Configuration
The `docker-compose.yaml` file defines three services:

1. **my-app**
   - Builds the Node.js application from the `Dockerfile`.
   - Exposes the application on port `3000`.
   - Connects to the `mongo` service.

2. **mongo**
   - Runs a MongoDB container.
   - Exposes MongoDB on port `27017`.

3. **mongo-express**
   - Provides a web-based interface to manage MongoDB.
   - Exposes the interface on port `8081`.

## Dockerfile
The `Dockerfile` is used to build the Node.js application image:
```dockerfile
FROM node:alpine3.20
RUN mkdir -p /home/app
COPY ./app /home/app
WORKDIR /home/app
RUN npm install
CMD [ "node", "server.js" ]
```

## Cleanup
To stop the application and remove containers, networks, and volumes created by Docker-Compose:
```bash
docker-compose -f docker-compose.yaml -p docker down
```
To remove unused Docker images and associated dangling artifacts:
```bash
docker image rm $(docker images -q)
```

## License
This project is licensed under the MIT License.

---
Enjoy working with Docker and Docker-Compose to deploy Node.js applications!
