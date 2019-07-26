# ConfigMap
```
localhost:doc19 zhao$ cat database-config.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: global-database-config
  namespace: default
data:
  database.properties: |
    database.url=https://mydatabaseserver.somewhere.com:3306
    database.password=P@SSW0rd1
localhost:doc19 zhao$ kubectl apply -f database-config.yaml
configmap/global-database-config created
localhost:doc19 zhao$ kubectl get cm
NAME                     DATA   AGE
global-database-config   1      15s
localhost:doc19 zhao$ kubectl describe cm global-database-config
Name:         global-database-config
Namespace:    default
Labels:       <none>
Annotations:  kubectl.kubernetes.io/last-applied-configuration:
                {"apiVersion":"v1","data":{"database.properties":"database.url=https://mydatabaseserver.somewhere.com:3306\ndatabase.password=P@SSW0rd1\n"...

Data
====
database.properties:
----
database.url=https://mydatabaseserver.somewhere.com:3306
database.password=P@SSW0rd1

Events:  <none>
localhost:doc19 zhao$
```
```
kubectl exec -it <pod_name> bash
ls
echo $DATABASE_URL
echo $DATABASE_PASSWORD
```
---
set ConfigMap with envFrom
![](img/1.png)
![](img/2.png)
```
localhost:doc19 zhao$ kubectl describe pod position-simulator-585b7d658b-kwbp4
Name:           position-simulator-585b7d658b-kwbp4
Namespace:      default
Priority:       0
Node:           minikube/10.0.2.15
Start Time:     Thu, 25 Jul 2019 17:45:08 -0400
Labels:         app=position-simulator
                pod-template-hash=585b7d658b
Annotations:    <none>
Status:         Running
IP:             172.17.0.15
Controlled By:  ReplicaSet/position-simulator-585b7d658b
Containers:
  position-simulator:
    Container ID:   docker://5e0a8e8e1844ed9fe4915c43f5abd5afafb2c9996692ad1827f823210f50c4a2
    Image:          richardchesterwood/k8s-fleetman-position-simulator:release2
    Image ID:       docker-pullable://richardchesterwood/k8s-fleetman-position-simulator@sha256:0b540a28f5a617b5d5643e82939018414a0af6a7ed0c0f4bb1e50cddb7fd5a8d
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Thu, 25 Jul 2019 17:45:36 -0400
    Ready:          True
    Restart Count:  0
    Environment Variables from:
      global-database-config-v3  ConfigMap  Optional: false
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
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason     Age                  From               Message
  ----     ------     ----                 ----               -------
  Normal   Scheduled  117s                 default-scheduler  Successfully assigned default/position-simulator-585b7d658b-kwbp4 to minikube
  Warning  Failed     104s (x3 over 116s)  kubelet, minikube  Error: configmap "global-database-config-v3" not found
  Normal   Pulled     89s (x4 over 116s)   kubelet, minikube  Container image "richardchesterwood/k8s-fleetman-position-simulator:release2" already present on machine
  Normal   Created    89s                  kubelet, minikube  Created container position-simulator
  Normal   Started    89s                  kubelet, minikube  Started container position-simulator
localhost:doc19 zhao$
```
---
set ConfigMap with VolumeMount
![](img/3.png)
![](img/4.png)
---
# Secrets:

![](img/5.png)
![](img/6.png)
![](img/7.png)
![](img/8.png)


https://www.youtube.com/watch?v=DiJ0Na8rWvc&t=563s
