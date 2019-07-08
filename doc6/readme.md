```
localhost:doc6 zhao$ kubectl get all
NAME                          READY   STATUS             RESTARTS   AGE
pod/queue                     1/1     Running            0          1h
pod/webapp-66fbdb9599-b4jq5   0/1     InvalidImageName   0          14m
pod/webapp-jvb8j              1/1     Running            0          22m
pod/webapp-mjrlb              1/1     Running            0          21m


NAME                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/fleetman-queue    NodePort    10.101.245.41   <none>        8161:30010/TCP   2h
service/fleetman-webapp   NodePort    10.104.2.249    <none>        80:30080/TCP     5d
service/kubernetes        ClusterIP   10.96.0.1       <none>        443/TCP          9d


NAME                     DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/webapp   2         3         1            2           41m

NAME                                DESIRED   CURRENT   READY   AGE
replicaset.apps/webapp              2         2         2       1h
replicaset.apps/webapp-66fbdb9599   1         1         0       14m
replicaset.apps/webapp-746ff4c965   0         0         0       41m




localhost:doc6 zhao$ kubectl get ns
NAME          STATUS   AGE
default       Active   9d
kube-public   Active   9d
kube-system   Active   9d
localhost:doc6 zhao$ kubectl get namespace
NAME          STATUS   AGE
default       Active   9d
kube-public   Active   9d
kube-system   Active   9d
localhost:doc6 zhao$ kubectl get pods
NAME                      READY   STATUS             RESTARTS   AGE
queue                     1/1     Running            0          1h
webapp-66fbdb9599-b4jq5   0/1     InvalidImageName   0          21m
webapp-jvb8j              1/1     Running            0          29m
webapp-mjrlb              1/1     Running            0          28m
localhost:doc6 zhao$ kubectl get po
NAME                      READY   STATUS             RESTARTS   AGE
queue                     1/1     Running            0          1h
webapp-66fbdb9599-b4jq5   0/1     InvalidImageName   0          21m
webapp-jvb8j              1/1     Running            0          29m
webapp-mjrlb              1/1     Running            0          29m
localhost:doc6 zhao$ kubectl get pods -n kube-system
NAME                                    READY   STATUS    RESTARTS   AGE
etcd-minikube                           1/1     Running   0          5h
kube-addon-manager-minikube             1/1     Running   4          9d
kube-apiserver-minikube                 1/1     Running   0          5h
kube-controller-manager-minikube        1/1     Running   0          5h
kube-dns-86f4d74b45-8cfr6               3/3     Running   16         9d
kube-proxy-hd4cr                        1/1     Running   0          5h
kube-scheduler-minikube                 1/1     Running   0          5h
kubernetes-dashboard-5498ccf677-9xhn7   1/1     Running   12         9d
storage-provisioner                     1/1     Running   12         9d
localhost:doc6 zhao$ kubectl get all -n kube-system
NAME                                        READY   STATUS    RESTARTS   AGE
pod/etcd-minikube                           1/1     Running   0          5h
pod/kube-addon-manager-minikube             1/1     Running   4          9d
pod/kube-apiserver-minikube                 1/1     Running   0          5h
pod/kube-controller-manager-minikube        1/1     Running   0          5h
pod/kube-dns-86f4d74b45-8cfr6               3/3     Running   16         9d
pod/kube-proxy-hd4cr                        1/1     Running   0          5h
pod/kube-scheduler-minikube                 1/1     Running   0          5h
pod/kubernetes-dashboard-5498ccf677-9xhn7   1/1     Running   12         9d
pod/storage-provisioner                     1/1     Running   12         9d


NAME                           TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)         AGE
service/kube-dns               ClusterIP   10.96.0.10       <none>        53/UDP,53/TCP   9d
service/kubernetes-dashboard   NodePort    10.102.116.201   <none>        80:30000/TCP    9d

NAME                        DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
daemonset.apps/kube-proxy   1         1         1       1            1           <none>          9d

NAME                                   DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/kube-dns               1         1         1            1           9d
deployment.apps/kubernetes-dashboard   1         1         1            1           9d

NAME                                              DESIRED   CURRENT   READY   AGE
replicaset.apps/kube-dns-86f4d74b45               1         1         1       9d
replicaset.apps/kubernetes-dashboard-5498ccf677   1         1         1       9d




localhost:doc6 zhao$ kubectl get ns
NAME          STATUS   AGE
default       Active   9d
kube-public   Active   9d
kube-system   Active   9d
localhost:doc6 zhao$ kubectl get all -n kube-public









No resources found.
localhost:doc6 zhao$ kubectl get all -n kube-system
NAME                                        READY   STATUS    RESTARTS   AGE
pod/etcd-minikube                           1/1     Running   0          5h
pod/kube-addon-manager-minikube             1/1     Running   4          9d
pod/kube-apiserver-minikube                 1/1     Running   0          5h
pod/kube-controller-manager-minikube        1/1     Running   0          5h
pod/kube-dns-86f4d74b45-8cfr6               3/3     Running   16         9d
pod/kube-proxy-hd4cr                        1/1     Running   0          5h
pod/kube-scheduler-minikube                 1/1     Running   0          5h
pod/kubernetes-dashboard-5498ccf677-9xhn7   1/1     Running   12         9d
pod/storage-provisioner                     1/1     Running   12         9d


NAME                           TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)         AGE
service/kube-dns               ClusterIP   10.96.0.10       <none>        53/UDP,53/TCP   9d
service/kubernetes-dashboard   NodePort    10.102.116.201   <none>        80:30000/TCP    9d

NAME                        DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
daemonset.apps/kube-proxy   1         1         1       1            1           <none>          9d

NAME                                   DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/kube-dns               1         1         1            1           9d
deployment.apps/kubernetes-dashboard   1         1         1            1           9d

NAME                                              DESIRED   CURRENT   READY   AGE
replicaset.apps/kube-dns-86f4d74b45               1         1         1       9d
replicaset.apps/kubernetes-dashboard-5498ccf677   1         1         1       9d




localhost:doc6 zhao$ kubectl describe svc kube-dns -n kube-system
Name:              kube-dns
Namespace:         kube-system
Labels:            k8s-app=kube-dns
                   kubernetes.io/cluster-service=true
                   kubernetes.io/name=KubeDNS
Annotations:       <none>
Selector:          k8s-app=kube-dns
Type:              ClusterIP
IP:                10.96.0.10
Port:              dns  53/UDP
TargetPort:        53/UDP
Endpoints:         172.17.0.4:53
Port:              dns-tcp  53/TCP
TargetPort:        53/TCP
Endpoints:         172.17.0.4:53
Session Affinity:  None
Events:            <none>
localhost:doc6 zhao$ kubectl apply -f networking-tests.yaml
error: error parsing networking-tests.yaml: error converting YAML to JSON: yaml: line 9: did not find expected '-' indicator
localhost:doc6 zhao$ kubectl apply -f networking-tests.yaml
pod/mysql created
service/database created
localhost:doc6 zhao$ kubectl get all
NAME                          READY   STATUS             RESTARTS   AGE
pod/mysql                     1/1     Running            0          24s
pod/queue                     1/1     Running            0          2h
pod/webapp-66fbdb9599-b4jq5   0/1     InvalidImageName   0          1h
pod/webapp-jvb8j              1/1     Running            0          1h
pod/webapp-mjrlb              1/1     Running            0          1h


NAME                      TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
service/database          ClusterIP   10.111.225.103   <none>        3306/TCP         24s
service/fleetman-queue    NodePort    10.101.245.41    <none>        8161:30010/TCP   3h
service/fleetman-webapp   NodePort    10.104.2.249     <none>        80:30080/TCP     5d
service/kubernetes        ClusterIP   10.96.0.1        <none>        443/TCP          9d


NAME                     DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/webapp   2         3         1            2           1h

NAME                                DESIRED   CURRENT   READY   AGE
replicaset.apps/webapp              2         2         2       2h
replicaset.apps/webapp-66fbdb9599   1         1         0       1h
replicaset.apps/webapp-746ff4c965   0         0         0       1h




localhost:doc6 zhao$ kubectl exec -it webapp-jvb8j
error: you must specify at least one command for the container
localhost:doc6 zhao$ kubectl exec -it webapp-jvb8j bash
OCI runtime exec failed: exec failed: container_linux.go:348: starting container process caused "exec: \"bash\": executable file not found in $PATH": unknown
command terminated with exit code 126
localhost:doc6 zhao$ kubectl exec -it webapp-jvb8j sh
/ # ls
bin    etc    lib    mnt    root   sbin   sys    usr
dev    home   media  proc   run    srv    tmp    var
/ # cat /etc/resolv.conf
nameserver 10.96.0.10
search default.svc.cluster.local svc.cluster.local cluster.local
options ndots:5
/ # nslookup google.com
nslookup: can't resolve '(null)': Name does not resolve

Name:      google.com
Address 1: 172.217.10.78 lga34s14-in-f14.1e100.net
Address 2: 2607:f8b0:4006:802::200e lga34s12-in-x0e.1e100.net
/ # nslookup database
nslookup: can't resolve '(null)': Name does not resolve

Name:      database
Address 1: 10.111.225.103 database.default.svc.cluster.local
/ # exit
localhost:doc6 zhao$ kubectl get all
NAME                          READY   STATUS             RESTARTS   AGE
pod/mysql                     1/1     Running            0          9m
pod/queue                     1/1     Running            0          2h
pod/webapp-66fbdb9599-b4jq5   0/1     InvalidImageName   0          1h
pod/webapp-jvb8j              1/1     Running            0          1h
pod/webapp-mjrlb              1/1     Running            0          1h


NAME                      TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
service/database          ClusterIP   10.111.225.103   <none>        3306/TCP         9m
service/fleetman-queue    NodePort    10.101.245.41    <none>        8161:30010/TCP   3h
service/fleetman-webapp   NodePort    10.104.2.249     <none>        80:30080/TCP     5d
service/kubernetes        ClusterIP   10.96.0.1        <none>        443/TCP          9d


NAME                     DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/webapp   2         3         1            2           1h

NAME                                DESIRED   CURRENT   READY   AGE
replicaset.apps/webapp              2         2         2       2h
replicaset.apps/webapp-66fbdb9599   1         1         0       1h
replicaset.apps/webapp-746ff4c965   0         0         0       1h




localhost:doc6 zhao$ kubectl exec -it webapp-mjrlb sh
/ # ls
bin    etc    lib    mnt    root   sbin   sys    usr
dev    home   media  proc   run    srv    tmp    var
/ # mysql
sh: mysql: not found
/ # apk update
fetch http://dl-cdn.alpinelinux.org/alpine/v3.7/main/x86_64/APKINDEX.tar.gz
fetch http://dl-cdn.alpinelinux.org/alpine/v3.7/community/x86_64/APKINDEX.tar.gz
v3.7.3-87-gf9f4e0e8b1 [http://dl-cdn.alpinelinux.org/alpine/v3.7/main]
v3.7.3-78-g634dbf6dd0 [http://dl-cdn.alpinelinux.org/alpine/v3.7/community]
OK: 9068 distinct packages available
/ # apk add mysql-client
(1/6) Installing mariadb-common (10.1.40-r0)
(2/6) Installing ncurses-terminfo-base (6.0_p20171125-r1)
(3/6) Installing ncurses-terminfo (6.0_p20171125-r1)
(4/6) Installing ncurses-libs (6.0_p20171125-r1)
(5/6) Installing mariadb-client (10.1.40-r0)
(6/6) Installing mysql-client (10.1.40-r0)
Executing busybox-1.27.2-r7.trigger
OK: 53 MiB in 34 packages
/ # mysql
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/run/mysqld/mysqld.sock' (2 "No such file or directory")
/ # mysql -h database -u root -ppassword fleetman
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.7.26 MySQL Community Server (GPL)

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MySQL [fleetman]> create table test(test varchar(255));
Query OK, 0 rows affected (0.01 sec)

MySQL [fleetman]> show tables;
+--------------------+
| Tables_in_fleetman |
+--------------------+
| test               |
+--------------------+
1 row in set (0.01 sec)

MySQL [fleetman]> exit
Bye
/ # nslookup database
nslookup: can't resolve '(null)': Name does not resolve

Name:      database
Address 1: 10.111.225.103 database.default.svc.cluster.local
/ # cat /etc/resolv.conf
nameserver 10.96.0.10
search default.svc.cluster.local svc.cluster.local cluster.local
options ndots:5
/ # exit
```
