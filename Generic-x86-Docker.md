This page guides you to install and run Autoware on the Intel x86 processor (64 bits) using Docker. For other platforms, such as NVIDIA DRIVE, please check [here](https://github.com/CPFL/Autoware/wiki/Docker) whether they are supported. The outline of this page is as follows.

1. Docker Setup
1. NVIDIA Docker Setup
1. Autoware Docker Setup

## Docker Setup
   You first need to build the Docker environment. If the following installation process does not work for you, please check [Docker's installation website](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/)

###   Old Docker Cleanup
   ```bash
   $ sudo apt-get remove docker docker-engine docker.io
   ```
   You are ready to move on the next step if all Docker packages are removed.

###  Docker CE Installation
   This time you may want to install Docker using the repository, though there are several other ways to install Docker.

####  Step 1: Repository Setup

   Do update on apt-get.
   ```bash
   $ sudo apt-get update
   ```
   Permit apt-get to access the repository.
   ```bash
   $ sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
   ```
   Add Docker's official GPG key docker.
   ```bash
   $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   ```
   Validate the key. If you see the fingerprint below, you are reay to move on the next step.
   ```bash
   $ sudo apt-key fingerprint 0EBFCD88

   pub 4096R/0EBFCD88 2017-02-22
   Key fingerprint = 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88
   uid Docker Release (CE deb)
   sub 4096R/F273FCD8 2017-02-22
   ```
   Install the repository.
   ``` bash
   $ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
   ```
#### Step 2: Docker CE Installation

   Update on apt-get.
   ``` bash
   $ sudo apt-get update
   ```
   Install the latest version of Docker CE.
   ``` bash
   $ sudo apt-get install docker-ce
   ``` 
   Validate the installation succeeded.
   ``` bash
   $ sudo docker run hello-world
   ``` 

## NVIDIA Docker Setup

You need to install Docker Plugin provided by NVIDIA in order to access NVIDIA GPUs from Docker Container.

If not already installed, Install CUDA drivers for your platform: [Linux](
https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#package-manager-installation)

Download the .deb file.
   ``` bash
   $ wget https://github.com/NVIDIA/nvidia-docker/releases/download/v1.0.1/nvidia-docker_1.0.1-1_amd64.deb
   ``` 
Install the downloaded .deb file.
   ``` bash
   $ sudo dpkg -i nvidia-docker_1.0.1-1_amd64.deb
   ``` 
Check if the nvidia-docker service exists.
   ``` bash
   $ systemctl list-units --type=service | grep -i nvidia-docker
   ``` 
If the above fails, check with
   ``` bash
   $ systemctl list-units --type=service | grep -i nvidia-docker-plugin
   ```
Install modprobe if even the above throws error
   ``` bash
   $ sudo apt-get install nvidia-modprobe
   ```
Check if the nvidia-docker service runs with
   ``` bash
   $ sudo nvidia-docker run --rm nvidia/cuda nvidia-smi
   ``` 
If the above does not run, check with
   ``` bash
   $ sudo nvidia-docker-plugin run --rm nvidia/cuda nvidia-smi
   ``` 
Note: If you run into the following error 
```bash
docker: Error response from daemon: OCI runtime create failed: container_linux.go:348: starting container process caused "exec: \"nvidia-smi\": executable file not found in $PATH": unknown.
```

Try Following these nvidia-docker [instructions](https://github.com/NVIDIA/nvidia-docker)

## Autoware Docker Setup

You can build the Autoware runtime environment using nvidia-docker. You may choose either to use the configuration of Docker Hub "as is" or to modify-then-recompile Dockerfile.

### Case 1: Using Docker Hub "As Is"
   Move to the docker/generic directory in Autoware.
   ``` bash
   $ git clone https://github.com/CPFL/Autoware.git
   $ cd Autoware/docker/generic
   ``` 
   If you use the versions older than 1.10.0, modify the last sentence of run.sh in that directory: `autoware-$1` --> `autoware/autoware:latest-kinetic`
   (*comment out does not work, need to modify)

   Run run.sh kinetic if you use Ubuntu 16.04, assuming that the default path is "/home/$USER/shared_dir".
   ``` bash
   $ sudo sh run.sh            # v1.10.0 and after
   $ sudo sh run.sh kinetic    # v1.9.1 and before
   ``` 
   If you want to use your own path, run build.sh kinetic with the path argument.
   ``` bash
   $ sudo sh run.sh -s {SHARED_DIR_PATH}         # v1.10.0 and after
   $ sudo sh run.sh kinetic {SHARED_DIR_PATH}    # v1.9.1 and before
   ```

### Case 2: Using modify-then-recompile Dockerfile
#### Step 1: Autoware Docker Build

   Move to the docker directory in Autoware.
   ``` bash
   $ git clone https://github.com/CPFL/Autoware.git
   $ cd Autoware/docker/generic
   ``` 
   Run build.sh kinetic if you use Ubuntu 16.04.
   ``` bash
   $ sudo sh build.sh kinetic
   ```
#### Step2: Autoware Docker Run
    
   Run run.sh kinetic if you use Ubuntu 16.04, assuming that the default path is "/home/$USER/shared_dir".
   ``` bash
   $ sudo sh run.sh -r "" -t autoware-kinetic    # v1.10.0 and after
   $ sudo sh run.sh kinetic                      # v1.9.1 and before
   ``` 
   If you want to use your own path, run build.sh kinetic with the path argument.
   ``` bash
   $ sudo sh run.sh -r "" -t autoware-kinetic -s {SHARED_DIR_PATH}    # v1.10.0 and after
   $ sudo sh run.sh kinetic {SHARED_DIR_PATH}                         # v1.9.1 and before
   ```