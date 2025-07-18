# kubectl get node    // information about nodes and details
# kubectl describe node node_name  // details of nodes 

# Namespace Commands 
*  kubectl get pod --all-namespaces / -A  // show all pods 
*  kubectl get ns 
*  kubectl create namespace namespace_name
*  kubectl delete namespace namespace_name 

# pod commands 
* kubectl create podname --image=imagename --port=containerport  \\ create pod 
* kubectl exec -it podname -- command    \\ access pod 
* kubectl expose podname   \\ expose pod in clusterip 
* kubectl run pod1 --image=nginx --port=80 --dry-run=client -o yaml // print yaml version
* kubectl run pod1 --image=nginx --port=80 --dry-run=client -o json // print json format

# decleartive management 
* kubectl delete  -f testpod.yaml    // Delete deployment using yaml 
* kubectl apply  -f testpod.yaml     // apply deployment 

# Service commands
* kubectl get svc -A     \\ check your svc 