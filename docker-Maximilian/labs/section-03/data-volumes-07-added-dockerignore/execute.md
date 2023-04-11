
# docker build -t feedback-node:volumes .

you should to use de bid mounts only in developement mode 
we add COPY . . in docker file for production 

 # docker run -d --rm --name feedback-app -p 3000:80 -v feedback-files:/app/feedback -v "C:\docker\docker-Maximilian\labs\section-03\data-volumes-07-added-dockerignore:/app:ro" -v /app/node_modules -v /app/temp feedback-node:volumes


