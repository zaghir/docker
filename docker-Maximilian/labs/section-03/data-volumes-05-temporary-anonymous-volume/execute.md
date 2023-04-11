
# docker build -t feedback-node:volumes .

we create container with named volume 

 -v feedback:/app/feedback  => named volume
 -v "/c/docker/docker-Maximilian/labs/section-03/data-volumes-04-bindmounts:/app:ro"  =>  bind mounts  and read only
 -v /app/node_modules feedback-node:volumes => anonymous

# docker run -d --rm --name feedback-app -p 3000:80 -v feedback:/app/feedback -v "C:\docker\docker-Maximilian\labs\section-03\data-volumes-05-temporary-anonymous-volume:/app" -v /app/node_modules -v /app/temp feedback-node:volumes
