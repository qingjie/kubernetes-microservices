```
kubectl get po --watch

```
```
localhost:doc18 zhao$ kubectl apply -f rules-for-new-joiners.yaml
role.rbac.authorization.k8s.io/new-joiner created
localhost:doc18 zhao$ kubectl get roles
NAME         AGE
new-joiner   6s
localhost:doc18 zhao$ kubectl get role new-joiner
NAME         AGE
new-joiner   34s
localhost:doc18 zhao$ kubectl describe role new-joiner
Name:         new-joiner
Labels:       <none>
Annotations:  kubectl.kubernetes.io/last-applied-configuration:
                {"apiVersion":"rbac.authorization.k8s.io/v1","kind":"Role","metadata":{"annotations":{},"name":"new-joiner","namespace":"default"},"rules"...
PolicyRule:
  Resources  Non-Resource URLs  Resource Names  Verbs
  ---------  -----------------  --------------  -----
  *          []                 []              [get watch list]
  *.apps     []                 []              [get watch list]

```
![](img/1.png)
![](img/2.png)

```
localhost:doc18 zhao$ kubectl apply -f rules-for-new-joiners.yaml
role.rbac.authorization.k8s.io/new-joiner configured
rolebinding.rbac.authorization.k8s.io/put-specific-user-or-users-into-new-joiner-role created
localhost:doc18 zhao$ kubectl get rolebinding put-specific-user-or-users-into-new-joiner-role
NAME                                              AGE
put-specific-user-or-users-into-new-joiner-role   95s
localhost:doc18 zhao$ kubectl describe rolebinding put-specific-user-or-users-into-new-joiner-role
Name:         put-specific-user-or-users-into-new-joiner-role
Labels:       <none>
Annotations:  kubectl.kubernetes.io/last-applied-configuration:
                {"apiVersion":"rbac.authorization.k8s.io/v1","kind":"RoleBinding","metadata":{"annotations":{},"name":"put-specific-user-or-users-into-new...
Role:
  Kind:  Role
  Name:  new-joiner
Subjects:
  Kind  Name                      Namespace
  ----  ----                      ---------
  User  francis-linux-login-name
```
---
do the following things on AWS
```
kubectl get nodes
whoami
kubectl get all
sudo useradd francis-linux-login-name
ls /home
sudo passwd francis-linux-login-name
kubectl create ns playground
su - francis-linux-login-name
whoami
kubectl get all
exit current and login super user
kubectl config view
and exit super user to login francis-linux-login-name
kubectl config set-cluster fleetman.k8s.local --server=(url is from previous step)

```
![](img/3.png)
![](img/4.png)
![](img/5.png)
![](img/6.png)
```
kubectl config view
kubectl config set-context mycontext --user francis-linux-login-name --cluster fleetman.k8s.local
kubectl config view
```
![](img/7.png)
```
kubectl config use-context mycontext
kubectl get all
```
![](img/8.png)

```
openssl genrsa -out private-key-francis.key 2048
openssl req -new -key private-key-francis.key -out req.csr -subj "/CN=francis-linux-login-name/O=francis-linux-login-name"
vi req.csr
history | grep STATE
aws s3 ls
aws s3 ls s3://chesterwood-stat

```
![](img/9.png)
![](img/10.png)
![](img/11.png)
![](img/12.png)
![](img/13.png)
![](img/14.png)
![](img/15.png)
![](img/16.png)
![](img/17.png)
---
allocating Access to Users
![](img/18.png)
![](img/19.png)
![](img/20.png)
![](img/21.png)
![](img/22.png)
![](img/23.png)
![](img/24.png)
![](img/25.png)
![](img/26.png)
![](img/27.png)
---
ClusterRoles and ClusterRoleBindings
![](img/28.png)
![](img/29.png)
![](img/30.png)
![](img/31.png)
![](img/32.png)
![](img/33.png)
![](img/34.png)
![](img/35.png)
![](img/36.png)
![](img/37.png)
![](img/38.png)
![](img/39.png)
![](img/40.png)
![](img/41.png)
- kind: Service
![](img/42.png)

---
![](img/rbac-0.png)
![](img/rbac-1.png)
![](img/rbac-2.png)
![](img/rbac-3.png)
![](img/rbac-4.png)
![](img/rbac-5.png)
![](img/rbac-6.png)
