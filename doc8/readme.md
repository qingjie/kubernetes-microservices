# New Feature: Vehicle tracking shows the history of each vehicle
# update all images to : release2 tag

```
localhost:doc8 zhao$ kubectl get pvc
NAME        STATUS   VOLUME          CAPACITY   ACCESS MODES   STORAGECLASS     AGE
mongo-pvc   Bound    local-storage   20Gi       RWO            mylocalstorage   6m34s
localhost:doc8 zhao$ kubectl delete pvc mongo-pvc
localhost:doc8 zhao$ kubectl patch pvc mongo-pvc -p '{"metadata":{"finalizers":null}}'
localhost:doc8 zhao$ kubectl get pv
NAME            CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM               STORAGECLASS     REASON   AGE
local-storage   20Gi       RWO            Retain           Bound    default/mongo-pvc   mylocalstorage            6m21s
localhost:doc8 zhao$ kubectl delete pv local-storage --grace-period=0 --force

localhost:doc8 zhao$ localhost:doc8 zhao$ kubectl get pvcdelete pvc mongo-pvc
-bash: localhost:doc8: command not found
localhost:doc8 zhao$ delete pvc mongo-pvc
-bash: delete: command not found
localhost:doc8 zhao$ kubectl delete pvc mongo-pvc
persistentvolumeclaim "mongo-pvc" deleted
^C
localhost:doc8 zhao$ kubectl delete pvc mongo-pvc
persistentvolumeclaim "mongo-pvc" deleted
^C
localhost:doc8 zhao$ kubectl patch pvc mongo-pvc -p '{"metadata":{"finalizers":null}}'
persistentvolumeclaim/mongo-pvc patched
localhost:doc8 zhao$ kubectl get pvc
No resources found.
localhost:doc8 zhao$ kubectl get pv
No resources found.
localhost:doc8 zhao$ clear
localhost:doc8 zhao$ pwd
/Users/zhao/dev/doc8
localhost:doc8 zhao$ ls
img			operr-v3-base		services.yaml		workloads.yaml
mongo-stack.yaml	readme.md		storage.yaml
localhost:doc8 zhao$ pwd
/Users/zhao/dev/doc8
localhost:doc8 zhao$ kubectl get all
NAME                                     READY   STATUS    RESTARTS   AGE
pod/api-gateway-77dff9778b-hg98z         1/1     Running   2          2d4h
pod/mongodb-5dc79669d-rhmf6              1/1     Running   0          8m30s
pod/position-simulator-96f46d659-l6n27   1/1     Running   0          82m
pod/position-tracker-f6f5dd79d-c7vh4     1/1     Running   2          2d3h
pod/queue-8b577ccc6-xllpn                1/1     Running   2          2d4h
pod/webapp-7bf85bf85f-n9nr4              1/1     Running   4          2d4h


NAME                                TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                          AGE
service/fleetman-api-gateway        NodePort    10.98.203.46     <none>        8080:30020/TCP                   2d4h
service/fleetman-mongodb            ClusterIP   10.111.156.9     <none>        27017/TCP                        46h
service/fleetman-position-tracker   ClusterIP   10.99.19.185     <none>        8080/TCP                         2d4h
service/fleetman-queue              NodePort    10.106.133.70    <none>        8161:30010/TCP,61616:31227/TCP   2d4h
service/fleetman-webapp             NodePort    10.110.214.192   <none>        80:30080/TCP                     2d4h
service/kubernetes                  ClusterIP   10.96.0.1        <none>        443/TCP                          2d4h


NAME                                 READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/api-gateway          1/1     1            1           2d4h
deployment.apps/mongodb              1/1     1            1           2d3h
deployment.apps/position-simulator   1/1     1            1           2d4h
deployment.apps/position-tracker     1/1     1            1           2d4h
deployment.apps/queue                1/1     1            1           2d4h
deployment.apps/webapp               1/1     1            1           2d4h

NAME                                           DESIRED   CURRENT   READY   AGE
replicaset.apps/api-gateway-6b94f4bcf5         0         0         0       2d4h
replicaset.apps/api-gateway-77dff9778b         1         1         1       2d4h
replicaset.apps/mongodb-59458887cf             0         0         0       46h
replicaset.apps/mongodb-5dbdc5d5b9             0         0         0       2d3h
replicaset.apps/mongodb-5dc79669d              1         1         1       40m
replicaset.apps/mongodb-6dd67d6d46             0         0         0       46h
replicaset.apps/position-simulator-96f46d659   1         1         1       2d4h
replicaset.apps/position-simulator-d5fdcbc98   0         0         0       2d4h
replicaset.apps/position-tracker-795b4ffb77    0         0         0       2d4h
replicaset.apps/position-tracker-cd786fdfb     0         0         0       2d4h
replicaset.apps/position-tracker-f6f5dd79d     1         1         1       2d3h
replicaset.apps/queue-7d94749657               0         0         0       2d4h
replicaset.apps/queue-8b577ccc6                1         1         1       2d4h
replicaset.apps/webapp-5c5dcc8d66              0         0         0       2d4h
replicaset.apps/webapp-7bf85bf85f              1         1         1       2d4h




localhost:doc8 zhao$ kubectl delete pod/mongodb-5dc79669d-rhmf6
pod "mongodb-5dc79669d-rhmf6" deleted
localhost:doc8 zhao$ kubectl get all
NAME                                     READY   STATUS    RESTARTS   AGE
pod/api-gateway-77dff9778b-hg98z         1/1     Running   2          2d4h
pod/mongodb-5dc79669d-lmbnq              0/1     Pending   0          8s
pod/position-simulator-96f46d659-l6n27   1/1     Running   0          82m
pod/position-tracker-f6f5dd79d-c7vh4     1/1     Running   2          2d3h
pod/queue-8b577ccc6-xllpn                1/1     Running   2          2d4h
pod/webapp-7bf85bf85f-n9nr4              1/1     Running   4          2d4h


NAME                                TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                          AGE
service/fleetman-api-gateway        NodePort    10.98.203.46     <none>        8080:30020/TCP                   2d4h
service/fleetman-mongodb            ClusterIP   10.111.156.9     <none>        27017/TCP                        46h
service/fleetman-position-tracker   ClusterIP   10.99.19.185     <none>        8080/TCP                         2d4h
service/fleetman-queue              NodePort    10.106.133.70    <none>        8161:30010/TCP,61616:31227/TCP   2d4h
service/fleetman-webapp             NodePort    10.110.214.192   <none>        80:30080/TCP                     2d4h
service/kubernetes                  ClusterIP   10.96.0.1        <none>        443/TCP                          2d4h


NAME                                 READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/api-gateway          1/1     1            1           2d4h
deployment.apps/mongodb              0/1     1            0           2d3h
deployment.apps/position-simulator   1/1     1            1           2d4h
deployment.apps/position-tracker     1/1     1            1           2d4h
deployment.apps/queue                1/1     1            1           2d4h
deployment.apps/webapp               1/1     1            1           2d4h

NAME                                           DESIRED   CURRENT   READY   AGE
replicaset.apps/api-gateway-6b94f4bcf5         0         0         0       2d4h
replicaset.apps/api-gateway-77dff9778b         1         1         1       2d4h
replicaset.apps/mongodb-59458887cf             0         0         0       46h
replicaset.apps/mongodb-5dbdc5d5b9             0         0         0       2d3h
replicaset.apps/mongodb-5dc79669d              1         1         0       40m
replicaset.apps/mongodb-6dd67d6d46             0         0         0       46h
replicaset.apps/position-simulator-96f46d659   1         1         1       2d4h
replicaset.apps/position-simulator-d5fdcbc98   0         0         0       2d4h
replicaset.apps/position-tracker-795b4ffb77    0         0         0       2d4h
replicaset.apps/position-tracker-cd786fdfb     0         0         0       2d4h
replicaset.apps/position-tracker-f6f5dd79d     1         1         1       2d3h
replicaset.apps/queue-7d94749657               0         0         0       2d4h
replicaset.apps/queue-8b577ccc6                1         1         1       2d4h
replicaset.apps/webapp-5c5dcc8d66              0         0         0       2d4h
replicaset.apps/webapp-7bf85bf85f              1         1         1       2d4h




localhost:doc8 zhao$ kubectl describe pod/mongodb-5dc79669d-lmbnq
Name:           mongodb-5dc79669d-lmbnq
Namespace:      default
Priority:       0
Node:           <none>
Labels:         app=mongodb
                pod-template-hash=5dc79669d
Annotations:    <none>
Status:         Pending
IP:
Controlled By:  ReplicaSet/mongodb-5dc79669d
Containers:
  mongodb:
    Image:        mongo:3.6.5-jessie
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:
      /data/db from mongo-persistent-storage (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-n9pk7 (ro)
Conditions:
  Type           Status
  PodScheduled   False
Volumes:
  mongo-persistent-storage:
    Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
    ClaimName:  mongo-pvc
    ReadOnly:   false
  default-token-n9pk7:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-n9pk7
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason            Age                From               Message
  ----     ------            ----               ----               -------
  Warning  FailedScheduling  14s (x3 over 16s)  default-scheduler  persistentvolumeclaim "mongo-pvc" not found
localhost:doc8 zhao$ kubectl apply -f storage.yaml
persistentvolumeclaim/mongo-pvc created
persistentvolume/local-storage created
localhost:doc8 zhao$ kubectl get pvc
NAME        STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS     AGE
mongo-pvc   Pending                                      mylocalstorage   6s
localhost:doc8 zhao$ kubectl get pv
NAME            CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS     REASON   AGE
local-storage   20Gi       RWO            Retain           Available           mylocalstorage            7s
localhost:doc8 zhao$ kubectl get pvc
NAME        STATUS   VOLUME          CAPACITY   ACCESS MODES   STORAGECLASS     AGE
mongo-pvc   Bound    local-storage   20Gi       RWO            mylocalstorage   9s
localhost:doc8 zhao$ kubectl apply -f mongo-stack.yaml
deployment.apps/mongodb unchanged
service/fleetman-mongodb unchanged
localhost:doc8 zhao$ kubectl get all
NAME                                     READY   STATUS    RESTARTS   AGE
pod/api-gateway-77dff9778b-hg98z         1/1     Running   2          2d4h
pod/mongodb-5dc79669d-lmbnq              1/1     Running   0          68s
pod/position-simulator-96f46d659-l6n27   1/1     Running   0          83m
pod/position-tracker-f6f5dd79d-c7vh4     1/1     Running   2          2d3h
pod/queue-8b577ccc6-xllpn                1/1     Running   2          2d4h
pod/webapp-7bf85bf85f-n9nr4              1/1     Running   4          2d4h


NAME                                TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                          AGE
service/fleetman-api-gateway        NodePort    10.98.203.46     <none>        8080:30020/TCP                   2d4h
service/fleetman-mongodb            ClusterIP   10.111.156.9     <none>        27017/TCP                        46h
service/fleetman-position-tracker   ClusterIP   10.99.19.185     <none>        8080/TCP                         2d4h
service/fleetman-queue              NodePort    10.106.133.70    <none>        8161:30010/TCP,61616:31227/TCP   2d4h
service/fleetman-webapp             NodePort    10.110.214.192   <none>        80:30080/TCP                     2d4h
service/kubernetes                  ClusterIP   10.96.0.1        <none>        443/TCP                          2d4h


NAME                                 READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/api-gateway          1/1     1            1           2d4h
deployment.apps/mongodb              1/1     1            1           2d3h
deployment.apps/position-simulator   1/1     1            1           2d4h
deployment.apps/position-tracker     1/1     1            1           2d4h
deployment.apps/queue                1/1     1            1           2d4h
deployment.apps/webapp               1/1     1            1           2d4h

NAME                                           DESIRED   CURRENT   READY   AGE
replicaset.apps/api-gateway-6b94f4bcf5         0         0         0       2d4h
replicaset.apps/api-gateway-77dff9778b         1         1         1       2d4h
replicaset.apps/mongodb-59458887cf             0         0         0       46h
replicaset.apps/mongodb-5dbdc5d5b9             0         0         0       2d3h
replicaset.apps/mongodb-5dc79669d              1         1         1       41m
replicaset.apps/mongodb-6dd67d6d46             0         0         0       46h
replicaset.apps/position-simulator-96f46d659   1         1         1       2d4h
replicaset.apps/position-simulator-d5fdcbc98   0         0         0       2d4h
replicaset.apps/position-tracker-795b4ffb77    0         0         0       2d4h
replicaset.apps/position-tracker-cd786fdfb     0         0         0       2d4h
replicaset.apps/position-tracker-f6f5dd79d     1         1         1       2d3h
replicaset.apps/queue-7d94749657               0         0         0       2d4h
replicaset.apps/queue-8b577ccc6                1         1         1       2d4h
replicaset.apps/webapp-5c5dcc8d66              0         0         0       2d4h
replicaset.apps/webapp-7bf85bf85f              1         1         1       2d4h




localhost:doc8 zhao$ kubectl delete pod/mongodb-5dc79669d-lmbnq
pod "mongodb-5dc79669d-lmbnq" deleted
localhost:doc8 zhao$ kubectl get all
NAME                                     READY   STATUS    RESTARTS   AGE
pod/api-gateway-77dff9778b-hg98z         1/1     Running   2          2d4h
pod/mongodb-5dc79669d-db65z              1/1     Running   0          11s
pod/position-simulator-96f46d659-l6n27   1/1     Running   0          83m
pod/position-tracker-f6f5dd79d-c7vh4     1/1     Running   2          2d3h
pod/queue-8b577ccc6-xllpn                1/1     Running   2          2d4h
pod/webapp-7bf85bf85f-n9nr4              1/1     Running   4          2d4h


NAME                                TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                          AGE
service/fleetman-api-gateway        NodePort    10.98.203.46     <none>        8080:30020/TCP                   2d4h
service/fleetman-mongodb            ClusterIP   10.111.156.9     <none>        27017/TCP                        46h
service/fleetman-position-tracker   ClusterIP   10.99.19.185     <none>        8080/TCP                         2d4h
service/fleetman-queue              NodePort    10.106.133.70    <none>        8161:30010/TCP,61616:31227/TCP   2d4h
service/fleetman-webapp             NodePort    10.110.214.192   <none>        80:30080/TCP                     2d4h
service/kubernetes                  ClusterIP   10.96.0.1        <none>        443/TCP                          2d4h


NAME                                 READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/api-gateway          1/1     1            1           2d4h
deployment.apps/mongodb              1/1     1            1           2d3h
deployment.apps/position-simulator   1/1     1            1           2d4h
deployment.apps/position-tracker     1/1     1            1           2d4h
deployment.apps/queue                1/1     1            1           2d4h
deployment.apps/webapp               1/1     1            1           2d4h

NAME                                           DESIRED   CURRENT   READY   AGE
replicaset.apps/api-gateway-6b94f4bcf5         0         0         0       2d4h
replicaset.apps/api-gateway-77dff9778b         1         1         1       2d4h
replicaset.apps/mongodb-59458887cf             0         0         0       46h
replicaset.apps/mongodb-5dbdc5d5b9             0         0         0       2d3h
replicaset.apps/mongodb-5dc79669d              1         1         1       41m
replicaset.apps/mongodb-6dd67d6d46             0         0         0       46h
replicaset.apps/position-simulator-96f46d659   1         1         1       2d4h
replicaset.apps/position-simulator-d5fdcbc98   0         0         0       2d4h
replicaset.apps/position-tracker-795b4ffb77    0         0         0       2d4h
replicaset.apps/position-tracker-cd786fdfb     0         0         0       2d4h
replicaset.apps/position-tracker-f6f5dd79d     1         1         1       2d3h
replicaset.apps/queue-7d94749657               0         0         0       2d4h
replicaset.apps/queue-8b577ccc6                1         1         1       2d4h
replicaset.apps/webapp-5c5dcc8d66              0         0         0       2d4h
replicaset.apps/webapp-7bf85bf85f              1         1         1       2d4h




localhost:doc8 zhao$ kubectl describe pod/mongodb-5dc79669d-db65z
Name:           mongodb-5dc79669d-db65z
Namespace:      default
Priority:       0
Node:           minikube/10.0.2.15
Start Time:     Thu, 11 Jul 2019 16:05:04 -0400
Labels:         app=mongodb
                pod-template-hash=5dc79669d
Annotations:    <none>
Status:         Running
IP:             172.17.0.7
Controlled By:  ReplicaSet/mongodb-5dc79669d
Containers:
  mongodb:
    Container ID:   docker://b517ec555596084244df9e8b7d767085b66364a118fbd67d865ea5e3b2c0ce58
    Image:          mongo:3.6.5-jessie
    Image ID:       docker-pullable://mongo@sha256:3e00936a4fbd17003cfd33ca808f03ada736134774bfbc3069d3757905a4a326
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Thu, 11 Jul 2019 16:05:05 -0400
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /data/db from mongo-persistent-storage (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-n9pk7 (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  mongo-persistent-storage:
    Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
    ClaimName:  mongo-pvc
    ReadOnly:   false
  default-token-n9pk7:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-n9pk7
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  19s   default-scheduler  Successfully assigned default/mongodb-5dc79669d-db65z to minikube
  Normal  Pulled     18s   kubelet, minikube  Container image "mongo:3.6.5-jessie" already present on machine
  Normal  Created    18s   kubelet, minikube  Created container mongodb
  Normal  Started    18s   kubelet, minikube  Started container mongodb

```
