### memory limit: if over limit, container will be killed
### cpu limit: if over limit, will not allow

```
localhost:dev zhao$ cd doc13/
localhost:doc13 zhao$ ls
img			readme.md		storage.yaml
mongo-stack.yaml	services.yaml		workloads.yaml
localhost:doc13 zhao$ clear
localhost:doc13 zhao$ kubectl get all
NAME                                     READY   STATUS    RESTARTS   AGE
pod/api-gateway-77dff9778b-hg98z         1/1     Running   3          6d4h
pod/mongodb-5dc79669d-db65z              1/1     Running   1          3d23h
pod/position-simulator-96f46d659-l6n27   1/1     Running   1          4d1h
pod/position-tracker-f6f5dd79d-c7vh4     1/1     Running   3          6d3h
pod/queue-8b577ccc6-xllpn                1/1     Running   3          6d4h
pod/webapp-7bf85bf85f-n9nr4              0/1     Error     7          6d4h


NAME                                TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                          AGE
service/fleetman-api-gateway        NodePort    10.98.203.46     <none>        8080:30020/TCP                   6d4h
service/fleetman-mongodb            ClusterIP   10.111.156.9     <none>        27017/TCP                        5d22h
service/fleetman-position-tracker   ClusterIP   10.99.19.185     <none>        8080/TCP                         6d4h
service/fleetman-queue              NodePort    10.106.133.70    <none>        8161:30010/TCP,61616:31227/TCP   6d4h
service/fleetman-webapp             NodePort    10.110.214.192   <none>        80:30080/TCP                     6d4h
service/kubernetes                  ClusterIP   10.96.0.1        <none>        443/TCP                          6d4h


NAME                                 READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/api-gateway          1/1     1            1           6d4h
deployment.apps/mongodb              1/1     1            1           6d3h
deployment.apps/position-simulator   1/1     1            1           6d4h
deployment.apps/position-tracker     1/1     1            1           6d4h
deployment.apps/queue                1/1     1            1           6d4h
deployment.apps/webapp               0/1     1            0           6d4h

NAME                                           DESIRED   CURRENT   READY   AGE
replicaset.apps/api-gateway-6b94f4bcf5         0         0         0       6d4h
replicaset.apps/api-gateway-77dff9778b         1         1         1       6d4h
replicaset.apps/mongodb-59458887cf             0         0         0       5d22h
replicaset.apps/mongodb-5dbdc5d5b9             0         0         0       6d3h
replicaset.apps/mongodb-5dc79669d              1         1         1       4d
replicaset.apps/mongodb-6dd67d6d46             0         0         0       5d22h
replicaset.apps/position-simulator-96f46d659   1         1         1       6d4h
replicaset.apps/position-simulator-d5fdcbc98   0         0         0       6d4h
replicaset.apps/position-tracker-795b4ffb77    0         0         0       6d4h
replicaset.apps/position-tracker-cd786fdfb     0         0         0       6d4h
replicaset.apps/position-tracker-f6f5dd79d     1         1         1       6d3h
replicaset.apps/queue-7d94749657               0         0         0       6d4h
replicaset.apps/queue-8b577ccc6                1         1         1       6d4h
replicaset.apps/webapp-5c5dcc8d66              0         0         0       6d4h
replicaset.apps/webapp-7bf85bf85f              1         1         0       6d4h




localhost:doc13 zhao$ kubectl delete -f .
deployment.apps "mongodb" deleted
service "fleetman-mongodb" deleted
service "fleetman-webapp" deleted
service "fleetman-queue" deleted
service "fleetman-position-tracker" deleted
service "fleetman-api-gateway" deleted
persistentvolumeclaim "mongo-pvc" deleted
persistentvolume "local-storage" deleted
deployment.apps "queue" deleted
deployment.apps "position-simulator" deleted
deployment.apps "position-tracker" deleted
deployment.apps "api-gateway" deleted
deployment.apps "webapp" deleted
localhost:doc13 zhao$
localhost:doc13 zhao$ kubectl get all


NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   6d4h


```
check memory, it will not show on minikube, only show on AWS
```
localhost:doc13 zhao$ kubectl get nodes
NAME       STATUS   ROLES    AGE    VERSION
minikube   Ready    master   6d4h   v1.15.0
localhost:doc13 zhao$ kubectl describe node minikube
Name:               minikube
Roles:              master
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=minikube
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/master=
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Tue, 09 Jul 2019 11:20:29 -0400
Taints:             <none>
Unschedulable:      false
Conditions:
  Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----             ------  -----------------                 ------------------                ------                       -------
  MemoryPressure   False   Mon, 15 Jul 2019 16:04:02 -0400   Tue, 09 Jul 2019 11:20:26 -0400   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure     False   Mon, 15 Jul 2019 16:04:02 -0400   Tue, 09 Jul 2019 11:20:26 -0400   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure      False   Mon, 15 Jul 2019 16:04:02 -0400   Tue, 09 Jul 2019 11:20:26 -0400   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready            True    Mon, 15 Jul 2019 16:04:02 -0400   Tue, 09 Jul 2019 11:20:26 -0400   KubeletReady                 kubelet is posting ready status
Addresses:
  InternalIP:  10.0.2.15
  Hostname:    minikube
Capacity:
 cpu:                2
 ephemeral-storage:  17784772Ki
 hugepages-2Mi:      0
 memory:             4037040Ki
 pods:               110
Allocatable:
 cpu:                2
 ephemeral-storage:  16390445849
 hugepages-2Mi:      0
 memory:             3934640Ki
 pods:               110
System Info:
 Machine ID:                 cd52b0e231b541a98514f695d375fc3d
 System UUID:                BE29AF50-D8DB-4419-A795-7C74BCE71771
 Boot ID:                    7ea0cac1-6b10-4a7a-b345-6adb90ee1d47
 Kernel Version:             4.15.0
 OS Image:                   Buildroot 2018.05.3
 Operating System:           linux
 Architecture:               amd64
 Container Runtime Version:  docker://18.9.6
 Kubelet Version:            v1.15.0
 Kube-Proxy Version:         v1.15.0
Non-terminated Pods:         (9 in total)
  Namespace                  Name                                CPU Requests  CPU Limits  Memory Requests  Memory Limits  AGE
  ---------                  ----                                ------------  ----------  ---------------  -------------  ---
  kube-system                coredns-5c98db65d4-cqxrm            100m (5%)     0 (0%)      70Mi (1%)        170Mi (4%)     6d4h
  kube-system                coredns-5c98db65d4-qt9rf            100m (5%)     0 (0%)      70Mi (1%)        170Mi (4%)     6d4h
  kube-system                etcd-minikube                       0 (0%)        0 (0%)      0 (0%)           0 (0%)         6d4h
  kube-system                kube-addon-manager-minikube         5m (0%)       0 (0%)      50Mi (1%)        0 (0%)         6d4h
  kube-system                kube-apiserver-minikube             250m (12%)    0 (0%)      0 (0%)           0 (0%)         6d4h
  kube-system                kube-controller-manager-minikube    200m (10%)    0 (0%)      0 (0%)           0 (0%)         6d4h
  kube-system                kube-proxy-d2gnv                    0 (0%)        0 (0%)      0 (0%)           0 (0%)         6d4h
  kube-system                kube-scheduler-minikube             100m (5%)     0 (0%)      0 (0%)           0 (0%)         6d4h
  kube-system                storage-provisioner                 0 (0%)        0 (0%)      0 (0%)           0 (0%)         6d4h
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests    Limits
  --------           --------    ------
  cpu                755m (37%)  0 (0%)
  memory             190Mi (4%)  340Mi (8%)
  ephemeral-storage  0 (0%)      0 (0%)
Events:
  Type    Reason                   Age                  From                  Message
  ----    ------                   ----                 ----                  -------
  Normal  Starting                 9m2s                 kubelet, minikube     Starting kubelet.
  Normal  NodeHasSufficientMemory  9m2s (x8 over 9m2s)  kubelet, minikube     Node minikube status is now: NodeHasSufficientMemory
  Normal  NodeHasNoDiskPressure    9m2s (x8 over 9m2s)  kubelet, minikube     Node minikube status is now: NodeHasNoDiskPressure
  Normal  NodeHasSufficientPID     9m2s (x7 over 9m2s)  kubelet, minikube     Node minikube status is now: NodeHasSufficientPID
  Normal  NodeAllocatableEnforced  9m2s                 kubelet, minikube     Updated Node Allocatable limit across pods
  Normal  Starting                 8m23s                kube-proxy, minikube  Starting kube-proxy.
```



