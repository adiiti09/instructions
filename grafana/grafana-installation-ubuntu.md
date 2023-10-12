# Grafana Installaton on Ubuntu 22.04

### Install the prerequisite packages

    sudo apt-get install -y apt-transport-https software-properties-common wget

### Import the GPG key

    sudo mkdir -p /etc/apt/keyrings/
    wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null

### Aadd a repository for stable releases

    echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

### update the list of available packages

    sudo apt update

### Install Grafana OSS

    sudo apt install grafana

# Starting Grafana service with systemd

### To start the service, run the following commands

    sudo systemctl daemon-reload
    sudo systemctl start grafana-server
    sudo systemctl status grafana-server

### To verify that the service is running, run the following command

    sudo systemctl status grafana-server

### To configure the Grafana server to start at boot, run the following command
    sudo systemctl enable grafana-server.service

