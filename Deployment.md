# Kubernetes Deployments :
- when you create pod you want to manage replicas, scalability, rolling rollout, version control. 
- deployment manage replica behind its using replicasets 
- most of application design in deployments. A Deployment manages a set of Pods to run an application workload, usually one that doesn't maintain state.

# kubernetes Daemosetes: 
- ensure that pod is running on every node. 
- if you add node daemosetes pods auto added in node or if your remove pod its auto clean up garbaage pods.
- logging services, monitor service stack, networks services or storage services controllers.

# kubernetes Statefulsets ::: 
- if you need state management in your application in that case we need sts. 

# kubenetes replicasets:::