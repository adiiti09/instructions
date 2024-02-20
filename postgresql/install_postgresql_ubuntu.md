# Postgresql installation on Ubuntu

## Update and refresh local package index
        sudo apt update

##  Install the Postgres package along with a -contrib package that adds some additional utilities and functionality
        sudo apt install postgresql postgresql-contrib

## The installation procedure created a user account called postgres that is associated with the default Postgres role
## Switch to that user
        sudo -i -u postgres

## Then you can access the Postgres prompt by running:
        psql