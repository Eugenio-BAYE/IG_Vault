
# Installing Docker on Linux

If you want to use Docker directly from your Linux terminal without Docker Desktop, follow these steps. Docker can be installed using your package manager, and this guide will walk you through the setup on Ubuntu (or similar distributions). 

## Step 1: Update the package list

First, update your system's package list to ensure you have the latest versions of the necessary tools:

```bash
sudo apt-get update
```

## Step 2: Install prerequisites

Docker requires a few additional packages to be installed before you can proceed. These include packages for handling HTTPS connections and certificates:

```bash
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

## Step 3: Add Docker’s official GPG key

Next, you'll add Docker's official GPG key to your system. This allows your package manager to verify the integrity of the Docker packages you install:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

## Step 4: Set up the stable repository

Now, add Docker’s official stable repository to your package sources:

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## Step 5: Install Docker Engine

Update your package list again to include Docker packages from the new repository:

```bash
sudo apt-get update
```

Then, install Docker Engine and related components:

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## Step 6: Start and enable Docker

Start the Docker service and ensure it runs on startup:

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

## Step 7: Verify installation

To confirm that Docker is installed correctly, run the `hello-world` image:

```bash
sudo docker run hello-world
```

This will download a test image and run it in a container. If you see the "Hello from Docker!" message, Docker is correctly installed and working.

## Optional: Manage Docker as a non-root user

By default, Docker commands require `sudo`. To avoid using `sudo` every time, you can add your user to the `docker` group:

```bash
sudo usermod -aG docker $USER
```

Log out and back in for this change to take effect.

## Next Steps

You now have Docker installed on your Linux system, ready to be used from the terminal. You can start exploring Docker images, running containers, and building your own applications in containers.
