```
docker info
```
```
docker version
```
```
docker container run --publish 80:80 nginx
docker container run --publish 80:80 --name <name> --detach  <Image_Name>
docker container run --publish 80:80 --detach nginx
```
```
docker container ls
docker container ls -a
```
```
docker container log <container_name>|<container_id>
docker container stop  idContainer
```
```
docker container rm  idContainer
docker container rm -f idContainer          -force
```
```
docker build -f <path_of_docker_file>
```
see process running inside the container
------------------------------
```
docker container top <container_id>

UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                12281               12255               0                   09:32               ?                   00:00:00            nginx: master process nginx -g daemon off;
uuidd               12335               12281               0                   09:32               ?                   00:00:00            nginx: worker process
uuidd               12336               12281               0                   09:32               ?                   00:00:00            nginx: worker process
```

see all process in the host system
------------------------------
```
ps aux | grep nginx
```
Remove all unused container
------------------------------
```
docker container rm <space seprated container ids>
```

run a nginx,a mysql ,and apache server
------------------------------
```
docker container run -d -p 80:80 --name proxy  nginx
docker container run -d -p 8080:80 --name apache  httpd
docker container run -d -p 3306:3306 --name mysqldb --env MYSQL_RANDOM_ROOT_PASSWORD=yes mysql
docker container logs mysqldb           
and get password from log     like this [Note] [Entrypoint]: GENERATED ROOT PASSWORD: /3CISVdR5qXas/H3u9QVL7fWRl2rxxxW
```
```
docker container ls -a
CONTAINER ID   IMAGE                    COMMAND                  CREATED             STATUS                      PORTS                                                  NAMES
78768d5e7e12   mysql                    "docker-entrypoint.s…"   2 minutes ago       Up 2 minutes                0.0.0.0:3306->3306/tcp, :::3306->3306/tcp, 33060/tcp   mysqldb
d5db06223762   httpd                    "httpd-foreground"       5 minutes ago       Up 5 minutes                0.0.0.0:8080->80/tcp, :::8080->80/tcp                  apache
97f5a9b4fda2   nginx                    "/docker-entrypoint.…"   5 minutes ago       Up 5 minutes                0.0.0.0:80->80/tcp, :::80->80/tcp                      proxy
```
```
docker container rm -f mysqldb apache proxy
```
Containers CLI monitoring & inspection
--------------------------------------------
```
docker container top <idContainer>| <name> Process List in one container

docker container inspect <idContainer>| <name>   detail off one container
docker container run -d -p 80:80 --name proxy  nginx
docker container inspect proxy

docker container stats   performance stats on all containers
```
ssh running container
--------------------------------------
```
docker container run -it <idContainer>       Run container interactivity  user can interact with container
docker container run --help
-i, --interactive                    Keep STDIN open even if not attached
keep a session open in terminal
-t, --tty                            Allocate a pseudo-TTY
allocat a sudo terminal in session
```

