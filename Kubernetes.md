
# commands to set up k8s 
    sudo apt-get update
    sudo apt install python3-pip
    sudo pip3 install awscli --upgrade --user
    sudo rm /usr/local/bin/kubectl
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
    sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
    sudo apt install unzip
    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
    unzip awscliv2.zip 
    sudo ./aws/install 
    ARCH=amd64 
    PLATFORM=$(uname -s)_$ARCH
    curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"
    tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz 
    sudo mv /tmp/eksctl /usr/local/bin

Minikube installation: on LINUX

        curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
        sudo install minikube-linux-amd64 /usr/local/bin/minikube
        minikube start
        
                
Install and Set Up kubectl on Linux
Download the latest release with the command:

        curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
Validate the binary:
1. Download the kubectl checksum file:

        curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
2. Validate the kubectl binary against the checksum file:

       echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
  output: kubectl: OK

Install kubectl

        sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
        

setup eks cluster

    apiVersion: eksctl.io/v1alpha5
    kind: ClusterConfig
    metadata:
      name: kh-cluster
      region: us-east-1
    nodeGroups:
    - name: kh-workers
      instanceType: t2.small
      desiredCapacity: 2
      volumeSize: 20
    availabilityZones: ['us-east-1a', 'us-east-1b']






