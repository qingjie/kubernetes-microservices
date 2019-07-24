```
localhost:doc16 zhao$ kubectl get pod
NAME                                 READY   STATUS    RESTARTS   AGE
api-gateway-57579fc57b-52vn8         1/1     Running   1          45h
mongodb-5dc79669d-r5g2c              1/1     Running   2          8d
position-simulator-96f46d659-dxzzp   1/1     Running   2          8d
position-tracker-f6f5dd79d-b8q77     1/1     Running   2          8d
queue-5798db7fdb-b89tc               1/1     Running   2          8d
webapp-7bf85bf85f-lf8x8              1/1     Running   7          8d
localhost:doc16 zhao$ kubectl top pod
NAME                                 CPU(cores)   MEMORY(bytes)
api-gateway-57579fc57b-52vn8         2m           171Mi
mongodb-5dc79669d-r5g2c              3m           45Mi
position-simulator-96f46d659-dxzzp   11m          421Mi
position-tracker-f6f5dd79d-b8q77     7m           336Mi
queue-5798db7fdb-b89tc               18m          412Mi
webapp-7bf85bf85f-lf8x8              0m           4Mi
localhost:doc16 zhao$ kubectl get hpa
NAME          REFERENCE                TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
api-gateway   Deployment/api-gateway   4%/400%   1         4         1          45h
```

http://192.168.99.106:30080/api
or
curl 192.168.99.106:30080/api

localhost:doc16 zhao$ while true; do curl 192.168.99.106:30080/api; done

in a new window: do the following:
```
localhost:doc16 zhao$ while true; do curl 192.168.99.106:30080/api; echo; done
```
```
localhost:doc16 zhao$ kubectl delete -f autoscale-rules.yaml
horizontalpodautoscaler.autoscaling "api-gateway" deleted
localhost:doc16 zhao$ kubectl get hpa
No resources found.
```
```
localhost:doc16 zhao$ kubectl get pod
NAME                                 READY   STATUS    RESTARTS   AGE
api-gateway-d548b9fb4-qsx84          0/1     Running   0          15s
api-gateway-d548b9fb4-rzvb7          1/1     Running   0          67s
api-gateway-d548b9fb4-wcr87          0/1     Running   0          15s
mongodb-5dc79669d-r5g2c              1/1     Running   2          8d
position-simulator-96f46d659-dxzzp   1/1     Running   2          8d
position-tracker-f6f5dd79d-b8q77     1/1     Running   2          8d
queue-5798db7fdb-b89tc               1/1     Running   2          8d
webapp-7bf85bf85f-lf8x8              1/1     Running   7          8d
localhost:doc16 zhao$ kubectl get pod
NAME                                 READY   STATUS    RESTARTS   AGE
api-gateway-d548b9fb4-qsx84          1/1     Running   0          34s
api-gateway-d548b9fb4-rzvb7          1/1     Running   0          86s
api-gateway-d548b9fb4-wcr87          1/1     Running   0          34s
mongodb-5dc79669d-r5g2c              1/1     Running   2          8d
position-simulator-96f46d659-dxzzp   1/1     Running   2          8d
position-tracker-f6f5dd79d-b8q77     1/1     Running   2          8d
queue-5798db7fdb-b89tc               1/1     Running   2          8d
webapp-7bf85bf85f-lf8x8              1/1     Running   7          8d
localhost:doc16 zhao$ kubectl describe api-gateway-d548b9fb4-rzvb7
error: the server doesn't have a resource type "api-gateway-d548b9fb4-rzvb7"
localhost:doc16 zhao$ kubectl describe pod api-gateway-d548b9fb4-rzvb7
Name:           api-gateway-d548b9fb4-rzvb7
Namespace:      default
Priority:       0
Node:           minikube/10.0.2.15
Start Time:     Wed, 24 Jul 2019 15:30:45 -0400
Labels:         app=api-gateway
                pod-template-hash=d548b9fb4
Annotations:    <none>
Status:         Running
IP:             172.17.0.14
Controlled By:  ReplicaSet/api-gateway-d548b9fb4
Containers:
  api-gateway:
    Container ID:   docker://d0d3e47f422956726be9f61ce4bc3447a60d299d7ef4a90ad95b6bb7b31cbb23
    Image:          richardchesterwood/k8s-fleetman-api-gateway:performance
    Image ID:       docker-pullable://richardchesterwood/k8s-fleetman-api-gateway@sha256:19ea0588b3127f45420120de171da151bca5efacebcbc963fcb05419c12cdbe0
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Wed, 24 Jul 2019 15:30:46 -0400
    Ready:          True
    Restart Count:  0
    Requests:
      cpu:      50m
      memory:   200Mi
    Readiness:  http-get http://:8080/ delay=0s timeout=1s period=10s #success=1 #failure=3
    Environment:
      SPRING_PROFILES_ACTIVE:  production-microservice
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-n9pk7 (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  default-token-n9pk7:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-n9pk7
    Optional:    false
QoS Class:       Burstable
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  2m33s  default-scheduler  Successfully assigned default/api-gateway-d548b9fb4-rzvb7 to minikube
  Normal  Pulled     2m33s  kubelet, minikube  Container image "richardchesterwood/k8s-fleetman-api-gateway:performance" already present on machine
  Normal  Created    2m33s  kubelet, minikube  Created container api-gateway
  Normal  Started    2m32s  kubelet, minikube  Started container api-gateway
```
