# Using Docker: Creating a Dockerfile

Now that Docker is installed, you can start using it to containerize your applications. A key part of this process is creating a `Dockerfile`, which is a text file that contains a series of instructions Docker uses to build an image for your application.

## What is a Dockerfile?

A `Dockerfile` is essentially a blueprint for your Docker image. It defines the base image, dependencies, and the steps required to build and run your application inside a container.

### Basic Structure of a Dockerfile

Here's a typical structure of a `Dockerfile`:

1. **FROM**: Specifies the base image (e.g., `node`, `ubuntu`).
2. **WORKDIR**: Sets the working directory inside the container.
3. **COPY**: Copies files from your local machine to the container.
4. **RUN**: Executes commands during the build process (e.g., installing dependencies).
5. **CMD** or **ENTRYPOINT**: Defines the command that runs when the container starts.

### Example: Dockerizing a Node.js Application

Let's say you have a simple Node.js application with the following file structure:

```
my-app/
  ├── Dockerfile
  ├── package.json
  └── app.js
```

Here’s how you can create a `Dockerfile` for this app:

1. **Create the Dockerfile**

In your project folder, create a file named `Dockerfile` with the following content:

```dockerfile
# Use the official Node.js image as the base
FROM node:20-alpine

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy the package.json and package-lock.json to the container
COPY package*.json ./

# Install the app dependencies inside the container
RUN npm install

# Copy the rest of the app's source code to the container
COPY . .

# Expose the port the app runs on
EXPOSE 3000

# Define the command to run the app
CMD ["node", "app.js"]
```

### Dockerfile Breakdown

- `FROM node:20-alpine`: Starts with the Node.js image (version 20, Alpine variant, which is lightweight).
- `WORKDIR /usr/src/app`: Sets `/usr/src/app` as the working directory inside the container.
- `COPY package*.json ./`: Copies the `package.json` and `package-lock.json` files into the container.
- `RUN npm install`: Installs all the dependencies specified in the `package.json`.
- `COPY . .`: Copies the rest of your app's code into the container.
- `EXPOSE 3000`: Exposes port 3000 to make the app accessible from outside the container.
- `CMD ["node", "app.js"]`: Specifies the command to run the application when the container starts.

## Step 1: Build the Docker Image

Once the `Dockerfile` is created, you can build the Docker image using the following command:

```bash
docker build -t my-node-app .
```

- `-t my-node-app`: Tags the image with the name `my-node-app`.
- `.`: Refers to the current directory where the `Dockerfile` is located.

## Step 2: Run the Docker Container

After building the image, run the container using this command:

```bash
docker run -p 3000:3000 my-node-app
```

- `-p 3000:3000`: Maps port 3000 on your local machine to port 3000 inside the container.

You can now access the Node.js application by opening `http://localhost:3000` in your browser.

## Step 3: Stopping and Cleaning Up

To stop the running container, find its `CONTAINER ID` by listing all running containers:

```bash
docker ps
```

Then, stop the container with the following command:

```bash
docker stop <CONTAINER_ID>
```

To remove the stopped container:

```bash
docker rm <CONTAINER_ID>
```

You can also remove the image if no longer needed:

```bash
docker rmi my-node-app
```

## Conclusion

With this simple `Dockerfile`, you’ve successfully containerized a Node.js application, built a Docker image, and run it inside a container. From here, you can build more complex applications by adding databases, using `docker-compose`, and managing multiple services inside containers.