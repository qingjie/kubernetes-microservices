```

localhost:doc4 zhao$ kubectl get all
NAME                     READY   STATUS    RESTARTS   AGE
pod/queue                1/1     Running   0          15m
pod/webapp               1/1     Running   3          6d
pod/webapp-release-0-5   1/1     Running   1          4d


NAME                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/fleetman-queue    NodePort    10.101.245.41   <none>        8161:30010/TCP   15m
service/fleetman-webapp   NodePort    10.104.2.249    <none>        80:30080/TCP     5d
service/kubernetes        ClusterIP   10.96.0.1       <none>        443/TCP          9d







localhost:doc4 zhao$ kubectl describe svc fleetman-webapp
Name:                     fleetman-webapp
Namespace:                default
Labels:                   <none>
Annotations:              kubectl.kubernetes.io/last-applied-configuration:
                            {"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"name":"fleetman-webapp","namespace":"default"},"spec":{"ports":[{"name":...
Selector:                 app=webapp,release=0-5
Type:                     NodePort
IP:                       10.104.2.249
Port:                     http  80/TCP
TargetPort:               80/TCP
NodePort:                 http  30080/TCP
Endpoints:                172.17.0.5:80
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
localhost:doc4 zhao$ kubectl delete po webapp-release-0-5
pod "webapp-release-0-5" deleted
localhost:doc4 zhao$ kubectl get all
NAME         READY   STATUS    RESTARTS   AGE
pod/queue    1/1     Running   0          20m
pod/webapp   1/1     Running   3          6d


NAME                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/fleetman-queue    NodePort    10.101.245.41   <none>        8161:30010/TCP   20m
service/fleetman-webapp   NodePort    10.104.2.249    <none>        80:30080/TCP     5d
service/kubernetes        ClusterIP   10.96.0.1       <none>        443/TCP          9d







localhost:doc4 zhao$ tree
.
├── img
│   └── active-queue.png
├── pods.yaml
├── readme.md
└── services.yaml

1 directory, 4 files

localhost:doc4 zhao$ kubectl delete pod --all
pod "queue" deleted
pod "webapp" deleted
localhost:doc4 zhao$ kubectl get all


NAME                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/fleetman-queue    NodePort    10.101.245.41   <none>        8161:30010/TCP   46m
service/fleetman-webapp   NodePort    10.104.2.249    <none>        80:30080/TCP     5d
service/kubernetes        ClusterIP   10.96.0.1       <none>        443/TCP          9d







localhost:doc4 zhao$ kubectl apply -f pods.yaml
replicaset.apps/webapp created
pod/queue created
localhost:doc4 zhao$ kubectl get all
NAME               READY   STATUS    RESTARTS   AGE
pod/queue          1/1     Running   0          33s
pod/webapp-n8xlm   1/1     Running   0          33s


NAME                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/fleetman-queue    NodePort    10.101.245.41   <none>        8161:30010/TCP   47m
service/fleetman-webapp   NodePort    10.104.2.249    <none>        80:30080/TCP     5d
service/kubernetes        ClusterIP   10.96.0.1       <none>        443/TCP          9d



NAME                     DESIRED   CURRENT   READY   AGE
replicaset.apps/webapp   1         1         1       33s




localhost:doc4 zhao$ kubectl describe replicaset webapp
Name:         webapp
Namespace:    default
Selector:     app=webapp
Labels:       app=webapp
Annotations:  kubectl.kubernetes.io/last-applied-configuration:
                {"apiVersion":"apps/v1","kind":"ReplicaSet","metadata":{"annotations":{},"name":"webapp","namespace":"default"},"spec":{"replicas":1,"sele...
Replicas:     1 current / 1 desired
Pods Status:  1 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  app=webapp
  Containers:
   webapp:
    Image:        richardchesterwood/k8s-fleetman-webapp-angular:release0-5
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:
  Type    Reason            Age   From                   Message
  ----    ------            ----  ----                   -------
  Normal  SuccessfulCreate  3m1s  replicaset-controller  Created pod: webapp-n8xlm
localhost:doc4 zhao$ kubectl describe rs webapp
Name:         webapp
Namespace:    default
Selector:     app=webapp
Labels:       app=webapp
Annotations:  kubectl.kubernetes.io/last-applied-configuration:
                {"apiVersion":"apps/v1","kind":"ReplicaSet","metadata":{"annotations":{},"name":"webapp","namespace":"default"},"spec":{"replicas":1,"sele...
Replicas:     1 current / 1 desired
Pods Status:  1 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  app=webapp
  Containers:
   webapp:
    Image:        richardchesterwood/k8s-fleetman-webapp-angular:release0-5
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:
  Type    Reason            Age    From                   Message
  ----    ------            ----   ----                   -------
  Normal  SuccessfulCreate  3m15s  replicaset-controller  Created pod: webapp-n8xlm
localhost:doc4 zhao$ kubectl describe webapp
error: the server doesn't have a resource type "webapp"
localhost:doc4 zhao$ kubectl describe rs webapp
Name:         webapp
Namespace:    default
Selector:     app=webapp
Labels:       app=webapp
Annotations:  kubectl.kubernetes.io/last-applied-configuration:
                {"apiVersion":"apps/v1","kind":"ReplicaSet","metadata":{"annotations":{},"name":"webapp","namespace":"default"},"spec":{"replicas":1,"sele...
Replicas:     1 current / 1 desired
Pods Status:  1 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  app=webapp
  Containers:
   webapp:
    Image:        richardchesterwood/k8s-fleetman-webapp-angular:release0-5
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:
  Type    Reason            Age    From                   Message
  ----    ------            ----   ----                   -------
  Normal  SuccessfulCreate  4m11s  replicaset-controller  Created pod: webapp-n8xlm
localhost:doc4 zhao$ kubectl apply -f services.yaml
service/fleetman-webapp configured
service/fleetman-queue unchanged
localhost:doc4 zhao$ kubectl get all
NAME               READY   STATUS    RESTARTS   AGE
pod/queue          1/1     Running   0          6m
pod/webapp-n8xlm   1/1     Running   0          6m


NAME                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/fleetman-queue    NodePort    10.101.245.41   <none>        8161:30010/TCP   54m
service/fleetman-webapp   NodePort    10.104.2.249    <none>        80:30080/TCP     5d
service/kubernetes        ClusterIP   10.96.0.1       <none>        443/TCP          9d



NAME                     DESIRED   CURRENT   READY   AGE
replicaset.apps/webapp   1         1         1       6m




localhost:doc4 zhao$ kubectl delete pod webapp-n8xlm
pod "webapp-n8xlm" deleted
localhost:doc4 zhao$ kubectl get all
NAME               READY   STATUS    RESTARTS   AGE
pod/queue          1/1     Running   0          8m
pod/webapp-2ftzs   1/1     Running   0          18s


NAME                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/fleetman-queue    NodePort    10.101.245.41   <none>        8161:30010/TCP   55m
service/fleetman-webapp   NodePort    10.104.2.249    <none>        80:30080/TCP     5d
service/kubernetes        ClusterIP   10.96.0.1       <none>        443/TCP          9d



NAME                     DESIRED   CURRENT   READY   AGE
replicaset.apps/webapp   1         1         1       8m




localhost:doc4 zhao$ kubectl describe rs webapp
Name:         webapp
Namespace:    default
Selector:     app=webapp
Labels:       app=webapp
Annotations:  kubectl.kubernetes.io/last-applied-configuration:
                {"apiVersion":"apps/v1","kind":"ReplicaSet","metadata":{"annotations":{},"name":"webapp","namespace":"default"},"spec":{"replicas":1,"sele...
Replicas:     1 current / 1 desired
Pods Status:  1 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  app=webapp
  Containers:
   webapp:
    Image:        richardchesterwood/k8s-fleetman-webapp-angular:release0-5
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:
  Type    Reason            Age    From                   Message
  ----    ------            ----   ----                   -------
  Normal  SuccessfulCreate  8m34s  replicaset-controller  Created pod: webapp-n8xlm
  Normal  SuccessfulCreate  46s    replicaset-controller  Created pod: webapp-2ftzs
localhost:doc4 zhao$ kubectl apply -f pods.yaml
replicaset.apps/webapp unchanged
pod/queue unchanged
localhost:doc4 zhao$ kubectl apply -f pods.yaml
replicaset.apps/webapp configured
pod/queue unchanged
localhost:doc4 zhao$ kubectl describe rs webapp
Name:         webapp
Namespace:    default
Selector:     app=webapp
Labels:       app=webapp
Annotations:  kubectl.kubernetes.io/last-applied-configuration:
                {"apiVersion":"apps/v1","kind":"ReplicaSet","metadata":{"annotations":{},"name":"webapp","namespace":"default"},"spec":{"replicas":2,"sele...
Replicas:     2 current / 2 desired
Pods Status:  2 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  app=webapp
  Containers:
   webapp:
    Image:        richardchesterwood/k8s-fleetman-webapp-angular:release0-5
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:
  Type    Reason            Age    From                   Message
  ----    ------            ----   ----                   -------
  Normal  SuccessfulCreate  13m    replicaset-controller  Created pod: webapp-n8xlm
  Normal  SuccessfulCreate  5m42s  replicaset-controller  Created pod: webapp-2ftzs
  Normal  SuccessfulCreate  15s    replicaset-controller  Created pod: webapp-lv9m4
localhost:doc4 zhao$ kubectl get all
NAME               READY   STATUS    RESTARTS   AGE
pod/queue          1/1     Running   0          13m
pod/webapp-2ftzs   1/1     Running   0          6m
pod/webapp-lv9m4   1/1     Running   0          43s


NAME                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/fleetman-queue    NodePort    10.101.245.41   <none>        8161:30010/TCP   1h
service/fleetman-webapp   NodePort    10.104.2.249    <none>        80:30080/TCP     5d
service/kubernetes        ClusterIP   10.96.0.1       <none>        443/TCP          9d



NAME                     DESIRED   CURRENT   READY   AGE
replicaset.apps/webapp   2         2         2       13m




localhost:doc4 zhao$ kubectl delete webapp-2ftzs
error: resource(s) were provided, but no name, label selector, or --all flag specified
localhost:doc4 zhao$ kubectl delete po webapp-2ftzs
pod "webapp-2ftzs" deleted
localhost:doc4 zhao$ kubectl get all
NAME               READY   STATUS    RESTARTS   AGE
pod/queue          1/1     Running   0          15m
pod/webapp-lv9m4   1/1     Running   0          1m
pod/webapp-nnvld   1/1     Running   0          35s


NAME                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/fleetman-queue    NodePort    10.101.245.41   <none>        8161:30010/TCP   1h
service/fleetman-webapp   NodePort    10.104.2.249    <none>        80:30080/TCP     5d
service/kubernetes        ClusterIP   10.96.0.1       <none>        443/TCP          9d



NAME                     DESIRED   CURRENT   READY   AGE
replicaset.apps/webapp   2         2         2       15m
```
