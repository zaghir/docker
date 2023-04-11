# docker build -t favorites-node .

# docker container prune 

# docker run -d --name mongodb --rm --network favoties-net mongo 

50ae3f53779fe7faf8385890bb94409a2bdfea87dd0805aad031bfb74bf1e13a
docker: Error response from daemon: network favoties-net not found.

# docker network --help 
Commands:
  connect     Connect a container to a network
  create      Create a network
  disconnect  Disconnect a container from a network
  inspect     Display detailed information on one or more networks
  ls          List networks
  prune       Remove all unused networks
  rm          Remove one or more networks

# docker network create favoties-net
90749e7dde5d70a4f992149b4c007b8c1c443478944cb43478ceb50ace1fb5bb


# docker run -d --name mongodb --rm --network favoties-net mongo 

# docker network ls
NETWORK ID     NAME           DRIVER    SCOPE
2f6f1d305055   bridge         bridge    local
90749e7dde5d   favoties-net   bridge    local
77bb2b63511c   host           host      local
0c073848789e   none           null      local


in app.js 
change 'mongodb://localhost:27017/swfavorites', to  'mongodb://mongodb:27017/swfavorites',
docker resolve the name of container with ip address

# docker build -t favorites-node .


# docker run --name favorites -d --rm -p 3000:3000 --network favoties-net favorites-node

# docker logs favorites


with postman test url http://localhost:3000/favorites 
response 
{
    "favorites": []
}


post request 
http://localhost:3000/favorites 
body Request
  {
      "name":"A New Hope",
      "type":"movie",
      "url":"http://spapi.dev/api/film/1/"
  }

get request 
http://localhost:3000/favorites 