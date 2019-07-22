after you change image
from richardchesterwood/k8s-fleetman-api-gateway:release2
to richardchesterwood/k8s-fleetman-api-gateway:performance
```
localhost:doc14 zhao$ kubectl apply -f workloads.yaml
kubectl get all

```
http://192.168.99.106:30080/
This is for API gateway
http://192.168.99.106:30080/api
http://192.168.99.106:30080/api/panic

make sure metrics-server is enabled
```
localhost:doc14 zhao$ minikube addons list
- addon-manager: enabled
- dashboard: enabled
- default-storageclass: enabled
- efk: disabled
- freshpod: disabled
- gvisor: disabled
- heapster: disabled
- ingress: disabled
- logviewer: disabled
- metrics-server: enabled
- nvidia-driver-installer: disabled
- nvidia-gpu-device-plugin: disabled
- registry: disabled
- registry-creds: disabled
- storage-provisioner: enabled
- storage-provisioner-gluster: disabled
```

```
localhost:doc14 zhao$ kubectl top pod
NAME                                 CPU(cores)   MEMORY(bytes)
api-gateway-9d5546845-t8t69          3m           162Mi
mongodb-5dc79669d-r5g2c              4m           221Mi
position-simulator-96f46d659-dxzzp   10m          507Mi
position-tracker-f6f5dd79d-b8q77     5m           515Mi
queue-5798db7fdb-b89tc               16m          214Mi
webapp-7bf85bf85f-lf8x8              0m           4Mi
localhost:doc14 zhao$ kubectl top node
NAME       CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%
minikube   135m         6%     2777Mi          72%
```

```
localhost:doc14 zhao$ kubectl autoscale deployment api-gateway --cpu-percent 400 --min 1 --max 4
horizontalpodautoscaler.autoscaling/api-gateway autoscaled
localhost:doc14 zhao$ kubectl get hpa
NAME          REFERENCE                TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
api-gateway   Deployment/api-gateway   4%/400%   1         4         1          29s
localhost:doc14 zhao$ kubectl top pod
NAME                                 CPU(cores)   MEMORY(bytes)
api-gateway-57579fc57b-52vn8         3m           162Mi
mongodb-5dc79669d-r5g2c              5m           223Mi
position-simulator-96f46d659-dxzzp   10m          480Mi
position-tracker-f6f5dd79d-b8q77     5m           514Mi
queue-5798db7fdb-b89tc               16m          225Mi
webapp-7bf85bf85f-lf8x8              0m           4Mi
```

```
localhost:doc14 zhao$ kubectl describe hpa api-gateway
Name:                                                  api-gateway
Namespace:                                             default
Labels:                                                <none>
Annotations:                                           <none>
CreationTimestamp:                                     Mon, 22 Jul 2019 17:46:45 -0400
Reference:                                             Deployment/api-gateway
Metrics:                                               ( current / target )
  resource cpu on pods  (as a percentage of request):  6% (3m) / 400%
Min replicas:                                          1
Max replicas:                                          4
Deployment pods:                                       1 current / 1 desired
Conditions:
  Type            Status  Reason              Message
  ----            ------  ------              -------
  AbleToScale     True    ReadyForNewScale    recommended size matches current size
  ScalingActive   True    ValidMetricFound    the HPA was able to successfully calculate a replica count from cpu resource utilization (percentage of request)
  ScalingLimited  False   DesiredWithinRange  the desired count is within the acceptable range
Events:           <none>
localhost:doc14 zhao$ kubectl get hpa api-gateway
NAME          REFERENCE                TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
api-gateway   Deployment/api-gateway   6%/400%   1         4         1          7m27s
localhost:doc14 zhao$ kubectl get hpa api-gateway -o yaml
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  annotations:
    autoscaling.alpha.kubernetes.io/conditions: '[{"type":"AbleToScale","status":"True","lastTransitionTime":"2019-07-22T21:47:00Z","reason":"ReadyForNewScale","message":"recommended
      size matches current size"},{"type":"ScalingActive","status":"True","lastTransitionTime":"2019-07-22T21:47:00Z","reason":"ValidMetricFound","message":"the
      HPA was able to successfully calculate a replica count from cpu resource utilization
      (percentage of request)"},{"type":"ScalingLimited","status":"False","lastTransitionTime":"2019-07-22T21:47:00Z","reason":"DesiredWithinRange","message":"the
      desired count is within the acceptable range"}]'
    autoscaling.alpha.kubernetes.io/current-metrics: '[{"type":"Resource","resource":{"name":"cpu","currentAverageUtilization":6,"currentAverageValue":"3m"}}]'
  creationTimestamp: "2019-07-22T21:46:45Z"
  name: api-gateway
  namespace: default
  resourceVersion: "187044"
  selfLink: /apis/autoscaling/v1/namespaces/default/horizontalpodautoscalers/api-gateway
  uid: ac75ab97-5109-47ac-b4dc-5701f009d350
spec:
  maxReplicas: 4
  minReplicas: 1
  scaleTargetRef:
    apiVersion: extensions/v1beta1
    kind: Deployment
    name: api-gateway
  targetCPUUtilizationPercentage: 400
status:
  currentCPUUtilizationPercentage: 6
  currentReplicas: 1
  desiredReplicas: 1
```

