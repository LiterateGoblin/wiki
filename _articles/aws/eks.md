---
title: Amazon EKS
---
Amazon EKS is a managed service that acts as the control plane for the container orchestration software [Kubernetes](/kubernetes.html). It is also responsible for portions of the data plane.

## Control plane

The EKS control plane consists of at least two API server nodes (responsible for issuing commands to worker nodes) and three etcd (persistence layer) nodes across three AWS Availability Zones. Unhealthy nodes are automatically replaced.

## Data plane

Worker nodes in a EKS cluster can be fully unmanaged, within a "managed node group", or an AWS Fargate pod. A managed node group automates the provisioning, management, and scaling of the nodes; unhealthy nodes are terminated and replaced with a healthy node. The group can be updated as one unit. Fargate completely manages the node infrastructure and abstracts it away from a Kubernetes operator. When using Fargate, an operator specifies which pods should be scheduled in Fargate with a JSON document called a "Fargate profile". A cluster can include pods that are running on Fargate and pods that are managed or un-managed.

EKS allows the creation of worker nodes across multiple AWS Availability Zones.

## Integration with other AWS services

EKS natively integrates with the following services:

- AWS Elastic Load Balancing (ELB)
- [AWS Identity and Access Management (IAM)](/aws/iam.html) for authentication and authorization
- AWS VPC for networking

## EKS Management Tools

Clusters, nodes, and pods in EKS can be managed using the following tools:

- the AWS graphical console for EKS
- AWS Command Line Interface (CLI)
  - Alternatively, the AWS EKS API can be used directly by making requests to AWS over HyperText Transfer Protocol (HTTP). There are software development kits (SDKs) available.
- eksctl

## Security

Depending on the level of management of each node or pod that a user has (self-managed, managed, Fargate), the level of security that the user is responsible for changes. For self-managed nodes, the user is responsible for securing the most components, including the security of the pods, the Amazon Machine Image (AMI) runtime, the network, the IAM execution role of any given pod, the role-based access control configuration, and the actual code within a container image. With managed nodes, the responsibility of securing the Amazon Machine Image is moved to AWS as long as the nodes have been configured to use the default AMI. AWS is responsible for securing the most components when using Fargate. Fargate pods completely abstract the underlying node; an EKS user is not responsible for securing the AMI.

Authentication and authorization for commands made to the EKS API are handled using AWS IAM the same way the same way they are for any other AWS API. Authentication for commands made to the underlying Kubernetes API server are handled using IAM as well, but authorization is handled using the native Kubernetes role-based access control system.

The cluster and each node assumes an IAM role to determine which AWS API calls they are allowed to make.

## Networking

EKS integrates with AWS VPC's Container Network Interface (CNI) such that each pod on a cluster has the same IP address in the VPC as it does in the cluster. This is accomplished through the use of the Amazon VPC CNI plugin for Kubernetes.

Additionally, EKS integrates with ELB using the AWS Load Balancer controller. A Kubernetes ingress object can integrate with an AWS ELB Application Load Balancer, and a Kubernetes LoadBalancer service can integrate with an AWS ELB Network Load Balancer.

## References

1. "Amazon EKS Primer." *AWS Skill Builder*, **<https://explore.skillbuilder.aws/learn/course/57/play/46911/amazon-eks-primer>**. Accessed 22 Dec 2023.
