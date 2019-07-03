```
localhost:dev zhao$ cd doc2/
localhost:doc2 zhao$ ls
first-pod.yaml		learn-k8s.md		webapp-service.yaml
localhost:doc2 zhao$ mv learn-k8s.md readme.md
localhost:doc2 zhao$ ls
first-pod.yaml		readme.md		webapp-service.yaml
localhost:doc2 zhao$ atom first-pod.yaml
localhost:doc2 zhao$ kubectl apply -f webapp-service.yaml
Error from server: error when applying patch:
{"metadata":{"annotations":{"kubectl.kubernetes.io/last-applied-configuration":"{\"apiVersion\":\"v1\",\"kind\":\"Service\",\"metadata\":{\"annotations\":{},\"name\":\"fleetman-webapp\",\"namespace\":\"default\"},\"spec\":{\"ports\":[{\"name\":\"http\",\"nodePort\":30080,\"port\":80}],\"selector\":{\"app\":\"webapp\",\"release\":0},\"type\":\"NodePort\"}}\n"}},"spec":{"selector":{"release":0}}}
to:
Resource: "/v1, Resource=services", GroupVersionKind: "/v1, Kind=Service"
Name: "fleetman-webapp", Namespace: "default"
Object: &{map["apiVersion":"v1" "kind":"Service" "metadata":map["annotations":map["kubectl.kubernetes.io/last-applied-configuration":"{\"apiVersion\":\"v1\",\"kind\":\"Service\",\"metadata\":{\"annotations\":{},\"name\":\"fleetman-webapp\",\"namespace\":\"default\"},\"spec\":{\"ports\":[{\"name\":\"http\",\"nodePort\":30080,\"port\":80}],\"selector\":{\"app\":\"webapp\"},\"type\":\"NodePort\"}}\n"] "creationTimestamp":"2019-07-02T21:44:40Z" "name":"fleetman-webapp" "namespace":"default" "resourceVersion":"119107" "selfLink":"/api/v1/namespaces/default/services/fleetman-webapp" "uid":"9866092e-9d12-11e9-a14e-080027c8c9f9"] "spec":map["clusterIP":"10.104.2.249" "externalTrafficPolicy":"Cluster" "ports":[map["name":"http" "nodePort":'\u7580' "port":'P' "protocol":"TCP" "targetPort":'P']] "selector":map["app":"webapp"] "sessionAffinity":"None" "type":"NodePort"] "status":map["loadBalancer":map[]]]}
for: "webapp-service.yaml": cannot convert int64 to string
localhost:doc2 zhao$ pwd
/Users/zhao/dev/doc2
localhost:doc2 zhao$ kubectl apply -f webapp-service.yaml
service/fleetman-webapp configured
localhost:doc2 zhao$ kubectl apply -f first-pod.yaml
pod/webapp configured
pod/webapp-release-0-5 created
localhost:doc2 zhao$ kubectl get all
NAME                     READY   STATUS    RESTARTS   AGE
apiVersion: v1
pod/webapp               1/1     Running   2          1d
pod/webapp-release-0-5   1/1     Running   0          18s


NAME                      TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
service/fleetman-webapp   NodePort    10.104.2.249   <none>        80:30080/TCP   1d
service/kubernetes        ClusterIP   10.96.0.1      <none>        443/TCP        5d







localhost:doc2 zhao$ kubectl describe svc fleetman-webapp
Name:                     fleetman-webapp
Namespace:                default
Labels:                   <none>
Annotations:              kubectl.kubernetes.io/last-applied-configuration:
                            {"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"name":"fleetman-webapp","namespace":"default"},"spec":{"ports":[{"name":...
Selector:                 app=webapp,release=0
Type:                     NodePort
IP:                       10.104.2.249
Port:                     http  80/TCP
TargetPort:               80/TCP
NodePort:                 http  30080/TCP
Endpoints:                172.17.0.4:80
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
localhost:doc2 zhao$ vi webapp-service.yaml
localhost:doc2 zhao$ kubectl apply -f webapp-service.yaml
service/fleetman-webapp configured
localhost:doc2 zhao$ kubectl describe svc fleetman-webapp
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
localhost:doc2 zhao$ kubectl get pods
NAME                 READY   STATUS    RESTARTS   AGE
webapp               1/1     Running   2          1d
webapp-release-0-5   1/1     Running   0          5m
localhost:doc2 zhao$ kubectl get po
NAME                 READY   STATUS    RESTARTS   AGE
webapp               1/1     Running   2          1d
webapp-release-0-5   1/1     Running   0          5m
localhost:doc2 zhao$ kubectl get po --show-labels
NAME                 READY   STATUS    RESTARTS   AGE   LABELS
webapp               1/1     Running   2          1d    app=webapp,release=0
webapp-release-0-5   1/1     Running   0          5m    app=webapp,release=0-5
localhost:doc2 zhao$ kubectl get po --show-labels -l release=0
NAME     READY   STATUS    RESTARTS   AGE   LABELS
webapp   1/1     Running   2          1d    app=webapp,release=0
localhost:doc2 zhao$ kubectl get po --show-labels -l release=0-5
NAME                 READY   STATUS    RESTARTS   AGE   LABELS
webapp-release-0-5   1/1     Running   0          6m    app=webapp,release=0-5
localhost:doc2 zhao$ kubectl get po --show-labels -l release=1

```
