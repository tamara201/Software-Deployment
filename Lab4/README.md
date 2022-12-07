# Lab4

The task for Lab4 is to 
- set up and configure an AKS in Azure
- configure and deploy Wordpress incl. MySQL in the AKS cluster

## Set up and configure an AKS in Azure

I used this [Microsoft tutorial](https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-cli) to create the AKS cluster. 

First of all, you need to create a resource group using the following command:

    az group create --name Lab4 --location "West Europe"
   
Afterwards create create an AKS. The command below creates a cluster named *myAKSCluster* with one node and enables a system-assigned managed identity.

    az aks create -g Lab4 -n myAKSCluster --enable-managed-identity --node-count 1 --enable-addons monitoring --enable-msi-auth-for-monitoring  --generate-ssh-keys

> **_NOTE:_**  The command takes a few minutes to complete and returns JSON-formatted information about the cluster.

In order to manage a Kubernetes cluster, you need the Kubernetes command-line client `kubectl`. To install `kubectl` use the command `az aks install-cli`. It is also needed to configure `kubectl` to connect to the Kubernetes cluster with the following command:

      az aks get-credentials --resource-group Lab4 --name myAKSCluster

Afterwards you can verify the connection with the command `kubectl get nodes`.

The cluster where the service is deployed looks as follows:

![cluster](https://github.com/tamara201/Software-Deployment/blob/main/Lab4/Screenshots/cluster.png)

## Configure and deploy Wordpress incl. MySQL in the AKS cluster

For this part, I used following tutorials:
- [Example: Deploying WordPress and MySQL with Persistent Volumes](https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/)
- [Tutorial: Run applications in Azure Kubernetes Service (AKS)](https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-application?tabs=azure-cli)

The *kustomization.yaml* file contains a Secret generator for a password secret that is used by Wordpress and MySQL. In addition, it also contains references to both deployment files *mysql-deployment.yaml* and *wordpress-deployment.yaml*. The *mysql-deployment.yaml* and *wordpress-deployment.yaml* files describe a single-instance MySQL/Wordpress deployment as well as a persistent volume and the password secret. 

To deploy the files to the Kubernetes cluster use the following `apply` command:

    kubectl apply -k ./

To verify that all services are running properly use the command `kubectl get services`. To optain the IP of the deployed website you can also run the following command:

    kubectl get service wordpress --watch

Following output is displayed:

```
NAME        TYPE           CLUSTER-IP   EXTERNAL-IP     PORT(S)        AGE
wordpress   LoadBalancer   10.0.7.201   20.123.233.28   80:31863/TCP   2m9s
```

The external IP is the address for the website:

![wordpress](https://github.com/tamara201/Software-Deployment/blob/main/Lab4/Screenshots/wordpress.png)

## Stop, start and delete the AKS

To **stop** the AKS use the following command:

    az aks stop --name myAKSCluster --resource-group Lab4

To **start** the AKS run the following command:

    az aks start --name myAKSCluster --resource-group Lab4

To verify if the cluster stopped or is running use the command below.

    az aks show --resource-group Lab4 --name myAKSCluster

To **delete** the AKS you have to remove the resource group with the following command:

    az group delete --name Lab4 --yes --no-wait