```
localhost:doc13 zhao$ kubectl apply -f resource-testing.yaml
deployment.apps/queue created
localhost:doc13 zhao$ kubectl get all
NAME                         READY   STATUS    RESTARTS   AGE
pod/queue-84c666c476-sqfhf   1/1     Running   0          34s


NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   6d4h


NAME                    READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/queue   1/1     1            1           34s

NAME                               DESIRED   CURRENT   READY   AGE
replicaset.apps/queue-84c666c476   1         1         1       34s
localhost:doc13 zhao$ kubectl describe pod queue-84c666c476-sqfhf
Name:           queue-84c666c476-sqfhf
Namespace:      default
Priority:       0
Node:           minikube/10.0.2.15
Start Time:     Mon, 15 Jul 2019 16:12:24 -0400
Labels:         app=queue
                pod-template-hash=84c666c476
Annotations:    <none>
Status:         Running
IP:             172.17.0.2
Controlled By:  ReplicaSet/queue-84c666c476
Containers:
  queue:
    Container ID:   docker://558936616beb1f29b5441ee426218f660a2fec94fb088e7fb86fc2d0f0974bde
    Image:          richardchesterwood/k8s-fleetman-queue:release2
    Image ID:       docker-pullable://richardchesterwood/k8s-fleetman-queue@sha256:f7778362d6144a3c58bf2e34eb56c9c5bb038f150eb8c9599ca61862e4e64937
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Mon, 15 Jul 2019 16:12:25 -0400
    Ready:          True
    Restart Count:  0
    Requests:
      memory:     1500Mi
    Environment:  <none>
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
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  95s   default-scheduler  Successfully assigned default/queue-84c666c476-sqfhf to minikube
  Normal  Pulled     95s   kubelet, minikube  Container image "richardchesterwood/k8s-fleetman-queue:release2" already present on machine
  Normal  Created    95s   kubelet, minikube  Created container queue
  Normal  Started    94s   kubelet, minikube  Started container queue
```

