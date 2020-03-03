fix helm priviledges.txt
```


kubectl create serviceaccount --namespace kube-system tiller

kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller

kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}' 


```
![](install-mysql-with-helm-1.png)
![](install-mysql-with-helm-2.png)

---
# prometheus-operator
edit ClusterIP to LoadBalancer

![](edit-prometheus-operator-to-broswer.png)
![](15 mins-cpu.png)