autoscale-rules.yaml is from above file

```
localhost:doc14 zhao$ kubectl delete hpa api-gateway
horizontalpodautoscaler.autoscaling "api-gateway" deleted
localhost:doc14 zhao$ kubectl get hpa
No resources found.
localhost:doc14 zhao$ kubectl apply -f autoscale-rules.yaml
horizontalpodautoscaler.autoscaling/api-gateway created
localhost:doc14 zhao$ kubectl get hpa
NAME          REFERENCE                TARGETS          MINPODS   MAXPODS   REPLICAS   AGE
api-gateway   Deployment/api-gateway   <unknown>/400%   1         4         0          9s
```
```
localhost:doc14 zhao$ kubectl top pod
NAME                                 CPU(cores)   MEMORY(bytes)
api-gateway-57579fc57b-52vn8         3m           163Mi
mongodb-5dc79669d-r5g2c              6m           224Mi
position-simulator-96f46d659-dxzzp   10m          433Mi
position-tracker-f6f5dd79d-b8q77     6m           514Mi
queue-5798db7fdb-b89tc               16m          228Mi
webapp-7bf85bf85f-lf8x8              0m           4Mi
```

refresh the link to make api-gateway's cpu up
http://192.168.99.106:30080/api/panic

```
localhost:doc14 zhao$ kubectl top pod
NAME                                 CPU(cores)   MEMORY(bytes)
api-gateway-57579fc57b-52vn8         355m         164Mi
mongodb-5dc79669d-r5g2c              6m           225Mi
position-simulator-96f46d659-dxzzp   9m           424Mi
position-tracker-f6f5dd79d-b8q77     3m           514Mi
queue-5798db7fdb-b89tc               14m          228Mi
webapp-7bf85bf85f-lf8x8              0m           4Mi
localhost:doc14 zhao$ kubectl describe hpa api-gateway
Name:                                                  api-gateway
Namespace:                                             default
Labels:                                                <none>
Annotations:                                           kubectl.kubernetes.io/last-applied-configuration:
                                                         {"apiVersion":"autoscaling/v1","kind":"HorizontalPodAutoscaler","metadata":{"annotations":{},"name":"api-gateway","namespace":"default"},"...
CreationTimestamp:                                     Mon, 22 Jul 2019 18:00:02 -0400
Reference:                                             Deployment/api-gateway
Metrics:                                               ( current / target )
  resource cpu on pods  (as a percentage of request):  710% (355m) / 400%
Min replicas:                                          1
Max replicas:                                          4
Deployment pods:                                       1 current / 2 desired
Conditions:
  Type            Status  Reason              Message
  ----            ------  ------              -------
  AbleToScale     True    SucceededRescale    the HPA controller was able to update the target scale to 2
  ScalingActive   True    ValidMetricFound    the HPA was able to successfully calculate a replica count from cpu resource utilization (percentage of request)
  ScalingLimited  False   DesiredWithinRange  the desired count is within the acceptable range
Events:
  Type    Reason             Age   From                       Message
  ----    ------             ----  ----                       -------
  Normal  SuccessfulRescale  12s   horizontal-pod-autoscaler  New size: 2; reason: cpu resource utilization (percentage of request) above target
```

