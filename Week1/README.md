# Introduction

# What is MLOps?

Machine Learning engineering is not just about running experiments, but to realize its value in the real world scenarios. MLOps is a set of principles and practices for efficient management of end-to-end ML lifecycle from experiments to productionization.

**MLOps -**

- enables version management of both data as well as model artifacts.
- operationalises the development and release cycle of ML models in CICD ecosystem
- helps to monitor the performance of models in production to maintain effectiveness

# Environment Set up

This section is for outlining steps for configuring development environment with preference to Linux OS. For that matter, we are renting an Ubuntu server on AWS and setting up the environment to suit our need.

Note: I am on Windows Laptop, hence all the configurations done locally are pertaining to Windows OS only.

## Step 1: Spin up EC2 Instance

- Go to AWS Console to spin up an EC2 instance of Ubuntu flavour of t2.xlarge size.
- Download the secret access keys (.pem file)
- Take a note of the public IP

## Step 2: Connect to Ubuntu EC2 server

- [Optional] Move .pem secret access keys file to .ssh folder in home directory
- Execute the following command from .ssh directory to change the permission of .pem file to protect it
  ```sh
  chmod 400 downloaded_pem_file
  ```
- Execute the following command to connect to the server
  ```sh
  ssh -i pem_file ubuntu@public_ip
  ```
- For ease of connecting the server add the connection details in config file in .ssh directory.
  ```sh
  nano ~/.ssh/config
  ```
- If config file is missing you can create a new one

  ```sh
  touch config
  ```

  Add the following and save it.

  ```
  Host short-name-of-your-choice
       Hostname public-ip-of-ec2
       User ubuntu
       IdentityFile path-to-.pem-file
       StrictHostKeyChecking no
  ```

  ```
  root@MrRobot:~/llmzoomCamp# cat ~/.ssh/config
  Host zoom-host
     Hostname 3.144.127.187
     User ubuntu
     IdentityFile ~/llmzoomCamp/llm-zoomcamp.pem
     StrictHostKeyChecking no
  ```

```

  root@MrRobot:~/llmzoomCamp# ssh zoom-host
  Welcome to Ubuntu 24.04.3 LTS (GNU/Linux 6.14.0-1015-aws x86_64)

  * Documentation:  https://help.ubuntu.com
  * Management:     https://landscape.canonical.com
  * Support:        https://ubuntu.com/pro
```

Now run `ssh short-name-of-your-choice` to quickly connect to the ubuntu server.

## Step 3: Configure Ubuntu server

### Install Anaconda

- Visit Anaconda website to get the download link for Linux (x86) version and execute the following to download the file in the server.

  ```sh
  wget https://repo.anaconda.com/archive/Anaconda3-2025.06-0-Linux-x86_64.sh
  ```

- Run the following command to install the downloaded file
  ```sh
  bash Anaconda3-2025.06-0-Linux-x86_64.sh
  ```
  If required, logout and re-login to the server.

### Install Docker

- Next we install Docker. However if you run into "Package ‘docker.io’ has no installation candidates" error just update the system first and then try installing again.
  ```sh
  sudo apt update
  sudo apt install docker.io
  ```
- To run without sudo, add your user to the docker user group.
  ```sh
  sudo groupadd docker
  sudo usermod -aG docker $USER
  ```

### Install docker-compose

- Create a separate directory to install docker compose.
  ```sh
  mkdir soft
  cd soft
  ```
- To install Docker Compose get the latest release version for your OS (https://github.com/docker/compose -> Releases -> Assets) and make it executable.

  ```sh
  wget link-from-docker-compose-github -o docker-compose
  chmod -x docker-compose
  ```

  ```
  wget https://github.com/docker/compose/releases/download/v2.40.3/docker-compose-linux-x86_64
  chmod -x docker-compose
  ```

- To ensure docker-compose is called from soft directory from wherever we call, we need to edit .bashrc file.
  ```sh
  nano ~/.bashrc
  export PATH="${HOME}/soft:${PATH}"
  source .bashrc
  ```
  If required, logout and re-login to the server.

### Run Docker

- To verify that docker setup the following should run successfully.

```sh
  docker run hello-world
  sudo docker run hello-world
```

### VS Code Setup

- Install "Remote - SSH" extension in VS Code
- Click on "Open a Remote Window" icon on bottom-left corner
- From dropdown select "Connect to Host" and then select Linux. That opens a new VSCode window.

  - Permission issue fix terminal in windows 'PowerShell run as Admin'

```bash



# Replace 'path\to\your\key.pem' with the actual path to your file

$pemFilePath = "D:\Work\ML\MLOps\Demo\llm-zoomcamp.pem"


# Reset permissions to default and remove inheritance

icacls.exe "$pemFilePath" /reset

# Grant full control to the current user

icacls.exe "$pemFilePath" /grant:r "$($env:username):(F)"

# Remove permissions for other groups and users (adjust as needed)

## icacls.exe "$pemFilePath" /remove:g "Authenticated Users" BUILTIN\Administrators BUILTIN Everyone System Users

```

asd

```bash

PS C:\Windows\System32> icacls "D:\Work\ML\MLOps\Demo\llm-zoomcamp.pem" /inheritance:r
processed file: D:\Work\ML\MLOps\Demo\llm-zoomcamp.pem
Successfully processed 1 files; Failed processing 0 files
PS C:\Windows\System32> icacls "D:\Work\ML\MLOps\Demo\llm-zoomcamp.pem" /inheritance:r
processed file: D:\Work\ML\MLOps\Demo\llm-zoomcamp.pem
Successfully processed 1 files; Failed processing 0 files
PS C:\Windows\System32> icacls "D:\Work\ML\MLOps\Demo\llm-zoomcamp.pem" /grant:r "$($env:USERNAME):F"
processed file: D:\Work\ML\MLOps\Demo\llm-zoomcamp.pem
Successfully processed 1 files; Failed processing 0 files
PS C:\Windows\System32> icacls "D:\Work\ML\MLOps\Demo\llm-zoomcamp.pem" /remove "Authenticated Users"
processed file: D:\Work\ML\MLOps\Demo\llm-zoomcamp.pem
Successfully processed 1 files; Failed processing 0 files
PS C:\Windows\System32> icacls "D:\Work\ML\MLOps\Demo\llm-zoomcamp.pem"
D:\Work\ML\MLOps\Demo\llm-zoomcamp.pem MRROBOT\risar:(F)

Successfully processed 1 files; Failed processing 0 files
PS C:\Windows\System32>
```

- In terminal clone MLOps-Zoomcamp project

  ```sh
  git clone https://github.com/DataTalksClub/mlops-zoomcamp.git
  ```

- Create a notebooks folder

  ```sh
  mkdir notebooks
  cd notebooks
  ```

- The notebooks are hosted on the server. However to access them locally we need to do the port forwarding that can be easily done in VSCode. Open Ports section next to terminal in VSCode and enter 8888 as port for source and enter. This will add the port to allow traffic.
- Next open jupyter notebook
  ```sh
  jupyter notebook
  ```

**Voila!!! You are done with the configuration**

# Important

Do not forget to stop the EC2 instance if not in use.

Go to terminal section select port forwarding and paste the URL generated
above in browser

```
http://127.0.0.1:8888/tree?token=aaba32723bce5d2e8dc11c2e0ebd9e6874e1c966c302921a
```
