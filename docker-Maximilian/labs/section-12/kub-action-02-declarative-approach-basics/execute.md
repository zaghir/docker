run deployment 
> kubectl apply -f=deployment.yaml

> kubectl apply -f=deployment.yaml -f=d1.yaml -f=d2.yaml

> kubectl get deployments
NAME                    READY   UP-TO-DATE   AVAILABLE   AGE
second-app-deployment   1/1     1            0           18s

> kubectl get pods
NAME                                     READY   STATUS             RESTARTS   AGE
second-app-deployment-5ff689f666-k8f25   0/1     ImagePullBackOff   0          26s


run service
> kubectl apply -f service.yaml

expose service 
> minikube service backend 


update 
you can change number of replica in deployment.yaml and execute kubectl apply -f=deployment.yaml again

delete 
> kubectl delete -f=deployment.yaml,service.yaml
> kubectl delete -f=deployment.yaml -f=service.yaml