```
localhost:doc14 zhao$ kubectl top pod
NAME                                 CPU(cores)   MEMORY(bytes)
api-gateway-57579fc57b-52vn8         355m         164Mi
mongodb-5dc79669d-r5g2c              6m           225Mi
position-simulator-96f46d659-dxzzp   9m           424Mi
position-tracker-f6f5dd79d-b8q77     3m           514Mi
queue-5798db7fdb-b89tc               14m          228Mi
webapp-7bf85bf85f-lf8x8              0m           4Mi
localhost:doc14 zhao$ kubectl top pod
NAME                                 CPU(cores)   MEMORY(bytes)
api-gateway-57579fc57b-52vn8         5m           166Mi
mongodb-5dc79669d-r5g2c              9m           225Mi
position-simulator-96f46d659-dxzzp   10m          424Mi
position-tracker-f6f5dd79d-b8q77     5m           514Mi
queue-5798db7fdb-b89tc               17m          213Mi
webapp-7bf85bf85f-lf8x8              0m           4Mi
```
```
localhost:doc14 zhao$ kubectl describe hpa api-gateway
Name:                                                  api-gateway
Namespace:                                             default
Labels:                                                <none>
Annotations:                                           kubectl.kubernetes.io/last-applied-configuration:
                                                         {"apiVersion":"autoscaling/v1","kind":"HorizontalPodAutoscaler","metadata":{"annotations":{},"name":"api-gateway","namespace":"default"},"...
CreationTimestamp:                                     Mon, 22 Jul 2019 18:00:02 -0400
Reference:                                             Deployment/api-gateway
Metrics:                                               ( current / target )
  resource cpu on pods  (as a percentage of request):  10% (5m) / 400%
Min replicas:                                          1
Max replicas:                                          4
Deployment pods:                                       2 current / 2 desired
Conditions:
  Type            Status  Reason               Message
  ----            ------  ------               -------
  AbleToScale     True    ScaleDownStabilized  recent recommendations were higher than current one, applying the highest recent recommendation
  ScalingActive   True    ValidMetricFound     the HPA was able to successfully calculate a replica count from cpu resource utilization (percentage of request)
  ScalingLimited  False   DesiredWithinRange   the desired count is within the acceptable range
Events:
  Type    Reason             Age   From                       Message
  ----    ------             ----  ----                       -------
  Normal  SuccessfulRescale  103s  horizontal-pod-autoscaler  New size: 2; reason: cpu resource utilization (percentage of request) above target
```

two api-gateway
```
localhost:doc14 zhao$ kubectl get pods
NAME                                 READY   STATUS    RESTARTS   AGE
api-gateway-57579fc57b-4hh6s         1/1     Running   0          3m38s
api-gateway-57579fc57b-52vn8         1/1     Running   0          33m
mongodb-5dc79669d-r5g2c              1/1     Running   1          7d
position-simulator-96f46d659-dxzzp   1/1     Running   1          7d
position-tracker-f6f5dd79d-b8q77     1/1     Running   1          7d
queue-5798db7fdb-b89tc               1/1     Running   1          7d
webapp-7bf85bf85f-lf8x8              1/1     Running   4          7d
localhost:doc14 zhao$ kubectl get all
NAME                                     READY   STATUS    RESTARTS   AGE
pod/api-gateway-57579fc57b-4hh6s         1/1     Running   0          2m3s
pod/api-gateway-57579fc57b-52vn8         1/1     Running   0          32m
pod/mongodb-5dc79669d-r5g2c              1/1     Running   1          7d
pod/position-simulator-96f46d659-dxzzp   1/1     Running   1          7d
pod/position-tracker-f6f5dd79d-b8q77     1/1     Running   1          7d
pod/queue-5798db7fdb-b89tc               1/1     Running   1          7d
pod/webapp-7bf85bf85f-lf8x8              1/1     Running   4          7d


NAME                                TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                          AGE
service/fleetman-api-gateway        NodePort    10.100.44.246   <none>        8080:30020/TCP                   7d
service/fleetman-mongodb            ClusterIP   10.105.61.4     <none>        27017/TCP                        7d
service/fleetman-position-tracker   ClusterIP   10.106.80.156   <none>        8080/TCP                         7d
service/fleetman-queue              NodePort    10.97.14.19     <none>        8161:30010/TCP,61616:31975/TCP   7d
service/fleetman-webapp             NodePort    10.96.236.247   <none>        80:30080/TCP                     7d
service/kubernetes                  ClusterIP   10.96.0.1       <none>        443/TCP                          13d


NAME                                 READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/api-gateway          2/2     2            2           7d
deployment.apps/mongodb              1/1     1            1           7d
deployment.apps/position-simulator   1/1     1            1           7d
deployment.apps/position-tracker     1/1     1            1           7d
deployment.apps/queue                1/1     1            1           7d
deployment.apps/webapp               1/1     1            1           7d

NAME                                           DESIRED   CURRENT   READY   AGE
replicaset.apps/api-gateway-57579fc57b         2         2         2       32m
replicaset.apps/api-gateway-77dff9778b         0         0         0       7d
replicaset.apps/api-gateway-9d5546845          0         0         0       45m
replicaset.apps/mongodb-5dc79669d              1         1         1       7d
replicaset.apps/position-simulator-96f46d659   1         1         1       7d
replicaset.apps/position-tracker-f6f5dd79d     1         1         1       7d
replicaset.apps/queue-5798db7fdb               1         1         1       7d
replicaset.apps/webapp-7bf85bf85f              1         1         1       7d


NAME                                              REFERENCE                TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
horizontalpodautoscaler.autoscaling/api-gateway   Deployment/api-gateway   9%/400%   1         4         2          8m6s
```
