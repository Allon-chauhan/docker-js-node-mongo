# 🐳 Use Docker for Local Development

### 🛠️ Technologies Used:
1. Docker
2. Node.js
3. MongoDB
4. MongoExpress

## ✅ Prerequisites:
1. npm installed on your local computer to run the Node server.
2. Docker installed on your local computer to download images and run containers.

### 📥 Downloading Sample Node.js (HTML & JavaScript) Code and Required Docker Images
1. Download a sample Node.js code from [here](https://gitlab.com/twn-devops-bootcamp/latest/07-docker/js-app.git).
2. Download the MongoDB Docker image by entering the following command:
   ```bash
   docker pull mongo
   ```
   Reference: [Docker Hub](https://hub.docker.com/_/mongo)
3. Download the MongoExpress Docker image by entering the following command:
   ```bash
   docker pull mongo-express
   ```
   Reference: [Docker Hub](https://hub.docker.com/_/mongo-express)

### 🌐 Creating a Docker Network for Internal Container Communication
1. Use this command to create a Docker network:
   ```bash
   docker network create mongo-network
   ```
   *(We will use this when creating Docker containers)*

### 🚀 Running and Configuring Containers to Run the Images

1. Run the MongoDB container and set environment variables (Database Admin Username and Password):
   ```bash
   docker run -d \
     -p 27017:27017 \
     -e MONGO_INITDB_ROOT_USERNAME=admin \
     -e MONGO_INITDB_ROOT_PASSWORD=password \
     --name mongodb \
     --net mongo-network \
     mongo:latest
   ```
2. Run the MongoExpress container and set environment variables:
   ```bash
   docker run -d \
     -p 8081:8081 \
     -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
     -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
     --net mongo-network \
     -e ME_CONFIG_MONGODB_SERVER=mongodb \
     --name mongo-express \
     mongo-express:latest
   ```
   *(The server.js file is already configured with the above username and password to connect to MongoDB)*

### 🔧 Accessing and Configuring MongoExpress
1. Open your browser and navigate to:
   ```
   http://localhost:8081
   ```
2. **Credentials:**
   Reference: [MongoExpress Docker Hub](https://hub.docker.com/_/mongo-express)

   | Name                            | Default  | Description        |
      |---------------------------------|----------|--------------------|
   | ME_CONFIG_MONGODB_AUTH_DATABASE | 'db'     | Database name      |
   | ME_CONFIG_MONGODB_AUTH_USERNAME | 'admin'  | Database username  |
   | ME_CONFIG_MONGODB_AUTH_PASSWORD | 'pass'   | Database password  |

3. Create a new database named `user-account`.
4. Create a new collection named `users` within the `user-account` database.

*Note: These specific database and collection names are provided in the `server.js` file. If changed, make sure to update them in the file as well!*

### 🟢 Starting the Node.js Server
1. On your local computer, ensure you're in the app directory. Use the command below to confirm:
   ```bash
   pwd
   ```
2. Set up npm:
   ```bash
   npm install
   ```
3. Start the server:
   ```bash
   node server.js
   ```
4. Open your browser and navigate to:
   ```
   http://localhost:3000
   ```
