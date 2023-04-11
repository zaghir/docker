
# docker build -t feedback-node:volumes .

we create container with named volume 

 -v feedback:/app/feedback  => named volume
 -v "/c/docker/docker-Maximilian/labs/section-03/data-volumes-04-bindmounts:/app:ro"  =>  bind mounts  and read only
 -v /app/node_modules feedback-node:volumes => anonymous

# docker run -d --rm --name feedback-app -p 3000:80 -v feedback:/app/feedback -v "C:\docker\docker-Maximilian\labs\section-03\data-volumes-04-read-only:/app:ro" -v /app/node_modules -v /app/temp feedback-node:volumes

553779298b78a1b79fed42f54b650dd12428893e516774d76eb1e0fc4e1e3a45


# restart docker is you have a problems 

Like that 
e123be514d176b6290c9a98e1f2c20c3d98a78e4ceb8680d1e979366947c55a0
docker: Error response from daemon: failed to create shim task: OCI runtime create failed: runc create failed: unable to start container process: error during container init: error mounting "/var/lib/docker/volumes/fa93ad21a51520c6e447992ef209ae9041d6c9f264ff384c1b66bc0b0899d040/_data" to rootfs at "/app/node_modules": mkdir /var/lib/docker/overlay2/7947221390d08a6102b23a1ee567a4ec223dfe0f9c1d7b007c8e494805f9baae/merged/app/node_modules: read-only file system: unknown.

                                                                                                
# docker container ls
CONTAINER ID   IMAGE                   COMMAND                  CREATED         STATUS         PORTS                  NAMES
553779298b78   feedback-node:volumes   "docker-entrypoint.s…"   3 minutes ago   Up 3 minutes   0.0.0.0:3000->80/tcp   feedback-app


We create 3 volumes 
type_volume             commande   
named volume           -v feedback:/app/feedback     
bind  mount volume     -v "C:\docker\docker-Maximilian\labs\section-03\data-volumes-04-read-only:/app:ro" 
anounymous volume      -v /app/node_modules 
anounymous volume      -v /app/temp 

# docker volume ls
DRIVER    VOLUME NAME
local     7635bf9dd808caf7a4b6aa0582204850db40f9c8c9bdad50c9ad2beeccd577ca
local     da363f5b9936cffc0811cb08322d8f17c9addea588ac02a58181e355cb60d2fc
local     feedback


# docker volume create --help 

Usage:  docker volume create [OPTIONS] [VOLUME]
Create a volume
Options:
  -d, --driver string   Specify volume driver name (default "local")
      --label list      Set metadata for a volume
  -o, --opt map         Set driver specific options (default map[])


# docker volume create feedback-files 

 # docker run -d --rm --name feedback-app -p 3000:80 -v feedback-files:/app/feedback -v "C:\docker\docker-Maximilian\labs\section-03\data-volumes-04-read-only:/app:ro" -v /app/node_modules -v /app/temp feedback-node:volumes



 # docker volume ls
DRIVER    VOLUME NAME
local     7635bf9dd808caf7a4b6aa0582204850db40f9c8c9bdad50c9ad2beeccd577ca
local     da363f5b9936cffc0811cb08322d8f17c9addea588ac02a58181e355cb60d2fc
local     feedback
local     feedback-files

# docker volume inspect feedback
[
    {
        "CreatedAt": "2023-03-21T08:28:43Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/feedback/_data",
        "Name": "feedback",
        "Options": null,
        "Scope": "local"
    }
]

# docker volume rm feedback
Error response from daemon: remove feedback: volume is in use - [553779298b78a1b79fed42f54b650dd12428893e516774d76eb1e0fc4e1e3a45]

you should to remove container 

remove all volume unsued
# docker volume prune

