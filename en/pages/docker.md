# Docker

## Check version
    docker --version
    docker-compose --version
    docker-machine --version

## Containers

#### List all containers
	docker ps -a
        -a  all
        -l  last
        w/o paremeters  all started

#### Display system-wide information
	docker info

#### Start container
	docker start <containerName>

#### Stop container
	docker stop <containerName>

#### Stop and remove container
	docker rm -f <containerName>

#### Show container logs
	docker logs -f <containerName>
        -f flag causes the docker logs command to act like the tail -f command and watch the container’s standard output.

#### Show container processes
	docker top <containerName>
the processes running inside container

#### Inspect container
	docker inspect <containerName>
JSON document containing useful configuration and status information for container

Run `exit` to stop the container and close Bash shell

## Images

#### Docker images
	docker images

#### Remove image
	docker rmi <imageID>|<imageName>

#### Examples
Pull an image from Docker Hub and start a container

	docker run hello-world      - run the container with image hello-world
	docker run -it ubuntu bash
		-t flag assigns a pseudo-tty or terminal inside the new container
		-i flag allows you to make an interactive connection by grabbing the standard input (STDIN) of the container

	docker run -d -p 80:80 --name webserver nginx
		-d flag runs the container in the background (to daemonize it)

	docker run -d -P training/webapp python app.py
		the -P flag maps any required network ports inside the container to your host. This lets you view the web application.
		-P means the same as -p 5000

	docker run --rm -v $PWD:/app -w /app demo/oracle-java:8 javac Main.java
		--rm
			Automatically remove the container when it exits
		-v
			Bind mount a volume
		-w
			Working directory inside the container
		--name string
			Assign a name to the container

#### Search for Docker images
	docker search "linux mint"

#### Build an image
	docker build -f Dockerfile -t demo/oracle-java:8 .
		-f specifies the Dockerfile. This can be skipped if the filename used at the beginning of this process is Dockerfile.
		-t specifies the name of the image. The name demo/oracle-java, and the 8 after the colon, specify the image tag. The tag 8 is used because we are using Java 8. This can be changed to any tag name that makes sense.

> Note: Do not forget the .(dot) at the end of command; it specifies the context of the build. The .(dot) at the end of the command specifies the current directory. The files and directories of current directory will be sent to Docker daemon as a build artifact.

## Machines

#### List Docker Machines
	docker-machine ls

#### Create a machine
	docker-machine create --driver virtualbox <machineName>

#### Remove Docker Machines
	docker-machine rm my-docker-machine

#### IP
Docker is configured to use the default machine with IP 192.168.99.100

    docker-machine ip
        192.168.99.100

Use Machine to run Docker containers.
To run a Docker container, you:

- create a new (or start an existing) Docker virtual machine
- switch your environment to your new VM
- use the docker client to create, load, and manage containers

Once you create a machine, you can reuse it as often as you like. Like any VirtualBox VM, it maintains its configuration between uses.

The examples [here](https://docs.docker.com/machine/get-started/#use-machine-to-run-docker-containers) show how to create and start a machine, run Docker commands, and work with containers.

## Compose

#### Spin Off service(s) from docker-compose.yml file
	docker-compose up

#### Rebuild image(s)
	docker-compose build 		, or
	docker-compose up --build

#### Stop the application
    docker-compose down	     from within your project directory in the second terminal, or
    CTRL+C                          in the original terminal where you started the app

## Volumes

#### Create a volume
	docker volume create my-vol

#### List volumes
	docker volume ls

#### Inspect a volume
	docker volume inspect my-vol

#### Remove a volume
	docker volume rm my-vol

## Installation

#### Windows
- Docker CLI client for running Docker Engine to create images and containers
- Docker Machine so you can run Docker Engine commands from Windows terminals
- Docker Compose for running the docker-compose command
- Kitematic, the Docker GUI
- Docker QuickStart shell preconfigured for a Docker command-line environment
- Oracle VM VirtualBox