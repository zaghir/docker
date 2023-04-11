FROM node

WORKDIR /app

COPY package.json /app

# RUN   it s used when we build the image no when we run the contai
RUN npm install

#COPY source dest
#COPY . .   ==> . = all host file system   . = Image/container file system
#COPY . .
COPY . /app

# EXPOSE   docker it's isolated  we expose the port how we want to use and listen on this port
EXPOSE 80

# CMD [ "executable" ]
CMD [ "node" , "server.js" ] 
