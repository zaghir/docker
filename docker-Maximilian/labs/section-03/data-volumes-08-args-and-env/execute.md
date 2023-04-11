
# docker build -t feedback-node:web-app .

# docker build -t feedback-node:dev --build-arg DEFAUTL_PORT=8000 .


you should to use de bid mounts only in developement mode 
we add COPY . . in docker file for production 

 # docker run -d --rm --name feedback-app -p 3000:8000 --env-file ./.env -v feedback:/app/feedback -v "C:\docker\docker-Maximilian\labs\section-03\data-volumes-08-args-and-env:/app" -v /app/node_modules -v /app/temp feedback-node:web-app