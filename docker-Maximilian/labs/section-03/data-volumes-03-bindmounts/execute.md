
# docker build -t feedback-node:volumes .

we create container with named volume 

 -v feedback:/app/feedback  => named volume
 -v "/c/docker/docker-Maximilian/labs/section-03/data-volumes-04-bindmounts:/app"  =>  bind mounts
 -v /app/node_modules feedback-node:volumes => anonymous

# docker run -d --rm --name feedback-app -p 3000:80 -v feedback:/app/feedback -v "/c/docker/docker-Maximilian/labs/section-03/data-volumes-04-bindmounts:/app" -v /app/node_modules feedback-node:volumes