```
docker container run -it --name webproxy nginx bash           we support a bash
root@33bdcb128b2e:/# ls -lrt
total 72
drwxr-xr-x   2 root root 4096 Dec 11 17:25 home
drwxr-xr-x   2 root root 4096 Dec 11 17:25 boot
drwxr-xr-x   1 root root 4096 Feb 28 00:00 var
drwxr-xr-x   1 root root 4096 Feb 28 00:00 usr
drwxr-xr-x   2 root root 4096 Feb 28 00:00 srv
drwxr-xr-x   2 root root 4096 Feb 28 00:00 sbin
drwxr-xr-x   3 root root 4096 Feb 28 00:00 run
drwx------   2 root root 4096 Feb 28 00:00 root
drwxr-xr-x   2 root root 4096 Feb 28 00:00 opt
drwxr-xr-x   2 root root 4096 Feb 28 00:00 mnt
drwxr-xr-x   2 root root 4096 Feb 28 00:00 media
drwxr-xr-x   2 root root 4096 Feb 28 00:00 lib64
drwxr-xr-x   1 root root 4096 Feb 28 00:00 lib
drwxr-xr-x   2 root root 4096 Feb 28 00:00 bin
-rwxrwxr-x   1 root root 1202 Mar  1 13:59 docker-entrypoint.sh
drwxrwxrwt   1 root root 4096 Mar  1 14:00 tmp
drwxr-xr-x   1 root root 4096 Mar  1 14:00 docker-entrypoint.d
drwxr-xr-x   1 root root 4096 Mar 16 10:45 etc
dr-xr-xr-x 229 root root    0 Mar 16 10:45 proc
dr-xr-xr-x  13 root root    0 Mar 16 10:45 sys
drwxr-xr-x   5 root root  360 Mar 16 10:45 dev
root@33bdcb128b2e:/# exit
exit

docker container ls -a         STATUS = exit and COMMAND = bash  
CONTAINER ID   IMAGE                    COMMAND                  CREATED         STATUS                      PORTS     NAMES
33bdcb128b2e   nginx                    "/docker-entrypoint.…"   4 minutes ago   Exited (0) 52 seconds ago             webproxy
```

Changer anything inside runing container
------------------------------------------
```
docker container exec -it <idContainer>       open running container interactivity
```
The  docker exec command runs a new command in a running container

scenario
Start Nginx Docker Destro
Run command and create Directory inside the Running Container
Verify the New Directory
Download new Linux Alpine Destro
Use curl and view Facebook home page DOM in Alpine.

```
docker container run -d -p 80:80 --name webproxy  nginx
docker container exec -it 69ac9664b63e touch /tmp/yzr      create a file
docker container exec -it 69ac9664b63e bash                              --------- important
root@69ac9664b63e:/# cd /tmp
root@69ac9664b63e:/tmp# ls
yzr
root@69ac9664b63e:/tmp#

docker container run -it ubuntu bash
root@5466e64cfe89:/# ls -a
.  ..  .dockerenv  bin  boot  dev  etc  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@5466e64cfe89:/# curl www.facebook.com
bash: curl: command not found
root@5466e64cfe89:/# apt-get update
root@5466e64cfe89:/# apt-get install curl
root@5466e64cfe89:/# curl https://www.facebook.com
```


Explore Container Networks
-------------------------------
```
docker container run -p <host_port>:<docker_port> -d image
```

find the traffic and protocol on container
```
docker port <container_id>
docker port 69ac9664b63e

80/tcp -> 0.0.0.0:80
80/tcp -> :::80
```

Find Docker Container IP
```
docker inspect <container_id>
docker inspect 69ac9664b63e

"Networks": {
"bridge": {
"IPAMConfig": null,
"Links": null,
"Aliases": null,
"NetworkID": "4edb32c7a0e85a9176fef951c20c671f062b1f3c7fe80146a1456dd769b73ef4",
"EndpointID": "249d8998887c74b48c1aa3d7cf3e4bb4fea4f6b75e3faf0b7ab48c5530139c97",
"Gateway": "172.17.0.1",
"IPAddress": "172.17.0.2", <-------------------------------------
"IPPrefixLen": 16,
"IPv6Gateway": "",
"GlobalIPv6Address": "",
"GlobalIPv6PrefixLen": 0,
"MacAddress": "02:42:ac:11:00:02",
"DriverOpts": null
}
}
```

```
docker container inspect -f '{{.NetworkSettings.IPAddress}}' 69ac9664b63e         -f = filter
'172.17.0.2'
```

show all network
------------------------
```
docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
4edb32c7a0e8   bridge    bridge    local
927f1e7ea920   host      host      local
7d94f5874d5a   none      null      local
```

filter network
-----------------------
```
docker network ls -f driver=bridge
NETWORK ID     NAME      DRIVER    SCOPE
4edb32c7a0e8   bridge    bridge    local
```

