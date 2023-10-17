# Docker installation on Ubuntu

### Update repo
    sudo apt update

### Install prereqs
    sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
    
### Copy gpg keys needed to download docker
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

### Add docker repo to local repo list
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    
### Update local repo
    sudo apt update
    
### Installs docker community edition
    sudo apt install docker-ce
    
### Start docker service
    sudo systemctl status docker
    
### Add current user to docker group
    sudo usermod -aG docker ${USER}
    
### Try running the following command
    docker ps

#### You might get an error like below:
    permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/json": dial unix /var/run/docker.sock: connect: permission denied

### If you get above shown error run the command
    sudo chmod 666 /var/run/docker.sock

