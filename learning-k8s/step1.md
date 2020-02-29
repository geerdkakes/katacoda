## 1 Getting information on the cluster

Kubernetes has an API listening for instructions. For example, to deploy resources or get information on existing resources. Kubectl is a command line tool to give these instructions. This program uses the kubernetes API for this. Normally you have to first configure the program to connect to the correct URL and use the correct credentials. In this case everything is set up to start immediately.


We start by collecting information on the cluster. You can do this with the command: `kubectl cluster-info`{{execute}} (click to execute)


```
$ kubectl cluster-info
Kubernetes master is running at https://172.17.0.68:6443
KubeDNS is running at https://172.17.0.68:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

To find out at what version the cluster is running use: `kubectl version`{{execute}} (click to execute)

```
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"14", GitVersion:"v1.14.0", GitCommit:"641856db18352033a0d96dbc99153fa3b27298e5", GitTreeState:"clean", BuildDate:"2019-03-25T15:53:57Z", GoVersion:"go1.12.1", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"14", GitVersion:"v1.14.0", GitCommit:"641856db18352033a0d96dbc99153fa3b27298e5", GitTreeState:"clean", BuildDate:"2019-03-25T15:45:25Z", GoVersion:"go1.12.1", Compiler:"gc", Platform:"linux/amd64"}
```

To see the nodes the cluster contains use:

```
$ kubectl get nodes
NAME     STATUS   ROLES    AGE   VERSION
master   Ready    master   83m   v1.14.0
node01   Ready    <none>   83m   v1.14.0
```

In above example one master and one node is available. 