# Kubernetes Namespace: 
Namespaces are intended for use in environments with many users spread across multiple teams, or projects. For clusters with a few to tens of users, you should not need to create or think about namespaces at all.
Benifits: 
- enviorment based isolation 
- controll user and resource access 
- resource control and management 

# default namespace: 
Kubernetes includes this namespace so that you can start using your new cluster without first creating a namespace. production cluster pov we not create any resource in default. 

# kube-node-lease: 
This namespace holds Lease objects associated with each node. Node leases allow the kubelet to send heartbeats so that the control plane can detect node failure.

# kube-system: 
The namespace for objects created by the Kubernetes system

# kube-public:
This namespace is readable by all clients 