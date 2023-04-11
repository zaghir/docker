create image for backend 
# docker build -t gols-node .

run a container 
# docker run --name gols-backend --rm -d -p 80:80 --env-file ./.env  gols-node


publing in the network 
# docker run --name gols-backend --rm -d -p 80:80 --network gols-net  gols-node
 
# docker build -t gols-node .
