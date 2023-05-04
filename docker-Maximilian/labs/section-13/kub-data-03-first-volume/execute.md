> docker build -t zaghir/kub-data-demo:1 .
> docker image push zaghir/kub-data-demo:1

> kubectl apply -f=service.yaml -f=deployment.yaml 
> minikube service story-service

Post Request
> curl --location 'http://192.168.59.100:30201/story' \
--header 'Content-Type: application/json' \
--data '{
    "text": "my story"
}'

Get Request
curl --location --request GET 'http://192.168.59.100:30201/story' \
--header 'Content-Type: application/json' \
--data '{
    "text": "my story"
}'


Error Request 
curl --location --request GET 'http://192.168.59.100:30201/error' \
--header 'Content-Type: application/json' \
--data '{
    "text": "my story"
}'

Get Request
curl --location --request GET 'http://192.168.59.100:30201/story' \
--header 'Content-Type: application/json' \
--data '{
    "text": "my story"
}'

> kubectl get deployments
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
story-deployment   1/1     1            1           15m
