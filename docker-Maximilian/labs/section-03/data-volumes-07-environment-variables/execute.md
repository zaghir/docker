
# docker build -t feedback-node:env .

you should to use de bid mounts only in developement mode 
we add COPY . . in docker file for production 

 # docker run -d --rm --name feedback-app -p 3000:8000 --env-file ./.env -v feedback-files:/app/feedback -v "C:\docker\docker-Maximilian\labs\section-03\data-volumes-07-environment-variables:/app:ro" -v /app/node_modules -v /app/temp feedback-node:env
