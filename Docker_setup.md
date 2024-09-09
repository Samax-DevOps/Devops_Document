# Docker Install using the docker.io package on Ubuntu

## Step 1: Update Your Package List ##
First, update the package index to ensure you're working with the latest list of available packages:

```bash
Copy code
sudo apt update
```

## Step 2: Install Docker ##
Now, install Docker using the docker.io package from the Ubuntu repository:

```bash
Copy code
sudo apt install -y docker.io
```

This will install Docker, the Docker CLI, and other related tools.

## Step 3: Start and Enable Docker ##
After installation, start the Docker service and enable it to automatically start on boot:

```bash
Copy code
sudo systemctl start docker
sudo systemctl enable docker
```

##  Step 4: Verify Docker Installation ##
To confirm that Docker has been installed and is running correctly, check the version:

```bash
Copy code
docker --version
```
You can also run a test container to ensure everything is working:

```bash
sudo docker run hello-world
```

## Step 5: (Optional) Manage Docker as a Non-Root User ##
To avoid using sudo for every Docker command, add your user to the docker group:

```bash
sudo usermod -aG docker $USER
```

After running this command, log out and log back in, or run:

```bash
newgrp docker
```
Now you can use Docker commands without sudo:

```bash
docker ps
```

## Step 6: Test Docker Setup ##
To make sure Docker is running properly, try pulling and running an image, such as Nginx:

bash
Copy code
docker pull nginx
docker run -d -p 80:80 nginx
This will pull the Nginx image and start an Nginx web server on port 80.

With these steps, Docker will be installed on your Ubuntu system, and you'll be able to use it to run containers.            
