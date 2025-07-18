# Intrdocution of Pods: 
pod is a smallest unit of compute in kubernnetes. 
pod is a single or group of containers. 
pod is provide storage context and related thing to container in kubernetes. 

--- 
apiVersion: apps/v1     //  ----- api version supported by kubernetes component apps/v1 storage 
kind: Pod               // kind is your resource pod Deamonsets deployment 
metadata:               // metadata collect information of name namespace and labels 
  name: myapp
  labels:
    app.kubernetes.io/name: myapp
spec:                        // specification containers storage affinity nodeselectore 
  containers:                // containers informations 
  - name: myapp
    image: <Image>
    resources:          // limitation of resources  --- request--- minimum allcoation and  
      limits:             /// maximum resource allocation 
        memory: "128Mi"
        cpu: "500m"
    ports:
      - containerPort: <Port>