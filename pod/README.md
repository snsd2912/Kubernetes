# Pod

With kubernetes our ultimate aim is to deploy our application in the form of containers on a set of machines that are configured as 
worker nodes in a cluster. However, kubernetes does not deploy containers directly on the worker nodes. The containers are encapsulated into a Kubernetes object known as PODs. A POD is a single instance of an application. A POD is the smallest object, that you can create in kubernetes.

### Example-1

* What if the number of users accessing your application increase and you need to scale your application?
You need to add additional instances of your web application to share the load. 
* where would you spin up additional instances? Do we bring up a new container instance within the same POD? 
No! We create a new POD altogether with a new instance of the same application. 
* What if the user base FURTHER increases and your current node has no sufficient capacity? 
You can always deploy additional PODs on a new node in the cluster. You will have a new node added to the cluster to expand the cluster’s physical capacity. 

PODs usually have a one-to-one relationship with containers running your application. To scale UP you create new PODs and to scale down you delete PODs. You do not add additional containers to an existing POD to scale your application.

## Multi-containers pod

A single pod CAN have multiple containers, except for the fact that they are usually not multiple containers of the same kind.

### Example-2

Sometimes you might have a scenario were you have a helper container, that might be doing some kind of supporting task for our web application such as processing a user entered data, processing a file uploaded by the user. You want these helper containers to live along side your application container. \
In that case, you CAN have both of these containers part of the same POD, so that when a new application container is created, the helper is also created and when it dies the helper also dies since they are part of the same POD. The two containers can also communicate with each other directly by referring to each other as ‘localhost’ since they share the same network namespace. Plus they can easily share the same storage space as well. 

## Definition file

Create a *pod.yaml* file with the following content:
```
apiVersion: v1
kind: Pod
metadata:
  name:
  labels:
spec:
  containers:
    - name: 
      image: 
```

To create pod, run command:
```
kubectl create -f pod.yml
```

Other helpful commands:
```
# get list pods
kubectl get pod 
# get detail information of a specific pod
kubectl describe pod [pod-name]
```