To find all network Ids and Drivers
---------------------------------------
```
docker network ls --format "{{.ID}}: {{.Driver}}"
4edb32c7a0e8: bridge
927f1e7ea920: host
7d94f5874d5a: null
```

Insperct any network
---------------------
```
docker network inspect <network_id>
```

Create new network on host machine
-------------------------------------
```
docker network create <name>
docker network create mynetwork
```
```
docker network ls
NETWORK ID     NAME        DRIVER    SCOPE
4edb32c7a0e8   bridge      bridge    local
927f1e7ea920   host        host      local
9c1022ad3c1b   mynetwork   bridge    local        ----------
7d94f5874d5a   none        null      local
```

Create a bridge network
-------------------------------
```
docker network create -d bridge my-bridge-network
```

Connect network with container
---------------------------------
```
docker network connect network1 container1
or
docker container run -d --name my_nginx --network mynetwork nginx

docker container inspect my_nginx

docker network connect mynetwork webproxy

		docker network inspect mynetwork"Containers": {
            "69ac9664b63e699bacabbf4e4aa8d13d230bf865aafcf725ad2414c37d35cecd": {
                "Name": "webproxy",
                "EndpointID": "5332fbc785a7b0e49dbe1998a405214d449a204630d2fe503a1c5559400aeb4e",
                "MacAddress": "02:42:ac:12:00:03",
                "IPv4Address": "172.18.0.3/16",          ---------------
                "IPv6Address": ""
            },
            "8f878e848ea473f22fbdfc86a4a042c13ffb23547f21b6473e65546b8121fd0e": {
                "Name": "my_nginx",
                "EndpointID": "edc56c509c995e04dedf6bcb06e2f554e9781ae3c74c70bf4a8c419aeb6f225e",
                "MacAddress": "02:42:ac:12:00:02",
                "IPv4Address": "172.18.0.2/16",           ---------------
                "IPv6Address": ""
            }
        },

disconnect container from network
docker network disconnect <network_id> <container_id>
docker network disconnect bridge webproxy
```

Docker Images
------------------------------
```
detele image
docker image rm -f <image_id>
```
```
Download docker image
docker pull <image_name>
docker pull mysql
```
```
Pull specific version
docker pull <Image_name>:<Image_version>
docker pull mysql:5.7
```
```
List docker images
docker images

REPOSITORY                           TAG                                                     IMAGE ID       CREATED         SIZE
httpd                                latest                                                  6b8e87fff107   43 hours ago    144MB
mysql                                latest                                                  826efd84393b   7 days ago      521MB
ubuntu                               latest                                                  2b4cba85892a   12 days ago     72.8MB
nginx                                latest                                                  c919045c4c2b   2 weeks ago     142MB
```
```
Show image layers:
docker history <image_name>
docker history mysql
```
```
Tag image
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]

by default it tacks 'latest' tag when we don't specify docker image tag

docker tag nginx nginxtest
REPOSITORY                           TAG                                                     IMAGE ID       CREATED         SIZE
httpd                                latest                                                  6b8e87fff107   44 hours ago    144MB
mysql                                latest                                                  826efd84393b   7 days ago      521MB
ubuntu                               latest                                                  2b4cba85892a   12 days ago     72.8MB
nginx                                latest                                                  c919045c4c2b   2 weeks ago     142MB
```
```
docker images
REPOSITORY                           TAG                                                     IMAGE ID       CREATED         SIZE
httpd                                latest                                                  6b8e87fff107   44 hours ago    144MB
mysql                                latest                                                  826efd84393b   7 days ago      521MB
ubuntu                               latest                                                  2b4cba85892a   12 days ago     72.8MB
nginx                                latest                                                  c919045c4c2b   2 weeks ago     142MB
nginxtest                            latest                                                  c919045c4c2b   2 weeks ago     142MB ------------
```
```
docker tag mysql:5.7 mysqlyzr:test
```

