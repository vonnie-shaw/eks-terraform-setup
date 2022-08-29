# Terraform Installation And Setup In AWS EC2 Linux Instances
#  Using Terraform to provision a fully managed Amazon EKS Cluster

##### Prerequisite
+ AWS Acccount.
+ Create an ubuntu EC2 Instnace.
+ Create IAM Role With Required Policies.
   + VPCFullAccess
   + EC2FullAcces
   + S3FullAccess  ..etc
   + Administrator Access
+ Attach IAM Role to EC2 Instance.

### Install Terraform
```sh
$ sudo adduser eksadmin
$ sudo echo "eksadmin  ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/eksadmin
$ sudo su - eksadmin
```
``` sh
$ git clone https://github.com/devopscalgary/eks-terraform-setup.git
$ cd eks-terraform-setup
# install terraform using a bash shell script
$ sh terraform-install.sh

#### Clone terraform scripts
``` sh
$ git clone https://github.com/devopscalgary/eks-terraform-setup
$ cd eks-terraform-setup
```
#### <span style="color:orange">Update Your Key Name in variables.tf file before executing terraform script.</span>
## Infrastructure As A Code using Terraform
#### Create Infrastructure(Amazon EKS, IAM Roles, AutoScalingGroups, Launch Configuration, LoadBalancer, NodeGroups,VPC,Subnets,Route Tables,Security Groups, NACLs, ..etc) As A Code Using Terraform Scripts
``` sh
# Initialise to install plugins
$ terraform init 
# Validate terraform scripts
$ terraform validate 
# Plan terraform scripts which will list resources which is going  be created.
$ terraform plan 
# Apply to create resources
$ terraform apply --auto-approve
```

```sh
##  Destroy Infrastructure  
$ terraform destroy --auto-approve

## create the kubeconfig file  
$ mkdir .kube/ 
$ vi .kube/config
$ kubectl get pod
$ #!/bin/bash 
$ vi iam-authenticator.sh
# be sure the region is set in your region
$ sh iam-authenticator.sh 
$ kubectl get pod
## deploy cluster auto scaler
$ kubectl apply -f clusterautoscaler.yml

 ```
```
# on your K8s master, join the created worker nodes
kubeadm token create --print-join-command
# copy the command and run on the nodes
kubectl get nodes 
kubectl apply -f deployme.yaml

```

SECOND METHOD


git clone https://github.com/hashicorp/learn-terraform-provision-eks-cluster

$ cd learn-terraform-provision-eks-cluster
$ vi variables.tf #to set region
$ vi providers.tf #to be sure it's same region
$ vi eks-cluster.tf #provision your cluster
$ terraform init
$ terraform plan
$ terraform apply

#Configure kubectl 

$ vi outputs.tf #under value, edit region
$ aws eks --region $(terraform output -raw region) update-kubeconfig \
    --name $(terraform output -raw cluster_name)
$ kubectl cluster-info
$ kubectl get nodes


