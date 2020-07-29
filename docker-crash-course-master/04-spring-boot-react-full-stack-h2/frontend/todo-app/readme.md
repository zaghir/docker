in 04-spring-boot-react-full-stack-h2\frontend\todo-app  
run this command to install dependences for front module 
npm install 
npm start 
npm run build        create a package 

     74.55 KB      build\static\js\2.3f64e426.chunk.js
     3.26 KB       build\static\js\main.b5be4fdf.chunk.js
     764 B         build\static\js\runtime~main.c5541365.js
     624 B (-1 B)  build\static\css\main.fdab1a07.chunk.css

in 04-spring-boot-react-full-stack-h2\restful-web-services
--> create an image with Dockerfile , spotify , pring-boot-maven-plugin(create leayers)
mvn clean package 

--> create a container 
docker container run -p 8080:8080 in28min/rest-api-full-stack:0.0.1-SNAPSHOT



to run this fontend application we need 
   ## nodeJS
   npm install 
   npm run build 

   ## nginx
   To run the pakage 

    ## goll 
    keep the docker image as small as possible!



--> create an image for frontend
docker build . -t
--> create an image for frontend  with the tag
docker build . -t in28min/todo-front-end:0.0.1-SNAPSHOT

--> create a container from front-end image 
docker run  -p 4200:80 in28min/todo-front-end:0.0.1-SNAPSHOT 

