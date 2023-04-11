remove all container not used
# docker container prune

remove all volumes not used
# docker volume prune

remove all network not used 
# docker network prune

remove all image 
# docker image prune -a 


create network 
# docker network create gols-net

# docker run --name mongodb --rm -d -p 27017:27017 mongo 

publing in the network 
# docker run --name mongodb --rm -d --network gols-net  mongo 