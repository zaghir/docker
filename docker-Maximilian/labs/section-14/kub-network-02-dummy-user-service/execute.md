> cd kubernetes
> kubectl apply -f=users-service.yaml
> kubectl apply -f=users-deployment.yaml

for the minikube to get an ip address 
> minikube service users-service

with postman 

curl --location 'http://192.168.59.100:32700/login' \
--header 'Content-Type: application/json' \
--data '{
    "email": "test@gmail.com",
    "password": "test"
}'

curl --location 'http://192.168.59.100:32700/signup' \
--header 'Content-Type: application/json' \
--data '{
    "email": "test@gmail.com",
    "password": "test"
}'