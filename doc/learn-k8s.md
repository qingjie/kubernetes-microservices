```
localhost:k8s-test zhao$ minikube status
minikube: Running
cluster: Running
kubectl: Correctly Configured: pointing to minikube-vm at 192.168.99.101
```
```
localhost:k8s-test zhao$ minikube docker-env
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://192.168.99.101:2376"
export DOCKER_CERT_PATH="/Users/zhao/.minikube/certs"
export DOCKER_API_VERSION="1.23"
# Run this command to configure your shell:
# eval $(minikube docker-env)
```
```
localhost:k8s-test zhao$ eval $(minikube docker-env)
```
```
localhost:k8s-test zhao$ docker image pull richardchesterwood/k8s-fleetman-webapp-angular:release0-5
```
```
localhost:k8s-test zhao$ docker container run -p 8080:80 -d richardchesterwood/k8s-fleetman-webapp-angular:release0-5
localhost:k8s-test zhao$ docker container ls
localhost:k8s-test zhao$ minikube ip
192.168.99.101
```
http://192.168.99.101:8080

```
localhost:k8s-test zhao$ docker container stop 0726
localhost:k8s-test zhao$ docker container rm 0726
```
