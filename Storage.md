# Storage Class : 

Dynmaic allocations need driver depends on storage. 

NFS STORAGE DRIVER: 

Installation Setup: 
https://github.com/kubernetes-csi/csi-driver-nfs/blob/master/docs/install-csi-driver-v4.9.0.md

# curl -skSL https://raw.githubusercontent.com/kubernetes-csi/csi-driver-nfs/v4.9.0/deploy/install-driver.sh | bash -s v4.9.0 --


---
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: nfs-csi                                 /// storage name 
provisioner: nfs.csi.k8s.io
parameters:
  server: nfs-server.default.svc.cluster.local  /// nfs-server ip or hostname of storage 
  share: /                                      /// directory share that maintain data
  # csi.storage.k8s.io/provisioner-secret is only needed for providing mountOptions in DeleteVolume
  # csi.storage.k8s.io/provisioner-secret-name: "mount-options"
  # csi.storage.k8s.io/provisioner-secret-namespace: "default"
reclaimPolicy: Delete                           /// reclaim // retain // delete 
volumeBindingMode: Immediate                    /// waitforfirstconsumer
allowVolumeExpansion: true                      /// 
mountOptions:
  - nfsvers=4.1

---  
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: nfs-csi                                 /// storage name 
provisioner: nfs.csi.k8s.io
parameters:
  server: nfs-server.default.svc.cluster.local  /// nfs-server ip or hostname of storage 
  share: /                                      /// directory share that maintain data
reclaimPolicy: Delete                           /// reclaim // retain // delete 
volumeBindingMode: Immediate                    /// waitforfirstconsumer
allowVolumeExpansion: true                      /// 
mountOptions:
  - nfsvers=4.1git 