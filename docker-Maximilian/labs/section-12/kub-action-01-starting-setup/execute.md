
create the image 
`
> docker build -t kub-first-app .
`

check minikube

> minikube status 

minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

create deployment 
> kubectl create deployment first-app --image=kub-first-app 

see how deployment in the cluster 
> kubectl get deployments 


see all pods in the cluster 
> kubectl get pods 

delete deployment
> kubectl delete deployment first-app

we should take image from registry not from local 

> docker tag kub-first-app zaghir/kub-first-app
> docker push zaghir/kub-first-app
> kubectl create deployment first-app --image=zaghir/kub-first-app 

> kubectl get deployments
NAME        READY   UP-TO-DATE   AVAILABLE   AGE
first-app   1/1     1            1           28s


> kubectl get pods
NAME                         READY   STATUS    RESTARTS   AGE
first-app-8489f88fd7-xnz99   1/1     Running   0          65s


get dashbord
> minikube dashboard


create a service 
> kubectl expose deployment first-app --type=LoadBalancer --port=8080
service/first-app exposed

> kubectl get services
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
first-app    LoadBalancer   10.101.193.39   <pending>     8080:31636/TCP   26s
kubernetes   ClusterIP      10.96.0.1       <none>        443/TCP          80m


associat Ip address
> minikube service first-app
 
|-----------|-----------|-------------|---------------------------|
| NAMESPACE |   NAME    | TARGET PORT |            URL            |
|-----------|-----------|-------------|---------------------------|
| default   | first-app |        8080 | http://192.168.49.2:31636 |
|-----------|-----------|-------------|---------------------------|
* Tunnel de démarrage pour le service first-app.
docker@127.0.0.1's password: |-----------|-----------|-------------|------------------------|
| NAMESPACE |   NAME    | TARGET PORT |          URL           |
|-----------|-----------|-------------|------------------------|
| default   | first-app |             | http://127.0.0.1:50086 |
|-----------|-----------|-------------|------------------------|


> minikube dashboard

 call /error   --> application crash   --> then a new pod will be started
> http://192.168.59.100:32484/error

> kubectl get pods
NAME                         READY   STATUS    RESTARTS      AGE
first-app-8489f88fd7-jc4z7   1/1     Running   2 (84s ago)   15m

Replica 
A replica is simply an instance of a pod / Container. 
3 replicas means that the same Pod / Container is running 3 times 

> kubectl scale deployment/first-app --replicas=3
deployment.apps/first-app scaled

> kubectl get pods  
NAME                         READY   STATUS    RESTARTS   AGE
first-app-8489f88fd7-gnhpr   1/1     Running   0          25s
first-app-8489f88fd7-xmfcw   1/1     Running   0          25s
first-app-8489f88fd7-xnz99   1/1     Running   0          158m

> kubectl get services
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
first-app    LoadBalancer   10.101.193.39   <pending>     8080:31636/TCP   115m
kubernetes   ClusterIP      10.96.0.1       <none>        443/TCP          3h15m


> kubectl scale deployment/first-app --replicas=1
deployment.apps/first-app scaled

> kubectl get pods
NAME                         READY   STATUS        RESTARTS   AGE
first-app-8489f88fd7-gnhpr   1/1     Terminating   0          3m31s
first-app-8489f88fd7-xmfcw   1/1     Terminating   0          3m31s
first-app-8489f88fd7-xnz99   1/1     Running       0          162m




make some change  in app.js 
build image 
> docker build -t zaghir/kub-first-app .
> docker push zaghir/kub-first-app

> kubectl get deployments
NAME        READY   UP-TO-DATE   AVAILABLE   AGE
first-app   1/1     1            1           169m

update deployment 
> kubectl set image deployment/first-app kub-first-app=zaghir/kub-first-app

kubernets cant not detecte the change 
with add un tag in docker

> docker tag kub-first-app zaghir/kub-first-app:2
> docker push zaghir/kub-first-app:2

update deployment image 
> kubectl set image deployment/first-app kub-first-app=zaghir/kub-first-app:2

view update deployment
> kubectl rollout status deployment/first-app

Waiting for deployment "first-app" rollout to finish: 1 old replicas are pending termination...
Waiting for deployment "first-app" rollout to finish: 1 old replicas are pending termination...
deployment "first-app" successfully rolled out


> minikube dashboard 

> minikube service first-app

|-----------|-----------|-------------|---------------------------|
| NAMESPACE |   NAME    | TARGET PORT |            URL            |
|-----------|-----------|-------------|---------------------------|
| default   | first-app |        8080 | http://192.168.49.2:31636 |
|-----------|-----------|-------------|---------------------------|
* Tunnel de démarrage pour le service first-app.
docker@127.0.0.1's password: |-----------|-----------|-------------|------------------------|
| NAMESPACE |   NAME    | TARGET PORT |          URL           |
|-----------|-----------|-------------|------------------------|
| default   | first-app |             | http://127.0.0.1:61150 |
|-----------|-----------|-------------|------------------------|

rollback deployment
---------------------
> kubectl rollout undo deployment/first-app

> kubectl get pods
NAME                         READY   STATUS        RESTARTS   AGE
first-app-649fd74b47-bvtbf   1/1     Terminating   0          5m8s
first-app-8489f88fd7-677s2   1/1     Running       0          28s

> kubectl rollout status deployment/first-app
deployment "first-app" successfully rolled out

> kubectl rollout history deployment/first-app
deployment.apps/first-app
REVISION  CHANGE-CAUSE
2         <none>
3         <none>


detail of deployment
> kubectl rollout history deployment/first-app --revision=2

deployment.apps/first-app with revision #2
Pod Template:
  Labels:       app=first-app
        pod-template-hash=649fd74b47
  Containers:
   kub-first-app:
    Image:      zaghir/kub-first-app:2
    Port:       <none>
    Host Port:  <none>
    Environment:        <none>
    Mounts:     <none>
  Volumes:      <none>


back to revision 
> kubectl rollout undo deployment/first-app --to-revision=2


delete service 
> kubectl delete service first-app

delete deployment
> kubectl delete deployment first-app


Using a delarative aproche (1frs = imperative )
-----------------------------
> kubectl get deployments
No resources found in default namespace.
>kubectl get pods
No resources found in default namespace.
>kubectl get services
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   3h3m


