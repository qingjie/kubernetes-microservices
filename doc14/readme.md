
```
localhost:doc13 zhao$ kubectl get all
NAME                         READY   STATUS    RESTARTS   AGE
pod/queue-5598cd977b-6sz8h   1/1     Running   0          34m
pod/queue-5598cd977b-pspfm   1/1     Running   0          34m


NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   6d5h


NAME                    READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/queue   2/2     2            2           62m

NAME                               DESIRED   CURRENT   READY   AGE
replicaset.apps/queue-5598cd977b   2         2         2       41m
replicaset.apps/queue-5fc584d575   0         0         0       38m
replicaset.apps/queue-84c666c476   0         0         0       62m




localhost:doc13 zhao$ kubectl top pod
Error from server (NotFound): the server could not find the requested resource (get services http:heapster:)
localhost:doc13 zhao$ kubectl top node
Error from server (NotFound): the server could not find the requested resource (get services http:heapster:)
localhost:doc13 zhao$ minikube addons list
- addon-manager: enabled
- dashboard: disabled
- default-storageclass: enabled
- efk: disabled
- freshpod: disabled
- gvisor: disabled
- heapster: disabled
- ingress: disabled
- logviewer: disabled
- metrics-server: disabled
- nvidia-driver-installer: disabled
- nvidia-gpu-device-plugin: disabled
- registry: disabled
- registry-creds: disabled
- storage-provisioner: enabled
- storage-provisioner-gluster: disabled

localhost:doc13 zhao$ minikube addons enable metrics-server
✅  metrics-server was successfully enabled
localhost:doc13 zhao$ kubectl top pod
W0715 17:21:00.194296   23863 top_pod.go:266] Metrics not available for pod default/queue-5598cd977b-6sz8h, age: 40m6.194278s
error: Metrics not available for pod default/queue-5598cd977b-6sz8h, age: 40m6.194278s
localhost:doc13 zhao$ kubectl get all -n kube-system
NAME                                   READY   STATUS    RESTARTS   AGE
pod/coredns-5c98db65d4-cqxrm           1/1     Running   5          6d6h
pod/coredns-5c98db65d4-qt9rf           1/1     Running   5          6d6h
pod/etcd-minikube                      1/1     Running   3          6d6h
pod/kube-addon-manager-minikube        1/1     Running   3          6d6h
pod/kube-apiserver-minikube            1/1     Running   3          6d6h
pod/kube-controller-manager-minikube   1/1     Running   3          6d6h
pod/kube-proxy-d2gnv                   1/1     Running   3          6d6h
pod/kube-scheduler-minikube            1/1     Running   3          6d6h
pod/metrics-server-84bb785897-m9dk4    1/1     Running   0          109s
pod/storage-provisioner                1/1     Running   5          6d6h


NAME                     TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)                  AGE
service/kube-dns         ClusterIP   10.96.0.10     <none>        53/UDP,53/TCP,9153/TCP   6d6h
service/metrics-server   ClusterIP   10.106.141.2   <none>        443/TCP                  109s

NAME                        DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR                 AGE
daemonset.apps/kube-proxy   1         1         1       1            1           beta.kubernetes.io/os=linux   6d6h

NAME                             READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/coredns          2/2     2            2           6d6h
deployment.apps/metrics-server   1/1     1            1           109s

NAME                                        DESIRED   CURRENT   READY   AGE
replicaset.apps/coredns-5c98db65d4          2         2         2       6d6h
replicaset.apps/metrics-server-84bb785897   1         1         1       109s
localhost:doc13 zhao$ clear
localhost:doc13 zhao$ kubectl top pod
NAME                     CPU(cores)   MEMORY(bytes)
queue-5598cd977b-6sz8h   0m           233Mi
queue-5598cd977b-pspfm   0m           225Mi
localhost:doc13 zhao$ kubectl top node
NAME       CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%
minikube   81m          4%     1370Mi          35%
localhost:doc13 zhao$ kubectl delete -f resource-testing.yaml
deployment.apps "queue" deleted
```

```
localhost:doc14 zhao$ kubectl apply -f storage.yaml
localhost:doc14 zhao$ kubectl apply -f workloads.yaml
localhost:doc14 zhao$ kubectl apply -f services.yaml
localhost:doc14 zhao$ kubectl apply -f mongo-stack.yaml
localhost:doc14 zhao$ kubectl top pod
NAME                                 CPU(cores)   MEMORY(bytes)
api-gateway-77dff9778b-hcljb         45m          495Mi
mongodb-5dc79669d-r5g2c              7m           140Mi
position-simulator-96f46d659-dxzzp   23m          267Mi
position-tracker-f6f5dd79d-b8q77     59m          390Mi
queue-5798db7fdb-b89tc               46m          300Mi
webapp-7bf85bf85f-lf8x8              0m           4Mi
localhost:doc14 zhao$ kubectl top node
NAME       CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%
minikube   278m         13%    2489Mi          64%
```

```
localhost:doc14 zhao$ minikube addons enable dashboard
✅  dashboard was successfully enabled
ocalhost:doc14 zhao$ kubectl get all -n kube-system
NAME                                   READY   STATUS    RESTARTS   AGE
pod/coredns-5c98db65d4-cqxrm           1/1     Running   5          6d6h
pod/coredns-5c98db65d4-qt9rf           1/1     Running   5          6d6h
pod/etcd-minikube                      1/1     Running   3          6d6h
pod/kube-addon-manager-minikube        1/1     Running   3          6d6h
pod/kube-apiserver-minikube            1/1     Running   3          6d6h
pod/kube-controller-manager-minikube   1/1     Running   3          6d6h
pod/kube-proxy-d2gnv                   1/1     Running   3          6d6h
pod/kube-scheduler-minikube            1/1     Running   3          6d6h
pod/metrics-server-84bb785897-m9dk4    1/1     Running   0          19m
pod/storage-provisioner                1/1     Running   5          6d6h


NAME                     TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)                  AGE
service/kube-dns         ClusterIP   10.96.0.10     <none>        53/UDP,53/TCP,9153/TCP   6d6h
service/metrics-server   ClusterIP   10.106.141.2   <none>        443/TCP                  19m

NAME                        DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR                 AGE
daemonset.apps/kube-proxy   1         1         1       1            1           beta.kubernetes.io/os=linux   6d6h

NAME                             READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/coredns          2/2     2            2           6d6h
deployment.apps/metrics-server   1/1     1            1           19m

NAME                                        DESIRED   CURRENT   READY   AGE
replicaset.apps/coredns-5c98db65d4          2         2         2       6d6h
replicaset.apps/metrics-server-84bb785897   1         1         1       19m
localhost:doc14 zhao$ minikube dashboard
```
