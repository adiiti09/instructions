
### Update the apt package index and install packages needed to use the Kubernetes apt repository:
    sudo apt-get update
    sudo apt-get install -y apt-transport-https ca-certificates curl

### Download the public signing key for the Kubernetes package repositories. The same signing key is used for all repositories so you can disregard the version in the URL:
    curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

### Add the appropriate Kubernetes apt repository
### Please change the version as appropriate

    echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list


### Update apt package index, then install kubectl
    sudo apt-get update
    sudo apt-get install -y kubectl

### Once done verify as follows:
    kubectl version --output=json

