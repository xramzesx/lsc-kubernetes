# Large Scale Computing - lab 6 - Kubernetes

To run this app, you need to configure your cloud provider. For the lab purposes, we decided to use AWS. Firstly, create security-group:
![image](https://github.com/user-attachments/assets/ffb13950-f437-4b4e-9174-95ca92da3461)

Then create Kubernetes cluster on AWS EKS:
![image](https://github.com/user-attachments/assets/a3a6d30b-fa25-49f9-b898-4cdbec8023ab)
Configure networking
![image](https://github.com/user-attachments/assets/893fc347-5c89-4564-8a6a-04c13b12dad4)

Then create a node group:
![image](https://github.com/user-attachments/assets/0b4a85c3-a9bc-4d91-9d1a-a3a144063a2c)

Configure your aws cli credentials, then run:
```bash
aws eks --region us-east-1 update-kubeconfig --name lsc-hw-cluster
```

Run `kubectl get nodes` to check if everything works

Then clone this repository and run:

```bash
helm repo add stable https://charts.helm.sh/stable
helm repo add nfs-ganesha-server-and-external-provisioner https://kubernetes-sigs.github.io/nfs-ganesha-server-and-external-provisioner/
helm install nfs-server-provisioner nfs-ganesha-server-and-external-provisioner/nfs-server-provisioner -f ./nfs-values.yaml

kubectl apply -f ./config/pvc.yml
kubectl apply -f ./config/deployment.yml
kubectl apply -f ./config/service.yml
kubectl apply -f ./config/job.yml
```
