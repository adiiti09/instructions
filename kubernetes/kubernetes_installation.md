# Setting up 3 node Kubernetes Cluster

## Opening ports
### Master Node

  > Port Range      Purpose                 Used By

  > 6443*           Kubernetes API Server   All

  > 2379-2380       etcd server client API  kube-apiserver, etcd

  > 10250           Kubelet API             Self, Control Plane

  > 10251           kube-scheduler          Self

  > 10252           kube-controller-manager Self

### Worker Nodes

  > 10250           Kube API                Self, Control Plane

  > 30000-32767     NodePort Services       All

# Steps to be executed on both master and nodes

1. ssh to machines and switch user to root

        sudo -i

2. Configure persistent loading of modules
  
        tee /etc/modules-load.d/containerd.conf <<EOF
        overlay
        br_netfilter
        EOF

3. Load at runtime

        modprobe overlay
        modprobe br_netfilter

5. Update Iptables Settings

To ensure packets are properly processed by IP tables during filtering and port forwarding
Set the net.bridge.bridge-nf-call-iptables to ‘1’ in your sysctl config file

      tee /etc/sysctl.d/kubernetes.conf<<EOF
      net.bridge.bridge-nf-call-ip6tables = 1
      net.bridge.bridge-nf-call-iptables = 1
      net.ipv4.ip_forward = 1
      EOF

6. Reload configs
    
        sysctl --system

### Install docker and containerd on master and worker nodes
#### Docker is needed on master node as well because kubeadm uses containers (pods) to deploy etcd and the api server components

7. Install docker on all nodes by referring instruction given in 

      https://gitlab.com/nravinuthala/instructions/-/blob/main/docker/docker_ubuntu22.04_install_steps.md

      containerd config default> /etc/containerd/config.toml
    
      sed -e 's/SystemdCgroup = false/SystemdCgroup = true/g' -i /etc/containerd/config.toml

8. Restart containerd

      systemctl daemon-reload
    
      systemctl restart containerd
    
      systemctl enable containerd
    
      systemctl status containerd

# Follow the below instructions on both master and nodes

9.  Update the apt package index and install packages needed to use the Kubernetes apt repository

      apt update && apt install -y apt-transport-https ca-certificates curl

10. Download the Google Cloud public signing key 
  
      apt-key adv --keyserver keyserver.ubuntu.com --recv-keys B53DC80D13EDEF05

11. Add Kubernetes apt repository

      echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

12. Update apt package index, install kubelet, kubeadm and kubectl, and pin their version 
  
      KUBE_VERSION=1.26.0
    
      apt update
    
      apt install -y kubelet=${KUBE_VERSION}-00  kubeadm=${KUBE_VERSION}-00 kubectl=${KUBE_VERSION}-00 kubernetes-cni

13. To hold the installed packages at their installed versions, use the following command

      apt-mark hold kubelet kubeadm kubectl

14. Start the kubelet service is required on all the nodes

      systemctl enable kubelet && systemctl start kubelet

# Create a kubernetes cluster 
## Run the following on master

15. We have to initialize kubeadm on the master node

      kubeadm init --kubernetes-version=${KUBE_VERSION}

You will see output as shown below:

    Your Kubernetes control-plane has initialized successfully!

    To start using your cluster, you need to run the following as a regular user:

    mkdir -p $HOME/.kube
    sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
    sudo chown $(id -u):$(id -g) $HOME/.kube/config

    Alternatively, if you are the root user, you can run:

    export KUBECONFIG=/etc/kubernetes/admin.conf

    You should now deploy a pod network to the cluster.
    Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
    https://kubernetes.io/docs/concepts/cluster-administration/addons/

    Then you can join any number of worker nodes by running the following on each as root:


    kubeadm join 10.1.0.7:6443 --token vvq0a8.p96qxb50d80hof2a \
        --discovery-token-ca-cert-hash sha256:de183b2cb52b79ac63668587214ae320c1961939bfd2c7c0f2f7231a961ed7d3 

## Networking - Refer: 
  - https://github.com/kubeovn/kube-ovn
  - https://k21academy.com/docker-kubernetes/network-policies-in-kubernetes/

# Test the Cluster by running the following command on master

    kubectl get nodes

## The above command should show the node machine under list of nodes and status as ready. 
### If the status is shown as not ready, run the below command on master to setup network interface.

    kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml

After this the status of nodes should change to ready.


# To delete the cluster

    kubeadm reset

# To persist export KUBECONFIG command add it to the bottom of .bashrc

  do nano .bashrc and add export KUBECONFIG=/etc/kubernetes/admin.conf at the bottom and save it

# Ingress Steps

    https://www.golinuxcloud.com/steps-to-expose-services-using-kubernetes-ingress/
