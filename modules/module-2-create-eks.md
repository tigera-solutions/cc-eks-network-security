# Module 2 - Create an EKS cluster

For EKS, the Calico OSS can be used as a CNI, or you can make use of the AWS VPC networking as CNI and have Calico only as a plugin for the security policies.

We will use the second approach during this workshop. Please, find below an example on how to create a two nodes cluster with an small footprint, but feel free to create your EKS cluster with the parameters you prefer. Do not forget to include the region if different than the default on your account.

```bash
export CLUSTERNAME=tigera-workshop
export REGION=ca-central-1
export VERSION=1.27
# 
echo "# Start Lab Params" > ~/labVars.env
echo export CLUSTERNAME=$CLUSTERNAME >> ~/labVars.env
echo export REGION=$REGION >> ~/labVars.env
#
eksctl create cluster --name $CLUSTERNAME --version $VERSION  --region $REGION --node-type m5.xlarge
```

- View EKS cluster.

  Once cluster is created you can list it using eksctl.
  
  ```bash
  eksctl get cluster $CLUSTERNAME --region $REGION
  ```

- Test access to EKS cluster with kubectl

  Once the EKS cluster is provisioned with eksctl tool, the kubeconfig file would be placed into ~/.kube/config path. The kubectl CLI looks for kubeconfig at ~/.kube/config path or into KUBECONFIG env var.

  ```bash
  # verify kubeconfig file path
  ls ~/.kube/config
  # test cluster connection
  kubectl get nodes
  ```

  You should get the output with nodes as ```Ready```

  ```bash
  NAME                                              STATUS   ROLES    AGE     VERSION
  ip-192-168-20-189.ca-central-1.compute.internal   Ready    <none>   3m48s   v1.27.9-eks-5e0fdde
  ip-192-168-69-126.ca-central-1.compute.internal   Ready    <none>   3m47s   v1.27.9-eks-5e0fdde
  ```

  Get all pods and ensure they are in ```Running``` state with ```kubectl get pods -A```:

  ```bash
  NAMESPACE     NAME                       READY   STATUS    RESTARTS   AGE
  kube-system   aws-node-6qr7g             2/2     Running   0          5m2s
  kube-system   aws-node-rgr89             2/2     Running   0          5m1s
  kube-system   coredns-797959bcdb-7st4r   1/1     Running   0          10m
  kube-system   coredns-797959bcdb-gzzfj   1/1     Running   0          10m
  kube-system   kube-proxy-6bnmp           1/1     Running   0          5m2s
  kube-system   kube-proxy-qc5b5           1/1     Running   0          5m1s
  ```

[:arrow_right: Module 3 - Connect the EKS cluster to Calico Cloud](module-3-connect-calicocloud.md)  

[:arrow_left: Module 1 - Getting Started](module-1-getting-started.md)  
[:leftwards_arrow_with_hook: Back to Main](../README.md)  