```
Command to login :
docker login
docker login --username zaghir  --password ttoto
```
```
docker logout          for deleting token
```
```
Push Image on docker hub
docker image push USER/Image-name

docker image tag nginx zaghir/nginxtest      naming image correctecly  because our image is not official
or
docker image tag nginx zaghir/nginxtest:1.0.1
docker image push zaghir/nginxtest
or
docker image push zaghir/nginxtest:1.0.1

```

Dockerfile
-----------------------
```
Command to build image from dockerfile
docker image build -f <path_of_docker_file>

Docker build syntax
docker image build -t <image_name>:<tag_name> dir
-t : is to mention a tag to the image
image_name : the name of image
tag_name  : this is the tag you want to give to your image
dir : the directory where the docker file is present    dir = . for current director  or dir = path if not current directory
```
```
dockerfile
# Each instruction in this file generates a new layer that gets pushed to your local image cache
# The line below states we will base our new image on the Latest Official Ubuntu
FROM ubuntu:latest

# Identify the maintainer of an image
LABEL version="0.0.1"
LABEL maitainer="yzr@gmail.com"

# Update the image to the latest packages
RUN  apt-get update && apt-get upgrade -y

# Install NGINX to test.
RUN apt-get install nginx -y

# Expose port 80
EXPOSE 80

# Last is the actual command to start up NGINX within our Container
CMD [ "nginx", "-g", "daemon off;"]

create image
docker image build -t yzrnginx:0.0.1  C:\Users\yzaghir\Downloads

create container
docker run -d -p 4444:80 yzrnginx:0.0.1
```


Replace an existing index.html inside container
```
dockerfile
FROM nginx:latest

# Identify the maintainer of an image
LABEL version="0.0.1"
LABEL maitainer="yzr@gmail.com"

# Updateing the work DIR
WORKDIR /usr/share/nginx/html

# Replace Index.html with Custom file
COPY index.html index.html
COPY style.css style.css

create image
docker image build -t nginx-custom:0.0.1  C:\Users\yzaghir\Downloads\docker-notes

create container
docker run -d -p 4444:80 nginx-custom:0.0.1
```

Docker volumes
-----------------------------------------
```
docker inspect mysql

"Volumes": {
"/var/lib/mysql": {}
},
```

```
docker container run -d -p 3306:3306 --name mysqldb --env MYSQL_RANDOM_ROOT_PASSWORD=yes mysql
docker inspect mysqldb

"Mounts": [
{
"Type": "volume",
"Name": "c31921ace964838e5d4537b6a7514468f5fd9d1b611b8a198b78b396470d3fab",
"Source": "/var/lib/docker/volumes/c31921ace964838e5d4537b6a7514468f5fd9d1b611b8a198b78b396470d3fab/_data",
"Destination": "/var/lib/mysql",
"Driver": "local",
"Mode": "",
"RW": true,
"Propagation": ""
}
],
```
```
docker volume ls

DRIVER    VOLUME NAME
local     90ab9ed63e3f6b9d63b87051ed74996d1b9dc4393509ef0ccb5dac452f1029e5
local     c31921ace964838e5d4537b6a7514468f5fd9d1b611b8a198b78b396470d3fab

docker volume inspect 90ab9ed63e3f6b9d63b87051ed74996d1b9dc4393509ef0ccb5dac452f1029e5
[
{
"CreatedAt": "2022-03-16T10:18:03Z",
"Driver": "local",
"Labels": null,
"Mountpoint": "/var/lib/docker/volumes/90ab9ed63e3f6b9d63b87051ed74996d1b9dc4393509ef0ccb5dac452f1029e5/_data",
"Name": "90ab9ed63e3f6b9d63b87051ed74996d1b9dc4393509ef0ccb5dac452f1029e5",
"Options": null,
"Scope": "local"
}
]
```
```
create custom volume
docker run -d --name mysqldb2 -e MYSQL_ALLOW_EMPTY_PASSWORD=True --mount source=mysql-db,destination=/var/lib/mysql mysql
docker run -d --name mysqldb3 -e "MYSQL_ROOT_PASSWORD=mypassword" --mount source=mysql-db,destination=/var/lib/mysql mysql
```
```
docker container ls -a
CONTAINER ID   IMAGE                    COMMAND                  CREATED              STATUS                        PORTS                                                  NAMES
3e01ace5d24a   mysql                    "docker-entrypoint.s…"   About a minute ago   Up About a minute             3306/tcp, 33060/tcp                                    mysqldb3
697730d842ed   mysql                    "docker-entrypoint.s…"   16 hours ago         Up About a minute             3306/tcp, 33060/tcp                                    mysqldb2
0980a2977071   mysql                    "docker-entrypoint.s…"   17 hours ago         Up 25 seconds                 0.0.0.0:3306->3306/tcp, :::3306->3306/tcp, 33060/tcp   mysqldb
```
```
docker volume ls
DRIVER    VOLUME NAME
local     90ab9ed63e3f6b9d63b87051ed74996d1b9dc4393509ef0ccb5dac452f1029e5
local     c31921ace964838e5d4537b6a7514468f5fd9d1b611b8a198b78b396470d3fab
local     mysql-db
```
```
container mysqldb2 and  mysqldb3 use the same volume  mysql-db
```

