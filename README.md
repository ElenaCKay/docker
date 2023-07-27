# Docker

Docker provides a RESTful API that allows developers and users to interact with the Docker daemon programmatically. This API enables you to manage Docker containers, images, networks, volumes, and other resources remotely. Below is a general overview of how the Docker API works:

## 1. Docker Daemon

The Docker daemon is a background service that manages Docker containers, images, and other resources on the host system. It listens to the Docker API requests and performs actions accordingly.

## 2. API Endpoints

The Docker API exposes a set of HTTP endpoints that correspond to different Docker functionalities. These endpoints are accessible over HTTP, and each endpoint handles specific actions or operations.

## 3. HTTP Methods

To interact with the Docker API, clients use standard HTTP methods such as GET, POST, PUT, DELETE, etc., to issue requests to the API endpoints. The methods correspond to specific actions like creating a container, pulling an image, inspecting a container, starting/stopping a container, and so on.

## 4. Authentication

The Docker API can be secured using various authentication methods, such as TLS (Transport Layer Security) certificates, tokens, or username/password-based authentication, depending on the configuration.

## 5. API Versioning

The Docker API is versioned, allowing Docker to introduce changes and improvements while maintaining backward compatibility. Clients can specify the version they want to use in the request URL, such as `/v1.41/containers`.

## 6. JSON Format

Both request payloads and responses from the Docker API are in JSON format, making it easy to work with various programming languages.

### Example Workflow

Let's say you want to create a new Docker container using the Docker API. The steps might be as follows:

1. Your application or script sends an HTTP POST request to the appropriate API endpoint (e.g., `/containers/create`) with the necessary parameters, such as the image to use, container name, and network settings, in the request payload.

2. The Docker daemon receives the API request, processes it, and creates a new container based on the provided specifications.

3. The Docker daemon responds with an HTTP response containing relevant information about the created container, such as its ID and status.

4. If needed, you can then use other API endpoints to start, stop, restart, inspect, or remove the container, and perform various other management tasks.

## How to install docker on Windows

[Install docker](https://docs.docker.com/desktop/install/windows-install/)

Check docker is installed with `docker --version`

For the a list of docker commands `docker`

## Main Docker Commands

Here is a table listing some of the main Docker commands:

| Command                                      | Description                                               |
|----------------------------------------------|-----------------------------------------------------------|
| `docker run [OPTIONS] IMAGE [COMMAND] [ARGS]`   | Create and start a new container                         |
| `docker ps [OPTIONS]`                           | List running containers                                   |
| `docker images [OPTIONS]`                       | List available images                                     |
| `docker pull IMAGE[:TAG]`                       | Download an image from a registry                         |
| `docker build [OPTIONS] PATH/URL`               | Build an image from a Dockerfile                          |
| `docker stop [OPTIONS] CONTAINER [CONTAINER...]` | Stop one or more running containers                       |
| `docker start [OPTIONS] CONTAINER [CONTAINER...]`| Start one or more stopped containers                      |
| `docker restart [OPTIONS] CONTAINER [CONTAINER...]` | Restart one or more containers                         |
| `docker rm [OPTIONS] CONTAINER [CONTAINER...]`   | Remove one or more containers                             |
| `docker rmi [OPTIONS] IMAGE [IMAGE...]`          | Remove one or more images                                 |
| `docker exec [OPTIONS] CONTAINER COMMAND [ARGS]` | Run a command in a running container                      |
| `docker logs [OPTIONS] CONTAINER`               | Fetch the logs of a container                             |
| `docker inspect [OPTIONS] CONTAINER IMAGE`      | Display detailed information about a container or image   |
| `docker network ls`                             | List available networks                                   |
| `docker volume ls`                              | List available volumes                                    |
| `docker-compose [OPTIONS] [COMMAND] [ARGS]`     | Define and run multi-container Docker applications       |
| `docker system prune`                           | Remove unused data (containers, images, networks, etc.)   |
| `docker version`                               | Show the Docker version information                       |
| `docker info`                                  | Display system-wide information                           |

Remember that Docker provides many more commands and options. Use `docker --help` to see the complete list of available commands and `docker COMMAND --help` to get help on a specific command.

### Setting up docker

Create a docker hub account. Then check if it is running. To check if everything is working correctly run `docker run hello-world`. This will give a response with a reply saying hello if it has worked. If you recieve an error then something isnt set up correctly. Possible docker isnt running or the firewall is having issues.

### Setting up nginx container

`docker run -d -p 80:80 nginx` - get the api from docker and run it 

`docker ps` - check it is running and get the id

`docker stop {id}` - stop it running

`docker start {id}` - start it 

`docker exec -it {id} sh` - sh in to the vm 

Once in the vm you can make live changes to it and see the changes occuring in the browser. 

When in here it has little dependencies so I did an update and then installed sudo and nano.

```
apt update -y
apt install sudo
sudo install nano
cd /usr/share/nginx/html

sudo nano index.html
```

In the index.html you can make changes to the homepage of nginx and see it in the browser with localhost.

Then I exited `exit`.

To commit it I did `docker commit {id} ellieckay/nginx-test`

Then pushed it `docker push {id} ellieckay/nginx-test`

This command lets anyone see the page on localhost:100
```
docker run -d -p 100:80  ellieckay/nginx-test:latest
```

## Automate docker

Create a new folder for the docker.
Add a index.html file with some basic html. This will show up on the browser. Add another file called Dockerfile and this is where you add the script:

```
# Write the script in here

# Select base image
FROM nginx

# Label it
LABEL MAINTAINER=elena@sparta

# get index.html from localhost to default nginx index.html location
COPY index.html /usr/share/nginx/html/

# port mapping or exposing the required port
EXPOSE 80

# launch the new container
CMD ["nginx", "-g", "daemon off;"]

```

In the command line in the correct folder run these commands:

```
docker build -t ellieckay/tech241-nginx:v1 . # Builds it

docker run -d -p 97:80 ellieckay/tech241-nginx:v1 # Runs it

docker commit 061f4ffcf4ba ellieckay/tech241-nginx:v1 # Commits it 

docker push ellieckay/tech241-nginx:tagname # Pushes it to docker hub

```