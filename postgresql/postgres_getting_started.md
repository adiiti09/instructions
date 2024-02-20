# Getting started with postgresql
## Once postgres is installted a user is created called postgres
## Switch to thet user
        sudo -i -u postgres

## Connect to postgres using the client psql
        psql

## To exit out of the PostgreSQL prompt, run the following
        \q

## Check version
        SELECT version();

## To show the current database
        SELECT current_database();

## Create a blank database to load the DB downloaded below
        CREATE DATABASE dvdrental;

## Download sample datbase
        wget https://www.postgresqltutorial.com/wp-content/uploads/2019/05/dvdrental.zip

## Unzip and load the db
        unzip dvdrental.zip
        pg_restore -d dvdrental dvdrental.tar

## Connect to the new db
        psql
        \c dvdrental

## Display all tables in the dvdrental database
        \dt