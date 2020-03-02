```
localhost:doc5 zhao$ kubectl apply -f pods.yaml
deployment.apps/webapp configured
pod/queue unchanged
localhost:doc5 zhao$ kubectl get all
NAME                          READY   STATUS    RESTARTS   AGE
pod/queue                     1/1     Running   0          1h
pod/webapp-746ff4c965-bbhtp   1/1     Running   0          9m
pod/webapp-746ff4c965-gwkxp   1/1     Running   0          9m
pod/webapp-7jn47              1/1     Running   0          10s


NAME                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/fleetman-queue    NodePort    10.101.245.41   <none>        8161:30010/TCP   1h
service/fleetman-webapp   NodePort    10.104.2.249    <none>        80:30080/TCP     5d
service/kubernetes        ClusterIP   10.96.0.1       <none>        443/TCP          9d


NAME                     DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/webapp   2         3         1            2           9m

NAME                                DESIRED   CURRENT   READY   AGE
replicaset.apps/webapp              1         1         1       1h
replicaset.apps/webapp-746ff4c965   2         2         2       9m




localhost:doc5 zhao$ kubectl get all
NAME                          READY   STATUS    RESTARTS   AGE
pod/queue                     1/1     Running   0          1h
pod/webapp-746ff4c965-bbhtp   1/1     Running   0          9m
pod/webapp-746ff4c965-gwkxp   1/1     Running   0          9m
pod/webapp-7jn47              1/1     Running   0          13s


NAME                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/fleetman-queue    NodePort    10.101.245.41   <none>        8161:30010/TCP   1h
service/fleetman-webapp   NodePort    10.104.2.249    <none>        80:30080/TCP     5d
service/kubernetes        ClusterIP   10.96.0.1       <none>        443/TCP          9d


NAME                     DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/webapp   2         3         1            2           9m

NAME                                DESIRED   CURRENT   READY   AGE
replicaset.apps/webapp              1         1         1       1h
replicaset.apps/webapp-746ff4c965   2         2         2       9m




localhost:doc5 zhao$ kubectl rollout status
error: required resource not specified
localhost:doc5 zhao$ kubectl rollout status webapp
error: the server doesn't have a resource type "webapp"
localhost:doc5 zhao$ kubectl rollout status deploy webapp
deployment "webapp" successfully rolled out
localhost:doc5 zhao$ kubectl apply -f pods.yaml
deployment.apps/webapp configured
pod/queue unchanged
localhost:doc5 zhao$ kubectl rollout status deploy webapp
Waiting for deployment "webapp" rollout to finish: 1 out of 2 new replicas have been updated...
Waiting for deployment "webapp" rollout to finish: 1 out of 2 new replicas have been updated...
Waiting for deployment "webapp" rollout to finish: 1 out of 2 new replicas have been updated...
Waiting for deployment "webapp" rollout to finish: 1 old replicas are pending termination...
Waiting for deployment "webapp" rollout to finish: 1 old replicas are pending termination...
Waiting for deployment "webapp" rollout to finish: 1 old replicas are pending termination...
deployment "webapp" successfully rolled out
localhost:doc5 zhao$ kubectl rollout history deploy webapp
deployment.extensions/webapp
REVISION  CHANGE-CAUSE
2         <none>
3         <none>

localhost:doc5 zhao$ kubectl rollout undo deploy webapp
deployment.extensions/webapp rolled back
localhost:doc5 zhao$ kubectl rollout history deploy webapp
deployment.extensions/webapp
REVISION  CHANGE-CAUSE
3         <none>
4         <none>

localhost:doc5 zhao$ kubectl apply -f pods.yaml
deployment.apps/webapp configured
pod/queue unchanged
localhost:doc5 zhao$ kubectl get all
NAME                          READY   STATUS             RESTARTS   AGE
pod/queue                     1/1     Running            0          1h
pod/webapp-66fbdb9599-b4jq5   0/1     InvalidImageName   0          34s
pod/webapp-jvb8j              1/1     Running            0          8m
pod/webapp-mjrlb              1/1     Running            0          8m


NAME                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/fleetman-queue    NodePort    10.101.245.41   <none>        8161:30010/TCP   2h
service/fleetman-webapp   NodePort    10.104.2.249    <none>        80:30080/TCP     5d
service/kubernetes        ClusterIP   10.96.0.1       <none>        443/TCP          9d


NAME                     DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/webapp   2         3         1            2           27m

NAME                                DESIRED   CURRENT   READY   AGE
replicaset.apps/webapp              2         2         2       1h
replicaset.apps/webapp-66fbdb9599   1         1         0       34s
replicaset.apps/webapp-746ff4c965   0         0         0       27m




localhost:doc5 zhao$ kubectl get all
NAME                          READY   STATUS             RESTARTS   AGE
pod/queue                     1/1     Running            0          1h
pod/webapp-66fbdb9599-b4jq5   0/1     InvalidImageName   0          41s
pod/webapp-jvb8j              1/1     Running            0          8m
pod/webapp-mjrlb              1/1     Running            0          8m


NAME                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/fleetman-queue    NodePort    10.101.245.41   <none>        8161:30010/TCP   2h
service/fleetman-webapp   NodePort    10.104.2.249    <none>        80:30080/TCP     5d
service/kubernetes        ClusterIP   10.96.0.1       <none>        443/TCP          9d


NAME                     DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/webapp   2         3         1            2           27m

NAME                                DESIRED   CURRENT   READY   AGE
replicaset.apps/webapp              2         2         2       1h
replicaset.apps/webapp-66fbdb9599   1         1         0       41s
replicaset.apps/webapp-746ff4c965   0         0         0       27m




localhost:doc5 zhao$ kubectl get all
NAME                          READY   STATUS             RESTARTS   AGE
pod/queue                     1/1     Running            0          1h
pod/webapp-66fbdb9599-b4jq5   0/1     InvalidImageName   0          1m
pod/webapp-jvb8j              1/1     Running            0          9m
pod/webapp-mjrlb              1/1     Running            0          8m


NAME                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/fleetman-queue    NodePort    10.101.245.41   <none>        8161:30010/TCP   2h
service/fleetman-webapp   NodePort    10.104.2.249    <none>        80:30080/TCP     5d
service/kubernetes        ClusterIP   10.96.0.1       <none>        443/TCP          9d


NAME                     DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/webapp   2         3         1            2           27m

NAME                                DESIRED   CURRENT   READY   AGE
replicaset.apps/webapp              2         2         2       1h
replicaset.apps/webapp-66fbdb9599   1         1         0       1m
replicaset.apps/webapp-746ff4c965   0         0         0       27m

```
---
```
qzhaos-mbp:Chapter 10 Networking qzhao$ kubectl get all -n kube-system
NAME                                   READY   STATUS    RESTARTS   AGE
pod/coredns-6955765f44-bsshq           1/1     Running   1          7d
pod/coredns-6955765f44-cz8d5           1/1     Running   1          7d
pod/etcd-minikube                      1/1     Running   1          7d
pod/kube-apiserver-minikube            1/1     Running   1          7d
pod/kube-controller-manager-minikube   1/1     Running   1          7d
pod/kube-proxy-djt6p                   1/1     Running   1          7d
pod/kube-scheduler-minikube            1/1     Running   1          7d
pod/storage-provisioner                1/1     Running   1          7d

NAME               TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)                  AGE
service/kube-dns   ClusterIP   10.96.0.10   <none>        53/UDP,53/TCP,9153/TCP   7d

NAME                        DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR                 AGE
daemonset.apps/kube-proxy   1         1         1       1            1           beta.kubernetes.io/os=linux   7d

NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/coredns   2/2     2            2           7d

NAME                                 DESIRED   CURRENT   READY   AGE
replicaset.apps/coredns-6955765f44   2         2         2       7d
qzhaos-mbp:Chapter 10 Networking qzhao$ kubectl describe service/kube-dns -n kube-system
Name:              kube-dns
Namespace:         kube-system
Labels:            k8s-app=kube-dns
                   kubernetes.io/cluster-service=true
                   kubernetes.io/name=KubeDNS
Annotations:       prometheus.io/port: 9153
                   prometheus.io/scrape: true
Selector:          k8s-app=kube-dns
Type:              ClusterIP
IP:                10.96.0.10
Port:              dns  53/UDP
TargetPort:        53/UDP
Endpoints:         172.17.0.2:53,172.17.0.3:53
Port:              dns-tcp  53/TCP
TargetPort:        53/TCP
Endpoints:         172.17.0.2:53,172.17.0.3:53
Port:              metrics  9153/TCP
TargetPort:        9153/TCP
Endpoints:         172.17.0.2:9153,172.17.0.3:9153
Session Affinity:  None
Events:            <none>
```
