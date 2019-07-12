```
history | grep export
aws ec2 describe-availability-zones --region us-east-1
kops create cluster --zones us-east-1a,us-east-1b,us-east-1c,us-east-1d ${NAME}
ssh-keygen -b 2048 -t rsa -f ~/.ssh/id_rsa
kops create secret --name ${NAME} sshpublickey admin -i ~/.ssh/id_rsa.sshpublickey
kops edit cluster ${NAME}
kubectl get svc

```
