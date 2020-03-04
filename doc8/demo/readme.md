PersistentVolumeClaim & PersistentVolume

pls do not forget set RECLAIM POLICY, you can choose one that you need, like  Delete, Retain

# How to set PVC on with AWS

https://kubernetes.io/docs/concepts/storage/storage-classes/

https://kubernetes.io/docs/concepts/storage/storage-classes/#aws-ebs

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html

How to use PV/PVC for mongoDB storage, the following demo, I am using aws-ebs for mongo-db storage.
```
qzhaos-mbp: qzhao$ cat mongo-stack.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongodb
spec:
  selector:
    matchLabels:
      app: mongodb
  replicas: 1
  template: # template for the pods
    metadata:
      labels:
        app: mongodb
    spec:
      containers:
      - name: mongodb
        image: mongo:3.6.5-jessie
        volumeMounts:
          - name: mongo-persistent-storage
            mountPath: /data/db
      volumes:
        - name: mongo-persistent-storage
          # pointer to the configuration of HOW we want the mount to be implemented
          persistentVolumeClaim:
            claimName: mongo-pvc
---
kind: Service
apiVersion: v1
metadata:
  name: mongodb
spec:
  selector:
    app: mongodb
  ports:
    - name: mongoport
      port: 27017
  type: ClusterIP
```
```
qzhaos-mbp: qzhao$ cat storage-aws.yaml
# What do want?
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mongo-pvc
spec:
  storageClassName: cloud-ssd
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 7Gi
---
# How do we want it implemented
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: cloud-ssd
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
```
```
qzhaos-mbp: qzhao$ kubectl get all
NAME                           READY   STATUS    RESTARTS   AGE
pod/mongodb-57f6bf75cc-jmvq5   1/1     Running   0          2m4s

NAME                   TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)     AGE
service/kubernetes     ClusterIP   10.100.0.1       <none>        443/TCP     69m
service/zhao-mongodb   ClusterIP   10.100.125.118   <none>        27017/TCP   2m4s

NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/mongodb   1/1     1            1           2m4s

NAME                                 DESIRED   CURRENT   READY   AGE
replicaset.apps/mongodb-57f6bf75cc   1         1         1       2m4s


qzhaos-mbp: qzhao$ kubectl describe pod/mongodb-57f6bf75cc-jmvq5
Name:           mongodb-57f6bf75cc-jmvq5
Namespace:      default
Priority:       0
Node:           ip-192-168-22-76.ec2.internal/192.168.22.76
Start Time:     Wed, 04 Mar 2020 17:04:23 -0500
Labels:         app=mongodb
                pod-template-hash=57f6bf75cc
Annotations:    kubernetes.io/psp: eks.privileged
Status:         Running
IP:             192.168.2.236
IPs:            <none>
Controlled By:  ReplicaSet/mongodb-57f6bf75cc
Containers:
  mongodb:
    Container ID:   docker://bae8cd425f7938b15b3f7d1f7bfc489f76bacf9c131c2960237146f4c72d7c7f
    Image:          mongo:3.6.5-jessie
    Image ID:       docker-pullable://mongo@sha256:3e00936a4fbd17003cfd33ca808f03ada736134774bfbc3069d3757905a4a326
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Wed, 04 Mar 2020 17:05:03 -0500
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /data/db from mongo-persistent-storage (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-7jj6c (ro)
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
  default-token-7jj6c:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-7jj6c
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                  Age                    From                                    Message
  ----     ------                  ----                   ----                                    -------
  Warning  FailedScheduling        2m41s (x2 over 2m41s)  default-scheduler                       persistentvolumeclaim "mongo-pvc" not found
  Warning  FailedScheduling        2m25s (x4 over 2m39s)  default-scheduler                       pod has unbound immediate PersistentVolumeClaims
  Normal   Scheduled               2m24s                  default-scheduler                       Successfully assigned default/mongodb-57f6bf75cc-jmvq5 to ip-192-168-22-76.ec2.internal
  Normal   SuccessfulAttachVolume  2m22s                  attachdetach-controller                 AttachVolume.Attach succeeded for volume "pvc-1164a9fa-5e64-11ea-853d-160a68a82d21"
  Normal   Pulled                  104s                   kubelet, ip-192-168-22-76.ec2.internal  Container image "mongo:3.6.5-jessie" already present on machine
  Normal   Created                 104s                   kubelet, ip-192-168-22-76.ec2.internal  Created container mongodb
  Normal   Started                 104s                   kubelet, ip-192-168-22-76.ec2.internal  Started container mongodb
qzhaos-mbp: qzhao$
```
you will find volumn pvc-1164a9fa-5e64-11ea-853d-160a68a82d21` like the following:
```
qzhaos-mbp: qzhao$ kubectl get pvc
NAME        STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
mongo-pvc   Bound    pvc-1164a9fa-5e64-11ea-853d-160a68a82d21   7Gi        RWO            cloud-ssd      7m17s
```
```
qzhaos-mbp: qzhao$ kubectl get pv
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM               STORAGECLASS   REASON   AGE
pvc-1164a9fa-5e64-11ea-853d-160a68a82d21   7Gi        RWO            Delete           Bound    default/mongo-pvc   cloud-ssd               7m3s
```
If you want to keep storage, pls make sure you have reclaimPolicy: Retain like the following
```
# What do want?
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mongo-pvc
spec:
  storageClassName: cloud-ssd
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 7Gi
---
# How do we want it implemented
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: cloud-ssd
reclaimPolicy: Retain
provisioner: kubernetes.io/aws-ebs
parameters:
  type: io1

```
```
qzhaos-mbp: qzhao$ kubectl get pv
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM               STORAGECLASS   REASON   AGE
pvc-a56d6a46-5e65-11ea-88e4-0e4148703fd5   7Gi        RWO            Retain           Bound    default/mongo-pvc   cloud-ssd               88s
```
