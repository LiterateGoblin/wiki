---
title: Kubernetes
---
Kubernetes is open-source container orchestration software.

## Concepts

- **cluster** - a cluster is a set of worker nodes. Each cluster must have one or more nodes. Each cluster is also assigned to a control plane. Multiple clusters may share a control plane.
- **worker node** - a physical or virtual machine that hosts pods.
- **pod** - a pod is a set of colocated containers on one worker node. Containers within a pod can easily communicate. Pods are killed if the control plane finds that they are unhealthy, and a new pod is created to take its place.
- **service** - a service refers to a logical collection of pods and a means to access them.
- **namespace** - a virtual cluster within a physical cluster. Two or more resources within the same physical cluster can have the same name as long as they reside in different namespaces.
- **ReplicaSet** - a mechanism that ensures that a specific number of pods of the same type are always running.
- **deployment** - manages some set of ReplicaSets and lone pods in a cluster. An operator can configure a deployment to make changes to the cluster, and the deployment will enact the change in a controlled manner.

### Volumes

A pod has access to two kinds of storage: *ephemeral* and *persistent*. Ephemeral storage only lasts as long as a pod exists, and can be used to facilitate inter-container communication within a pod. Persistent storage has a lifecycle independent of any individual pod.

### Scheduling

The *pod scheduler* will place pods on nodes that meet all the criteria of that pod's specification.

### Planes

Each node can be placed on one of two planes: the *control plane* or the *data plane*. Nodes in the control plane are responsible for managing nodes in the data plane. Nodes in the data plane actually run the application software within the pods.

#### Control plane

Each control plane node includes a controller manager, a cloud controller, a scheduler, and an API server. The controller manager is responsible for threads called controllers that listen for and respond to cluster events. The cloud controller is one particular type of controller that interacts with the underlying cloud provider. The scheduler is a sub-system that selects which node a container will run on when a request to create a container is received. The API server is the primary interface for a Kubernetes operator to interact with the control plane. All communication from the cluster to the control plane is made to the API server. More API servers will be deployed if the load of any particular server becomes too great.

The control plane also contains etcd, a key-value store designed for high availability. Critical cluster data and state are stored in etcd.

#### Data plane

Each data plane node includes kube-proxy, a container runtime, kubelet, and 0 or more pods. Kube-proxy is a networking utility that ensures that pods are abiding by the host's networking rules. Docker is the most common container runtime on a data plane node, though Kubernetes supports several others. Kubelet is the most important daemon running on the worker nodes - it ensures that the designated containers running in a pod are healthy. kubelet also is responsible for communicating to the control plane on the behalf of the node.

### Custom resources

Custom resources can be defined in Kubernetes in addition to resources such as pods, deployments, and ReplicaSets. These custom resources are created with a Custom Resource Definition (CRD). A custom resource could be a grouping of native Kubernetes objects or a completely custom object. *Operators*, the name given to the custom controllers running on worker nodes, manage custom objects. Operators are preferred over manually updating Kubernetes objects.

## kubectl

kubectl is a command line interface that communicates with the API server within the control plane. It can be used to give commands to create an object, configure automatic scaling, and view details about the cluster.

## Scaling

Kubernetes provides ways to horizontally or vertically scale out or in when demands for a service increases or decreases.

### Cluster Autoscaler (CA)

When a pod fails to launch this may either be because there are not enough resources on the node to allocate to the pod, or because the scheduler has determined that the pod could conserve resources by running on a different node. The CA automatically adjusts the number of nodes in a cluster when one of these situations occur, provisioning more nodes in the former situation and deprovisioning nodes in the latter.

The cluster autoscaler runs as a deployment-type workload within the cluster itself. It relies on a metrics server also running as a deployment workload to provide it metrics about the current state of the CPU, or whatever metric is observed for autoscaling.

### Horizontal Pod Autoscaler (HPA)

This component monitors the metrics of each pod in a Kubernetes deployment. If the metric exceeds some threshold, more pods will be provisioned for that service until the threshold is no longer met or the maximum number of pods for that autoscaling group is met. The metric used by default is CPU utilization.

### Vertical Pod Autoscaler (VPA)

This component adjusts the CPU reservation of each pod to more closely match its actual historical usage - especially when another pod is waiting to be scheduled due to a lack of resources. When a pod is determined to have allocated more resources than required, the VPA changes the pod configuration directly.

## Networking

Each container in a pod can communicate with the other containers in that pod over localhost. Each pod on a node can communicate with each other using a virtual Ethernet device (veth).

## References

<https://explore.skillbuilder.aws/learn/course/57/play/46911/amazon-eks-primer>. Accessed 2023-12-20
