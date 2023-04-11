connect to docker https://hub.docker.com/

create a new repository like node-hello-word 

rebuild image by adding the same tag created by docker-hub  like => zaghir/node-hello-word
or colone image with the new name

docker images
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
gols         latest    2eefdd26b64e   55 minutes ago   1.01GB


docker tag gols:latest zaghir/node-hello-word


docker images
REPOSITORY               TAG       IMAGE ID       CREATED          SIZE
gols                     latest    2eefdd26b64e   56 minutes ago   1.01GB
zaghir/node-hello-word   latest    2eefdd26b64e   56 minutes ago   1.01GB

# push image 

# docker login 
zaghir

docker push zaghir/node-hello-word
latest: digest: sha256:a318ffc9b89d653eb64cd90c08d9df7fff0c296aca490cc1afd03705ad3cd129 size: 3047

docker logout


# docker pull node
Using default tag: latest
latest: Pulling from library/node
32fb02163b6b: Already exists
167c7feebee8: Already exists
d6dfff1f6f3d: Already exists
e9cdcd4942eb: Already exists
ca3bce705f6c: Already exists
4f4cf292bc62: Already exists
8347f8b4b86b: Already exists
c5f20f1b0856: Already exists
d220dfa3e187: Already exists
Digest: sha256:83841d113e09345a28b146e431f15b062341c5449218e501ba45ef8f9cff6049
Status: Downloaded newer image for node:latest
docker.io/library/node:latest

# docker images
REPOSITORY               TAG       IMAGE ID       CREATED       SIZE
gols                     latest    2eefdd26b64e   6 hours ago   1.01GB
zaghir/node-hello-word   latest    2eefdd26b64e   6 hours ago   1.01GB
node                     latest    fe9a4b9e181a   2 weeks ago   999MB

# docker rmi zaghir/node-hello-word
Untagged: zaghir/node-hello-word:latest
Untagged: zaghir/node-hello-word@sha256:a318ffc9b89d653eb64cd90c08d9df7fff0c296aca490cc1afd03705ad3cd129

# docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
gols         latest    2eefdd26b64e   6 hours ago   1.01GB
node         latest    fe9a4b9e181a   2 weeks ago   999MB

# docker pull zaghir/node-hello-word
Using default tag: latest
latest: Pulling from zaghir/node-hello-word
Digest: sha256:a318ffc9b89d653eb64cd90c08d9df7fff0c296aca490cc1afd03705ad3cd129
Status: Downloaded newer image for zaghir/node-hello-word:latest
docker.io/zaghir/node-hello-word:latest

# docker images
REPOSITORY               TAG       IMAGE ID       CREATED       SIZE
gols                     latest    2eefdd26b64e   6 hours ago   1.01GB
zaghir/node-hello-word   latest    2eefdd26b64e   6 hours ago   1.01GB
node                     latest    fe9a4b9e181a   2 weeks ago   999MB


# docker container run -d --rm  --name golsapp -p 3000:80 zaghir/node-hello-word
