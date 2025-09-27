
### What is docker ?
#### To understand docker first we need to know Why docker ? What is the need of it and why ?
- So in the early days, before docker what used to happen was...
- Let's say we built an application in node js and using mongo as the database.
- And we have node version as 16 mongo version as something and we are building in a linux machine.
- It is working fine in my laptop. Now I gave this code to my friend to test this. And he has node version 20, mongo version diffrent from mine and he has a windows machine.
- Now the code is not running in his machine due to this version mismatch. Now what he can do is he has to update to the versions that my app is using and also he has to use linux but it is very tidious task for him.
- So this when we work on a big product in the company it will be so hard to manage and test the app like this. 
- To solve this problem contanerization comes to the picture.
- What contanerization means is, we will create an container inside which I will install same version of node and mongo as of the application and we will run the application in that container.
- And when I want to test the code by my friend, I will give him this container. Now irrespective of what version and operating system he has in his machine, the container will run.
- Docker is a company or service that provides this containerization.

### How it is different from Virtual Machines ?

- Virtual machines have their own operating system.

- An operating system is build in two layers or main component we can say, one is the kernel and the other is application layer.

- So every VMs has an OS, which makes their size big.

- But in docker, it uses the host machine's kernel and only the application layer is different. So the size of the container is very small compared to VMs.

- This is the reason if you have older windows machine (below windows 10) or older macos version then there might be some docker container which will not run because docker is built for linux kernel. In the newer versions this is no longer an issue.


### Docker Networks

- Docker network is a private network inside docker which is used to connect containers together.

- First of all, why docker network ?

- Let's understand with an example:

- Suppose we are using two containers, one is `mongo` for database and another one is a simple express app container, which has two endpoints.

1. `/users` which returs all the users in the database

2. `/user` which is a post request to add a user in the database.

- Now, the problem is how we are gonna connect them.

- Because when we run the express app locally, we give the mong_url as localhost:27017, if we are using mongo container then we have to do port maping with -p 27017:27017. But when the express app is also running as an container inside docker how we are gonna do that. Because there will be no localhost that we can use.

- To solve this problem docker network comes to the picture.

- So what we do is, we first create a network.

	``` docker network create -d bridge my-network```

- Now we can run the containers with the network flag to connect them over that network.

	``` docker run -p 27017:27017 --name docker-mongo-container --net my-network -d mongo```

	``` docker run -p 3000:3000 --net my-network -e MONGO_URI=mongodb://docker-mongo-container:27017/testDB express```

- Now the question will be how to the mongo url is created or used.

- We can use the container name inplace of the host (localhost) in the mongo url.

- And as they share the same network, they can communicate with each other.

- If you have running containers and you want to connect them to a network, you can do that by using the following command.

	``` docker network connect my-network container-name```

### Docker Compose

Now we will understand what docker compose is.

- In the above example we saw that to run only two containers we have to do a lot of things like creating a network, running the containers with the network flag, etc. And it will get more complicated when the number of environment variable and port mapping increases.

- To solve this we use docker compose. What do we do actually ?

- We create a file called `docker-compose.yml` in the root of the project. The file name can be anything. And there we write all the configuration for our docker containers.

- Here is the docker-compost.yml file for the above example

	```
	version: "3"
	
	services:
	
	mongo:
	
	image: mongo
	
	container_name: docker-mongo
	
	ports:
	
	- "27017:27017"
	
	networks:
	
	- mongo-network
	
	  
	
	express:
	
	image: subasmohanty/express:latest
	
	container_name: docker-express
	
	environment:
	
	- MONGO_URI=mongodb://docker-mongo:27017/testDB
	
	ports:
	
	- "3000:3000"
	
	networks:
	
	- mongo-network
	
	restart: always
	
	networks:
	
	mongo-network:
	
	driver: bridge
	
	```

- Now we will understand what this does.

1. `version: "3"` is the version of the docker-compose file.

2. `services:` is where we mention all of the images or no of containers that we want to run.

3. `mongo:` is the name of the service. We can give any name. same as express

4. `image:` is the image that we want to use. This will be used like docker run image

5. `container_name:` is the name of the container as it describes.

6. `ports:` is the port mapping. This will be used like docker run -p 27017:27017

7. `networks:` is the network that we want to use. This will be used like docker run --net my-network

8. All the environment variable are passed to environment key.

9. `restart: always` is used to restart the container if it stops. But why it is gonna stop and why it is only used in express not mongo.

This is because express container is dependent on mongo, so if mongo stops or has not initialized, but express got initialized first then it will not found the mongo url (as it has stopped or not initialized) and it will stop. So to restart it we use `restart: always`.

10. And lastly we are using `networks:` to describe the network config.

- Now to run the containers using docker-compose file, go to the root directory where docker-compose.yaml file is present and run :

	```docker compose up```