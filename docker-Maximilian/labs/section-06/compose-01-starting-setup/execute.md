# docker image prune 
# docker network prune
# docker container prune 


# docker-compose up -d

force to build images if we have a changes 
# docker-compose up -d --build 

build only images 
# docker-compose build 
# docker container ls -a 

CONTAINER ID   IMAGE                                COMMAND                  CREATED         STATUS         PORTS                    NAMES
e022ce29cede   compose-01-starting-setup-frontend   "docker-entrypoint.s…"   6 minutes ago   Up 6 minutes   0.0.0.0:3000->3000/tcp   compose-01-starting-setup-frontend-1
e32c20e206d3   compose-01-starting-setup-backend    "docker-entrypoint.s…"   6 minutes ago   Up 6 minutes   0.0.0.0:80->80/tcp       compose-01-starting-setup-backend-1
efc14692e7dd   mongo                                "docker-entrypoint.s…"   6 minutes ago   Up 6 minutes   27017/tcp                compose-01-starting-setup-mongodb-1

# docker network ls
NETWORK ID     NAME                                 DRIVER    SCOPE
2f6f1d305055   bridge                               bridge    local
3c7e1a2e0ea2   compose-01-starting-setup_gols-net   bridge    local
77bb2b63511c   host                                 host      local
0c073848789e   none                                 null      local

# docker-compose down

remove data volume also
# docker-compose down -v 


