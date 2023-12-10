# LAMPhp82 on Docker

This file is also available in its version in [Brazilian Portuguese](./README-pr_br.md)

The environment defined here will instantiate three containers, one containing Apache
with the PHP 8.2 language working in FastCGI, another with the database
MySQL Server 8 and the last one with mailhog. The php instance will
make use of the current directory to be the base for the files served in the
Apache environment, html will be processed as conventional files by apache,
php files will be interpreted by php and served by apache afterwards. PHP is
configured for use with xDebug3 which will be available in port 9003.

MySQL Server is configured in a restrictive way (like most of shared servers
on the internet) and was inspired by the DigitalOcean configuration. The script
will create a database with the name configured in the DB_DATABASE parameter, a user
for operation of this database, according to the DB_USER variable that will use the
password defined in the DB_PASSWORD variable and access authority from any host.

Mailhog does not have any change to its default settings, it is an email wrapper
very useful for development environments. (https://mailtrap.io/blog/mailhog-explained/)

Docker-compose.yml variable settings can be changed from the `.env`  file available
in the same folder as docker-compose.yml.

To run the image you must download the "yml" file from this directory, create a
directory with the name "storage/docker" and inside it create the mysql folder.
All these folders must have authorization for reading and writing by the user
who will execute the docker command on the host machine. then you may create the
web instance by running "docker-compose up", which will make available
the environment for its use.

As you run "docker-compose up", it in turn will start downloading the docker
images involved and only then will the creation of the instance itself begin.
We recommend that the first run is done without launching docker to the
background ("-d" option of docker-compose), this way you can follow
on screen the download of the files, as well as the progress of creating the
initial instance.

PS: Creating this instance on the first run after downloading the image will
take around 10min (or more, depending on your machine) but after running
output similar to the one shown below will be displayed. Just after the messages
the instance will be ready to use.

    2020-07-22 00:46:23 1 [Note] mysqld: ready for connections.
    Version: '5.6.48'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server (GPL)

# Recommendations

Use without restrictions

# MySQL

Running this command creates an instance with a specific MySQL database.

To connect the created database use the parameters below:
* **HOST**: localhost
* **PORT**: 3306
* **DATABASE**: database_local
* **USERNAME** someuser
* **PASSWORD**: 123456

If you want to connect directly via the command line, use as follows:

```bash
docker exec -it LAMPhp82_db bash -c "mysql"
```

##PHP

###xDebug

For xdebug to work in Visual Studio Code you need to select a
debug configuration for PHP and add it to the launch.json file created for
the debugger the following variables:

```json
    "pathMappings": {
        "/app": "${workspaceFolder}"
    },
```

To make it even easier, we added a launch.json file to the project that is in the
".vscode" directory