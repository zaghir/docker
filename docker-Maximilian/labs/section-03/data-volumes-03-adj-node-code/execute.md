# docker build -t feedback-node:volumes .

# docker run -d --rm --name feedback-app -p 3000:80 feedback-node:volumes

http://localhost:3000/feedback/test.txt
http://localhost:3000/feedback/test2.txt


# docker container stop feedback-app
# docker run -d --rm --name feedback-app -p 3000:80 feedback-node:volumes
http://localhost:3000/feedback/test2.txt


# docker volume ls
DRIVER    VOLUME NAME
local     cd63cd7000be79e646f80dbd84f4b6b7edaa864fb990ab15d64ac486ba08544a

# docker rmi feedback-node:volumes
Untagged: feedback-node:volumes
Deleted: sha256:aaf31884ce8138050180e0fc4b33cd310ccbb89365bbb9d08cc7c7fa5337feac


remove  VOLUME [ "/app/feedback" ]  in docker file 
we create an image again 
# docker build -t feedback-node:volumes .

we create container with named volume 
# docker run -d --rm --name feedback-app -p 3000:80 -v feedback:/app/feedback feedback-node:volumes

# docker volume ls
DRIVER    VOLUME NAME
local     feedback


# docker container ls
CONTAINER ID   IMAGE                   COMMAND                  CREATED              STATUS              PORTS                  NAMES
2609efc1532b   feedback-node:volumes   "docker-entrypoint.s…"   About a minute ago   Up About a minute   0.0.0.0:3000->80/tcp   feedback-app

# docker container stop feedback-app 

volume stile there unlike anonymous volume 
# docker volume ls
DRIVER    VOLUME NAME
local     feedback



We saw, that anonymous volumes are removed automatically, when a container is removed.

This happens when you start / run a container with the --rm option.

If you start a container without that option, the anonymous volume would NOT be removed, even if you remove the container (with docker rm ...).

Still, if you then re-create and re-run the container (i.e. you run docker run ... again), a new anonymous volume will be created. So even though the anonymous volume wasn't removed automatically, it'll also not be helpful because a different anonymous volume is attached the next time the container starts (i.e. you removed the old container and run a new one).

Now you just start piling up a bunch of unused anonymous volumes - you can clear them via docker volume rm VOL_NAME or docker volume prune.
