step 1 : # selinux must be disable or permissive 
https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/
https://kubernetes.io/docs/reference/networking/ports-and-protocols/
setenforce 0 
selinux file for disable/permissive -- /etc/selinux/config

step 2 : Swap Must be disable 
swapoff -a 
check swap using  free -m 

Step 3 : Install Docker in machine 
yum install docker -y 
systemctl start docker 
systemctl enable docker 

step4 : Ip Forwarding Rule 
net.ipv4.ip_forward = 1 in file /etc/sysctl.conf
sysctl --system or system -p 


stpe 5 : containerd configure  ******* kubernetes will not run **********

containerd config default > /etc/containerd/config.toml
[root@ip-172-31-15-199 ec2-user]# vi /etc/containerd/config.toml
do SystemCgroup = true 
systemctl restart containerd 

step 5 : install kuberbnetes repo 

cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.32/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.32/rpm/repodata/repomd.xml.key
#exclude=kubelet kubeadm kubectl cri-tools kubernetes-cni
EOF

yum install kubeadm kubelet kubectl -y 

systemctl enable kubelet

# step 6 : cluster Installation : control-plan 

kubeadm init --pod-network-cidr=10.244.0.0/16

outpout ::::::::::::::::::::::::::: 
 mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 172.31.15.199:6443 --token rdi65n.uzz5rh4kg4imfa5w \
        --discovery-token-ca-cert-hash sha256:26c9c3f6b3288400ef70d7d522d9c68d3019d2ce3b1ee3bfa681a16c3df0222a


step 7: Optional Firewall rules 

systemctl status firewalld 

firewall-cmd --permanent --add-port=6443/tcp
firewall-cmd --permanent --add-port=2379-2380/tcp
firewall-cmd --permanent --add-port=10250/tcp
firewall-cmd --permanent --add-port=10259/tcp
firewall-cmd --permanent --add-port=10257/tcp
firewall-cmd --permanent --add-port=30000-32767/tcp
firewall-cmd --permanent --add-port=30000-32767/udp

firewall-cmd --reload

worker Nodes 

firewall-cmd --permanent --add-port=10250/tcp
firewall-cmd --permanent --add-port=10256/tcp
firewall-cmd --permanent --add-port=30000-32767/tcp
firewall-cmd --permanent --add-port=30000-32767/udp
firewall-cmd --reload

else you can stop firewalld 
systemctl stop firewalld 
systemctl disable  firewalld 


from step1 to step 5 till repo step remain same *********** on every worker node ********************


# get token back any time from master run this below command 
kubeadm token create --print-join-command

# for flannel network use link 
https://github.com/flannel-io/flannel

kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml 

# node and pod check 
kubectl get node 
kubectl get pod -A 


