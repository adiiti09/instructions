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

# Roles Example

Create 3 roles as follows:
  - prerequisites
  - mongodb
  - apache

    ansible-galaxy init prerequisites
    ansible-galaxy init mongodb
    ansible-galaxy init apache

        

