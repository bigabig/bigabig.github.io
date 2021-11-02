---
layout: post
title:  "VS Code: Develop in remote docker container"
date:   2021-11-02 14:00:00 +0100
categories: vscode docker
---

Goals:
- Use VS Code as IDE
- Develop in a docker container
- The docker container runs on a remote server

Benefits:
- All features of VS Code IDE
- Development environment is a docker container: easy to setup, easy to share, no need to install dependencies locally
- No resources of the local machine are used, all computations are done on the remote server that possibly has a lot of computational power

Requirements:
- Any GitHub project (you can also create a new one ofc)
- Install docker on local machine
- Install VS Code on local machine
- Install Docker extension for VS Code
- Install Remote - Containers extension for VS Code

Step 1: Configure ssh connection to remote server
```
# Generate a public/private key pair for SSH authentication
$ ssh-keygen

# Add generated key to the ssh-agent
$ ssh-add ~/.ssh/my_key

# Make sure that identity is available to the agent
$ ssh-add -l

# Copy the public key to the remote server
$ ssh-copy-id -i ~/.ssh/my_key user@remoteserver

# Make sure that you can connect to remote server without password
$ ssh user@remoteserver
```

Step 2: Create a docker context
```
$ docker context create my-remote-docker-machine --docker "host=ssh://user@remoteserver:port"

# Make sure that the context works: this should list all docker containers running on the remote server
$ docker context use my-remote-docker-machine
$ docker ps
```
In VS Code, you can now use the Command "Docker Context: Use" to select the my-remote-docker machine.

Step 3: Setup the project
```
# On your local machine, clone your GitHub repository
$ git clone <repository>

# On the remote server, clone your GitHub repository
$ ssh user@remoteserver
$ mkdir Development
$ cd Development
$ git clone <repository>
```
Now, your GitHub project is available on both, local machine and remote server.

Step 4: Create .devcontainer.json
You can either create a new .devcontainer.json file using the VS Code command "Add Development Container Configuration Files" or just copy the file below in /.devcontainer/.
The file creates a Ubuntu 20 docker container with Git, Python 3.9 and Node 16 already installed.
It also installs some VS Code extensions that are helpful for develpoing Vue.js webapplications.
```
{
  "name": "Ubuntu",
  "runArgs": ["--init"],
  "build": {
    "dockerfile": "Dockerfile",
    // Update 'VARIANT' to pick an Ubuntu version: hirsute, focal, bionic
    // Use hirsute or bionic on local arm64/Apple Silicon.
    "args": { "VARIANT": "focal" }
  },

  // Set *default* container specific settings.json values on container create.
  "settings": {},

  // Add the IDs of extensions you want installed when the container is created.
  "extensions": [
    "sdras.vue-vscode-snippets",
    "esbenp.prettier-vscode",
    "octref.vetur",
    "dbaeumer.vscode-eslint"
  ],

  // Use 'forwardPorts' to make a list of ports inside the container available locally.
  "forwardPorts": [3000],

  // Use 'postCreateCommand' to run commands after the container is created.
  // "postCreateCommand": "uname -a",
  "workspaceFolder": "/workspace",
  "workspaceMount": "source=/home/<user>/Development/<repository>/,target=/workspace,type=bind,consistency=cached",

  // Comment out connect as root instead. More info: https://aka.ms/vscode-remote/containers/non-root.
  "remoteUser": "root",
  "features": {
    "git": "os-provided",
    "node": "16",
    "python": "3.9"
  }
}
```

Step 5: Start developing
Now use the VS Code command "Reopen in Container". This command will now create a new Docker container based on the .devcontainer.json and Dockerfile on the remote server. 
On first execution, this will take a while.
Once finished, you are automatically connected to the remote server and can start developing!
