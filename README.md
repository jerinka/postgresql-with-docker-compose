# PostgreSQL with Docker-Compose 
Reference material for https://medium.com/@zhao.li/how-to-understand-building-images-with-docker-compose-24cbdbc0641f

Prerequisites
-------------
1. install docker
1. install docker-compose
1. install git
1. clone repository: `git clone --recursive https://github.com/zhao-lin-li/postgresql-with-docker-compose.git`

Getting Started
---------------
1. start service: `docker-compose up`

## Connect to the Database

There are multiple ways of connecting to the database container. In this example, we will drop into the database container and use the psql client software that is already installed in the database container.

```
docker-compose run database bash # drop into the container shell
database# psql --host=database --username=unicorn_user --dbname=rainbow_database
Password for user unicorn_user: 
psql (12.0 (Debian 12.0-2.pgdg100+1))
Type "help" for help.
rainbow_database=#
```
When prompted to the password, enter the password we configured in our docker-compose.yml, e.g. magical_password.

## Create a Table

```
rainbow_database=# \d # verify table does already not exist
Did not find any relations.
rainbow_database=# CREATE TABLE color_table(name TEXT);
CREATE TABLE
rainbow_database=# \d # verify table is created
              List of relations
 Schema |    Name     | Type  |    Owner     
--------+-------------+-------+--------------
 public | color_table | table | unicorn_user
(1 row)
```

## Add and Read Data

```
rainbow_database=# SELECT * FROM color_table; -- verify record does not already exist
 name 
------
(0 rows)
rainbow_database=# INSERT INTO color_table VALUES ('pink'); -- be sure to use single quotes
INSERT 0 1
rainbow_database=# SELECT * FROM color_table; -- verify record is created
 name 
------
 pink
(1 row)
```




