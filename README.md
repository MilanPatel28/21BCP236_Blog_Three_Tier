# 21BCP236 - My Jekyll Blog

## Introduction to Three-Tier Application with MongoDB, Node.js, React.js, and Docker

A three-tier architecture divides an application into three logical layers: presentation layer, application layer, and data layer. In our case, we are using the following technologies:

- **MongoDB:** A NoSQL database used as the data layer to store and manage application data.
- **Node.js:** A JavaScript runtime environment used in the application layer to run server-side code.
- **React.js:** A JavaScript library used in the presentation layer to build interactive user interfaces.
- **Docker:** A containerization platform used to package the application along with its dependencies into containers for easy deployment and scalability.

## Steps to Deploy the Three-Tier Application

1. **Get the Code from a Repository**
   - I have used the project of one of my friend: [MERN Stack Todo List](https://github.com/murlipatel1/mernstack_todolist).

2. **Build Docker Images**
   - Write Dockerfiles for frontend, backend, and MongoDB server. Then, build images for each component using Docker.
   ![image](https://github.com/MilanPatel28/21BCP236_Blog_Three_Tier/assets/102026489/fc1ea4bf-cccf-4b69-a878-24d8f7546d50)
   ![image](https://github.com/MilanPatel28/21BCP236_Blog_Three_Tier/assets/102026489/2b388043-3859-40d2-8ce0-76f39f1e61c6)
   ![image](https://github.com/MilanPatel28/21BCP236_Blog_Three_Tier/assets/102026489/697532d2-f648-44e0-ad70-e16a38a022e6)

3. **Run Docker Containers**
   - Run Docker containers using the built images for frontend, backend, and MongoDB server.
   ![image](https://github.com/MilanPatel28/21BCP236_Blog_Three_Tier/assets/102026489/55546ef3-5762-45da-bd74-93e802283500)
   ![image](https://github.com/MilanPatel28/21BCP236_Blog_Three_Tier/assets/102026489/36faacd5-90a5-4b79-ac7d-4b2ed98ead77)
   ![image](https://github.com/MilanPatel28/21BCP236_Blog_Three_Tier/assets/102026489/f54e0e0c-adc3-4aa2-8be7-5feaf1f4f067)

## Understanding Dockerfiles

A Dockerfile is a text file that contains instructions for building a Docker image. Here's a sample Dockerfile for each component:

- **MongoDB (Server) Dockerfile:**
  ```Dockerfile
  FROM mongo:latest
  # Expose MongoDB port
  EXPOSE 27017
  ```

- **Backend Dockerfile:**
```Dockerfile
FROM node:latest
# Set working directory
WORKDIR /app
# Copy package.json and package-lock.json
COPY package*.json ./
# Install dependencies
RUN npm install
# Copy server files
COPY . .
# Expose port
EXPOSE 5000
# Command to run the server
CMD ["node", "index.js"]
```

- **Frontend Dockerfile:**
```Dockerfile
# Use Node.js image as base
FROM node:latest AS build
# Set working directory
WORKDIR /app
# Copy package.json and package-lock.json
COPY package*.json ./
# Install dependencies
RUN npm install
# Copy the ReactJS application files
COPY . .
# Build the React app
RUN npm run build

# Production environment
FROM nginx:alpine
# Copy build files to Nginx
COPY --from=build /app/build /usr/share/nginx/html
# Expose port
EXPOSE 80
```

## Building and Running Docker Images

To build and run Docker images, use the following commands:

- **Build MongoDB Server Image:**
```bash
docker build -t 21bcp236-mongodb ./mongodb
```

- **Run MongoDB Container:**
```bash
docker run -d --name 21bcp236-mongodb-container --network todolist_IA 21bcp236-mongodb
```

- **Build Backend Image:**
```bash
docker build -t 21bcp236-backend ./backend
```

- **Run Backend Container:**
```bash
docker run -d --name 21bcp236-backend-container --network todolist_IA 21bcp236-backend
```

- **Build Frontend Image:**
```bash
docker build -t 21bcp236-frontend ./frontend
```

- **Run Frontend Container:**
```bash
docker run -d --name 21bcp236-frontend-container --network todolist_IA 21bcp236-frontend
```

## Pushing Docker Images to Docker Hub

Follow these steps to push Docker images to Docker Hub:

- **Login to Docker Hub:**
```bash
docker login
```
Enter your Docker Hub username and password when prompted.

- **Tag the Docker Image:**
```bash
docker tag my-mongodb username/my-mongodb
```
Replace username with your Docker Hub username.

- **Push the Docker Image:**
```bash
docker push username/my-mongodb
```

This will push the MongoDB Docker image to your Docker Hub repository. Repeat the same steps for Node.js and React.js Docker images.

![image](https://github.com/MilanPatel28/21BCP236_Blog_Three_Tier/assets/102026489/eb35b011-9300-4e3c-b1f5-a616ff5905b5)

# Conclusion

By following the steps outlined in this guide, you can deploy a three-tier application using MongoDB, Node.js, React.js, and Docker. This architecture provides scalability, flexibility, and ease of deployment for modern web applications.

© 21BCP236 - PDEU, Gandhinagar