```
localhost:doc13 zhao$ kubectl get all --all-namespaces
NAMESPACE     NAME                                   READY   STATUS    RESTARTS   AGE
default       pod/queue-84c666c476-sqfhf             1/1     Running   0          2m40s
kube-system   pod/coredns-5c98db65d4-cqxrm           1/1     Running   5          6d4h
kube-system   pod/coredns-5c98db65d4-qt9rf           1/1     Running   5          6d4h
kube-system   pod/etcd-minikube                      1/1     Running   3          6d4h
kube-system   pod/kube-addon-manager-minikube        1/1     Running   3          6d4h
kube-system   pod/kube-apiserver-minikube            1/1     Running   3          6d4h
kube-system   pod/kube-controller-manager-minikube   1/1     Running   3          6d4h
kube-system   pod/kube-proxy-d2gnv                   1/1     Running   3          6d4h
kube-system   pod/kube-scheduler-minikube            1/1     Running   3          6d4h
kube-system   pod/storage-provisioner                1/1     Running   5          6d4h


NAMESPACE     NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)                  AGE
default       service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP                  6d4h
kube-system   service/kube-dns     ClusterIP   10.96.0.10   <none>        53/UDP,53/TCP,9153/TCP   6d4h

NAMESPACE     NAME                        DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR                 AGE
kube-system   daemonset.apps/kube-proxy   1         1         1       1            1           beta.kubernetes.io/os=linux   6d4h

NAMESPACE     NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
default       deployment.apps/queue     1/1     1            1           2m40s
kube-system   deployment.apps/coredns   2/2     2            2           6d4h

NAMESPACE     NAME                                 DESIRED   CURRENT   READY   AGE
default       replicaset.apps/queue-84c666c476     1         1         1       2m40s
kube-system   replicaset.apps/coredns-5c98db65d4   2         2         2       6d4h
```

