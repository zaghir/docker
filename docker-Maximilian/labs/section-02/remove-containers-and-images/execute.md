# remove container 
docker container ps -a 

CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                      PORTS     NAMES
fa9ad3fb2560   6a29a044b793   "python rng.py"          13 minutes ago   Exited (0) 7 minutes ago              thirsty_sutherland
59c5d6780494   823ecbc1271e   "docker-entrypoint.s…"   20 hours ago     Exited (137) 17 hours ago             cool_franklin

docker container stop thirsty_sutherland cool_franklin 
docker rm thirsty_sutherland cool_franklin 




# remove image 
docker images 

REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
<none>       <none>    6a29a044b793   21 minutes ago   921MB
<none>       <none>    38bd46d1c3cc   17 hours ago     1.01GB
<none>       <none>    fd4c7501b805   17 hours ago     917MB
<none>       <none>    823ecbc1271e   20 hours ago     916MB

docker rmi 6a29a044b793 fd4c7501b805 38bd46d1c3cc

# remove all images 
docker image prune 


# remove automaticly a container 
docker container run -d -p 3000:80 --rm 823ecbc1271e

docker container stop <container>

docker container ps -a

CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

