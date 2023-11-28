Check if java (preferably jdk) is available before installing jenkins

    java -version

If you get an error like Command 'java' not found, you can install java using the below command

    sudo apt install openjdk-11-jdk

Copy GPG keys for the Jnekins repo
    curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/ jenkins-keyring.asc > /dev/null

Add repo signed by the keys added above
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

Update local repo cache
    sudo apt update

Install Jenkins
    sudo apt install jenkins