```
localhost:doc13 zhao$ kubectl describe node minikube
Name:               minikube
Roles:              master
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=minikube
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/master=
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Tue, 09 Jul 2019 11:20:29 -0400
Taints:             <none>
Unschedulable:      false
Conditions:
  Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----             ------  -----------------                 ------------------                ------                       -------
  MemoryPressure   False   Mon, 15 Jul 2019 16:15:02 -0400   Tue, 09 Jul 2019 11:20:26 -0400   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure     False   Mon, 15 Jul 2019 16:15:02 -0400   Tue, 09 Jul 2019 11:20:26 -0400   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure      False   Mon, 15 Jul 2019 16:15:02 -0400   Tue, 09 Jul 2019 11:20:26 -0400   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready            True    Mon, 15 Jul 2019 16:15:02 -0400   Tue, 09 Jul 2019 11:20:26 -0400   KubeletReady                 kubelet is posting ready status
Addresses:
  InternalIP:  10.0.2.15
  Hostname:    minikube
Capacity:
 cpu:                2
 ephemeral-storage:  17784772Ki
 hugepages-2Mi:      0
 memory:             4037040Ki
 pods:               110
Allocatable:
 cpu:                2
 ephemeral-storage:  16390445849
 hugepages-2Mi:      0
 memory:             3934640Ki
 pods:               110
System Info:
 Machine ID:                 cd52b0e231b541a98514f695d375fc3d
 System UUID:                BE29AF50-D8DB-4419-A795-7C74BCE71771
 Boot ID:                    7ea0cac1-6b10-4a7a-b345-6adb90ee1d47
 Kernel Version:             4.15.0
 OS Image:                   Buildroot 2018.05.3
 Operating System:           linux
 Architecture:               amd64
 Container Runtime Version:  docker://18.9.6
 Kubelet Version:            v1.15.0
 Kube-Proxy Version:         v1.15.0
Non-terminated Pods:         (10 in total)
  Namespace                  Name                                CPU Requests  CPU Limits  Memory Requests  Memory Limits  AGE
  ---------                  ----                                ------------  ----------  ---------------  -------------  ---
  default                    queue-84c666c476-sqfhf              0 (0%)        0 (0%)      1500Mi (39%)     0 (0%)         3m35s
  kube-system                coredns-5c98db65d4-cqxrm            100m (5%)     0 (0%)      70Mi (1%)        170Mi (4%)     6d4h
  kube-system                coredns-5c98db65d4-qt9rf            100m (5%)     0 (0%)      70Mi (1%)        170Mi (4%)     6d4h
  kube-system                etcd-minikube                       0 (0%)        0 (0%)      0 (0%)           0 (0%)         6d4h
  kube-system                kube-addon-manager-minikube         5m (0%)       0 (0%)      50Mi (1%)        0 (0%)         6d4h
  kube-system                kube-apiserver-minikube             250m (12%)    0 (0%)      0 (0%)           0 (0%)         6d4h
  kube-system                kube-controller-manager-minikube    200m (10%)    0 (0%)      0 (0%)           0 (0%)         6d4h
  kube-system                kube-proxy-d2gnv                    0 (0%)        0 (0%)      0 (0%)           0 (0%)         6d4h
  kube-system                kube-scheduler-minikube             100m (5%)     0 (0%)      0 (0%)           0 (0%)         6d4h
  kube-system                storage-provisioner                 0 (0%)        0 (0%)      0 (0%)           0 (0%)         6d4h
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests      Limits
  --------           --------      ------
  cpu                755m (37%)    0 (0%)
  memory             1690Mi (43%)  340Mi (8%)
  ephemeral-storage  0 (0%)        0 (0%)
Events:
  Type    Reason                   Age                From                  Message
  ----    ------                   ----               ----                  -------
  Normal  Starting                 20m                kubelet, minikube     Starting kubelet.
  Normal  NodeHasSufficientMemory  20m (x8 over 20m)  kubelet, minikube     Node minikube status is now: NodeHasSufficientMemory
  Normal  NodeHasNoDiskPressure    20m (x8 over 20m)  kubelet, minikube     Node minikube status is now: NodeHasNoDiskPressure
  Normal  NodeHasSufficientPID     20m (x7 over 20m)  kubelet, minikube     Node minikube status is now: NodeHasSufficientPID
  Normal  NodeAllocatableEnforced  20m                kubelet, minikube     Updated Node Allocatable limit across pods
  Normal  Starting                 19m                kube-proxy, minikube  Starting kube-proxy.
localhost:doc13 zhao$
```

