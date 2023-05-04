get storage classes 
> kubectl get sc
NAME                 PROVISIONER                RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
standard (default)   k8s.io/minikube-hostpath   Delete          Immediate           false                  25h


> kubectl apply -f=host-pv.yaml
> kubectl apply -f=host-pvc.yaml
> kubectl apply -f=deployment.yaml

> kubectl get pv
NAME      CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM              STORAGECLASS   REASON   AGE
host-pv   1Gi        RWO            Retain           Bound    default/host-pvc   standard                71s

> kubectl get pvc
NAME       STATUS   VOLUME    CAPACITY   ACCESS MODES   STORAGECLASS   AGE
host-pvc   Bound    host-pv   1Gi        RWO            standard       2m42s

> kubectl get deployments
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
story-deployment   2/2     2            2           18h
