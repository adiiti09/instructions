# Playbook to install apache webserver on Ubuntu 
## Create a file **install_apache.yml** and put the following content

    - hosts: all
      tasks:
      - name: install httpd package
        yum: name=httpd state=latest
      - name: start and enable httpd service
        service: name=httpd state=restarted enabled=yes
    
## Execute above playbook

    ansible-playbook install_apache.yml -b
        

