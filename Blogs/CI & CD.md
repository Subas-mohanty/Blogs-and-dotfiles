### Continuous Integration(CI)

- CI is a process in which we can ran some test when a push/pull request/commit is made to the repository.

- Suppose we want to check if the linting is successful or not, we can run the linting test on the code.

#### How do we do that ?

1. Create a folder named .github in the root directory of the repository.

2. Create a folder named workflows inside the .github folder.

3. Create a file named build.yml (this name can be anything) inside the workflows folder.

4. Write the test code for the CI in the build.yml file.

- Here is an example file that checks the build is successful or not

  

```

# this is the name that will be shown in the check for ex : Build on PR / Build the project (pull_request) Successful in 35s

name: Build on PR

on:

pull_request:

branches:

# this runs in all branches,

# we can specify branches here like this

# - main

# - master

- '*'

jobs:

build:

name: Build the project

runs-on: ubuntu-latest

# this uses thing is, actually it is getting from github, this actually means, clone the repo, setup the code and setup node js thing is, it is downloading and setting path of node js in the remote ubuntu machine that this build is running on

steps:

- name: Checkout code

uses: actions/checkout@v3

- name: Setup Node.js

uses: actions/setup-node@v3

with:

node-version: '20'

- name: Install dependencies

run: npm install

- name: Run Build

run: npm run build

```

- This will make sure everytime a pull request is made, the build is successful or not.

### Continuous Deployment(CD)

- CD is a process in which we can deploy the code to the server when push/commit to the main branch is made.

#### How do we do that ?

1. This is also same as CI. We have to create another file called deploy.yml in the workflows folder.

2. Write the deployment code in the deploy.yml file.

3. Steps to write CD.

1. Clone the repo

2. Dockerize it.

3. Push it to docker hub.

4. Pull the image and run it in the server(AWS)

- Here is an example file.

- In this file we are using docker. So we are dockerizing the app first pushing the docker image to docker hub and then we will pull and run the image in the AWS server.


```

name: Build and Deploy to Docker Hub

on:

push:

branches:

- master

  
jobs:

build-and-push:

runs-on: ubuntu-latest

steps:

- name: Check Out Repo

uses: actions/checkout@v2

  

- name: Log in to Docker Hub

uses: docker/login-action@v1

with:

username: ${{ secrets.DOCKER_USERNAME }}

password: ${{ secrets.DOCKER_PASSWORD }}


- name: Build and Push Docker image

uses: docker/build-push-action@v2

with:

context: .

file: ./Dockerfile

push: true

tags: 100xdevs/web-app:latest # Replace with your Docker Hub username and repository


- name: Verify Pushed Image

run: docker pull 100xdevs/web-app:latest # Replace with your Docker Hub username and repository


```

  
- The secret.docker user name and password should be added in the repository secrets. In Actions -> Secrets -> New Repository Secret.

- This will make sure that the code is deployed to the server when a push is made to the main branch.