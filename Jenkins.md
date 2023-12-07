Insallation of Jenkins over UBUNTU
Step 1: Update the System
 
    sudo apt-get update -y && sudo apt-get upgrade -y
Step 2: Install Java

    sudo apt install openjdk-11-jdk -y
Step 3: Install Jenkins (add the Jenkins repository and Key since they are not added by default in Ubuntu 22.04)

    curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null
    
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null

 Step 4:  Update the system and install Jenkins:

    sudo apt update -y
    sudo apt install jenkins -y
 Step 5: start and enable the Jenkins service:

    sudo systemctl start jenkins && sudo systemctl enable jenkins
