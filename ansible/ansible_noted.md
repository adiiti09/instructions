# Playbook to install apache webserver on Ubuntu 

`- hosts: all`
  tasks:
  - name: install httpd package
    yum: name=httpd state=latest
  - name: start and enable httpd service
    service: name=httpd state=restarted enabled=yes
    