change replicas to 2
```
kubectl apply -f resource-testing.yaml
localhost:doc13 zhao$ kubectl get all
NAME                         READY   STATUS    RESTARTS   AGE
pod/queue-84c666c476-qbrhj   1/1     Running   0          48s
pod/queue-84c666c476-sqfhf   1/1     Running   0          6m44s


NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   6d4h


NAME                    READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/queue   2/2     2            2           6m44s

NAME                               DESIRED   CURRENT   READY   AGE
replicaset.apps/queue-84c666c476   2         2         2       6m44s
localhost:doc13 zhao$ kubectl describe node minikube
Name:               minikube
Roles:              master
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=minikube
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/master=
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Tue, 09 Jul 2019 11:20:29 -0400
Taints:             <none>
Unschedulable:      false
Conditions:
  Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----             ------  -----------------                 ------------------                ------                       -------
  MemoryPressure   False   Mon, 15 Jul 2019 16:19:02 -0400   Tue, 09 Jul 2019 11:20:26 -0400   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure     False   Mon, 15 Jul 2019 16:19:02 -0400   Tue, 09 Jul 2019 11:20:26 -0400   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure      False   Mon, 15 Jul 2019 16:19:02 -0400   Tue, 09 Jul 2019 11:20:26 -0400   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready            True    Mon, 15 Jul 2019 16:19:02 -0400   Tue, 09 Jul 2019 11:20:26 -0400   KubeletReady                 kubelet is posting ready status
Addresses:
  InternalIP:  10.0.2.15
  Hostname:    minikube
Capacity:
 cpu:                2
 ephemeral-storage:  17784772Ki
 hugepages-2Mi:      0
 memory:             4037040Ki
 pods:               110
Allocatable:
 cpu:                2
 ephemeral-storage:  16390445849
 hugepages-2Mi:      0
 memory:             3934640Ki
 pods:               110
System Info:
 Machine ID:                 cd52b0e231b541a98514f695d375fc3d
 System UUID:                BE29AF50-D8DB-4419-A795-7C74BCE71771
 Boot ID:                    7ea0cac1-6b10-4a7a-b345-6adb90ee1d47
 Kernel Version:             4.15.0
 OS Image:                   Buildroot 2018.05.3
 Operating System:           linux
 Architecture:               amd64
 Container Runtime Version:  docker://18.9.6
 Kubelet Version:            v1.15.0
 Kube-Proxy Version:         v1.15.0
Non-terminated Pods:         (11 in total)
  Namespace                  Name                                CPU Requests  CPU Limits  Memory Requests  Memory Limits  AGE
  ---------                  ----                                ------------  ----------  ---------------  -------------  ---
  default                    queue-84c666c476-qbrhj              0 (0%)        0 (0%)      1500Mi (39%)     0 (0%)         66s
  default                    queue-84c666c476-sqfhf              0 (0%)        0 (0%)      1500Mi (39%)     0 (0%)         7m2s
  kube-system                coredns-5c98db65d4-cqxrm            100m (5%)     0 (0%)      70Mi (1%)        170Mi (4%)     6d4h
  kube-system                coredns-5c98db65d4-qt9rf            100m (5%)     0 (0%)      70Mi (1%)        170Mi (4%)     6d4h
  kube-system                etcd-minikube                       0 (0%)        0 (0%)      0 (0%)           0 (0%)         6d4h
  kube-system                kube-addon-manager-minikube         5m (0%)       0 (0%)      50Mi (1%)        0 (0%)         6d4h
  kube-system                kube-apiserver-minikube             250m (12%)    0 (0%)      0 (0%)           0 (0%)         6d4h
  kube-system                kube-controller-manager-minikube    200m (10%)    0 (0%)      0 (0%)           0 (0%)         6d4h
  kube-system                kube-proxy-d2gnv                    0 (0%)        0 (0%)      0 (0%)           0 (0%)         6d4h
  kube-system                kube-scheduler-minikube             100m (5%)     0 (0%)      0 (0%)           0 (0%)         6d4h
  kube-system                storage-provisioner                 0 (0%)        0 (0%)      0 (0%)           0 (0%)         6d4h
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests      Limits
  --------           --------      ------
  cpu                755m (37%)    0 (0%)
  memory             3190Mi (83%)  340Mi (8%)
  ephemeral-storage  0 (0%)        0 (0%)
Events:
  Type    Reason                   Age                From                  Message
  ----    ------                   ----               ----                  -------
  Normal  Starting                 23m                kubelet, minikube     Starting kubelet.
  Normal  NodeHasSufficientMemory  23m (x8 over 23m)  kubelet, minikube     Node minikube status is now: NodeHasSufficientMemory
  Normal  NodeHasNoDiskPressure    23m (x8 over 23m)  kubelet, minikube     Node minikube status is now: NodeHasNoDiskPressure
  Normal  NodeHasSufficientPID     23m (x7 over 23m)  kubelet, minikube     Node minikube status is now: NodeHasSufficientPID
  Normal  NodeAllocatableEnforced  23m                kubelet, minikube     Updated Node Allocatable limit across pods
  Normal  Starting                 23m                kube-proxy, minikube  Starting kube-proxy.
localhost:doc13 zhao$
```