bind mount
----------------
```
share strorage between host machine and container

Start nginx with bind mount
Run nginx

docker container run -d --name nginxbind --mount type=bind,source=$(pwd),target=/app nginx
docker container run -d --name nginxbind --mount type=bind,source=C:/Users/yzaghir/Downloads/docker-notes/d,target=/app nginx
$(pwd) = use the current directory , or hard code directory
traget = with directory in the container will be mounted
```
creete database in mysqldb
---------------------------------------------
```
docker run -d --name mysqldb -e "MYSQL_ROOT_PASSWORD=mypassword" --mount source=mysql-db,destination=/var/lib/mysql mysql
apt-get install mysql-client
mysql -u root -p mypassword -h 172.17.0.2 -P 3306

CREATE DATABASE testdb
use testdb;
CREATE TABLE Persons( personId int , lastName varchar(255) , firstName varchar(255) , address varchar(255) city(255));
insert  ;
commit ;
```

Docker compose
-----------------------------------------------------------------
```
Download the necessary files from github using the following command
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

Apply executable permissions to the binary:
sudo chmod +x /usr/local/bin/docker-compose
```
```
Verify Syntax:
docker-compose —version
```
```
Docker-compose.yml if default name of Yml file

Custom name can be used by command docker-compose.yml
docker-compose -f xxxx.yml
```
template.yml
----------------
```
version: '3' #Specifies the Compose file syntax version.

services: #service is the name for a “Container in production”
servicename: #container service name
image: #optional, specify if build specific
command: #optional, relmand CMD specified in image
environment: #optional, similar to -e in Docker run command
volumes: #optional, similar to --mount in docker run
servicename2:

volumes: #Optional, Mounts a linked path on the host machine that can be used by the container.

networks: #Optional, Same as Docker Network
```

Docker Compose : Starting MySQL and Wordpress containers
We will start with Docker Compose File
Prepare docker-compose.yml file
Save file and Run via command
```
docker-compose up -d
```
Verify Containers on Host Machine
Access WordPress in Browser

Down the Docker Containers via Docker Compose
```
docker-compose down
```

exemple
-----------
```
version: '3' #Version of YML file

services:
db:
image: mysql:5.7
volumes:
- db_data:/var/lib/mysql
restart: always
environment:
MYSQL_ROOT_PASSWORD: mypassword
MYSQL_DATABASE: wordpress
MYSQL_USER: wordpressuser
MYSQL_PASSWORD: wordpress

wordpress:
depend-on:
- db
image: wordpress:latest
ports:
- "8080:80"
restart: always
environment:
WORDPRESS_DB_HOST: db:3306
WORDPRESS_DB_USER: wordpressuser
WORDPRESS_DB_PASSWORD: wordpress

volumes:
db_data:
```
```
docker-compose up 
```
