create image docker and push to repository

> docker-compose up -d --build
> docker image tag kub-data-02-deployment-and-service-stories zaghir/kub-data-demo
> docker image push zaghir/kub-data-demo

or

> cd kub-data-02-deployment-and-service
> docker build -t zaghir/kub-data-demo .
> docker image push zaghir/kub-data-demo

test container with postman 
> docker container run -d -p 80:3000 --rm zaghir/kub-data-demo  

> delete 
> kubectl delete -f=deployment.yaml,service.yaml

> kubectl apply -f=service.yaml -f=deployment.yaml 
deployment.apps/story-deployment created
service/story-service created

> kubectl get deployments
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
story-deployment   1/1     1            1           20s

expose service 
> minikube service story-service

|-----------|---------------|-------------|-----------------------------|
| NAMESPACE |     NAME      | TARGET PORT |             URL             |
|-----------|---------------|-------------|-----------------------------|
| default   | story-service |          80 | http://192.168.59.100:32700 |
|-----------|---------------|-------------|-----------------------------|
* Ouverture du service default/story-service dans le navigateur par défaut...

send post request to  http://192.168.59.100:32700

curl --location 'http://192.168.59.100:32700/story' \
--header 'Content-Type: application/json' \
--data '{
    "text": "my story"
}'