change replicaset to 3
```
localhost:doc13 zhao$ kubectl apply -f resource-testing.yaml
deployment.apps/queue configured
localhost:doc13 zhao$ kubectl get all
NAME                         READY   STATUS    RESTARTS   AGE
pod/queue-84c666c476-8z89d   0/1     Pending   0          19s
pod/queue-84c666c476-qbrhj   1/1     Running   0          7m32s
pod/queue-84c666c476-sqfhf   1/1     Running   0          13m


NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   6d5h


NAME                    READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/queue   2/3     3            2           13m

NAME                               DESIRED   CURRENT   READY   AGE
replicaset.apps/queue-84c666c476   3         3         2       13m

localhost:doc13 zhao$ kubectl describe pod/queue-84c666c476-8z89d
Name:           queue-84c666c476-8z89d
Namespace:      default
Priority:       0
Node:           <none>
Labels:         app=queue
                pod-template-hash=84c666c476
Annotations:    <none>
Status:         Pending
IP:
Controlled By:  ReplicaSet/queue-84c666c476
Containers:
  queue:
    Image:      richardchesterwood/k8s-fleetman-queue:release2
    Port:       <none>
    Host Port:  <none>
    Requests:
      memory:     1500Mi
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-n9pk7 (ro)
Conditions:
  Type           Status
  PodScheduled   False
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
  Type     Reason            Age               From               Message
  ----     ------            ----              ----               -------
  Warning  FailedScheduling  1s (x3 over 82s)  default-scheduler  0/1 nodes are available: 1 Insufficient memory.
```

```
localhost:doc13 zhao$ kubectl get all
NAME                         READY   STATUS    RESTARTS   AGE
pod/queue-5fc584d575-cfzd9   0/1     Pending   0          3m5s
pod/queue-5fc584d575-k8lkr   1/1     Running   0          3m5s


NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   6d5h


NAME                    READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/queue   1/2     2            1           27m

NAME                               DESIRED   CURRENT   READY   AGE
replicaset.apps/queue-5598cd977b   0         0         0       5m54s
replicaset.apps/queue-5fc584d575   2         2         1       3m5s
replicaset.apps/queue-84c666c476   0         0         0       27m




localhost:doc13 zhao$ kubectl describe pod/queue-5fc584d575-cfzd9
Name:           queue-5fc584d575-cfzd9
Namespace:      default
Priority:       0
Node:           <none>
Labels:         app=queue
                pod-template-hash=5fc584d575
Annotations:    <none>
Status:         Pending
IP:
Controlled By:  ReplicaSet/queue-5fc584d575
Containers:
  queue:
    Image:      richardchesterwood/k8s-fleetman-queue:release2
    Port:       <none>
    Host Port:  <none>
    Requests:
      cpu:        1
      memory:     300Mi
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-n9pk7 (ro)
Conditions:
  Type           Status
  PodScheduled   False
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
  Type     Reason            Age                  From               Message
  ----     ------            ----                 ----               -------
  Warning  FailedScheduling  48s (x4 over 3m18s)  default-scheduler  0/1 nodes are available: 1 Insufficient cpu.
```
