[Markdown Live Preview](https://markdownlivepreview.com/)

# Vagrant lab for CKA online course



## setup on control node
$ vagrant ssh m1-centos  
[vagrant@m1-centos ~]$ sudo yum install -y vim git bash-completion
[vagrant@m1-centos ~]$ git clone https://github.com/petercharlespcg/cka.git  
[vagrant@m1-centos ~]$ cd cka  
[vagrant@m1-centos cka]$ sudo ./setup-docker.sh  
[vagrant@m1-centos cka]$ cat /etc/fstab  
[vagrant@m1-centos cka]$ sudo ./setup-kubetools.sh

[vagrant@m1-centos cka]$ kubectl get nodes  
The connection to the server localhost:8080 was refused - did you specify the right host or port?
Solution: To start using your cluster, you need to run the following as a regular user:   
[vagrant@m1-centos cka]$   mkdir -p $HOME/.kube  
[vagrant@m1-centos cka]$   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config  
[vagrant@m1-centos cka]$   sudo chown $(id -u):$(id -g) $HOME/.kube/config

[vagrant@m1-centos cka]$ kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"  
[vagrant@m1-centos cka]$ kubectl get pods --all-namespaces  
kube-system   weave-net-tn7pr                     2/2     Running   0          91s

[vagrant@m1-centos cka]$ kubectl get nodes  
NAME        STATUS   ROLES    AGE   VERSION  
m1-centos   Ready    master   9h    v1.18.3

[vagrant@c1-centos cka]$ cat kube-join.sh
kubeadm join 192.168.20.10:6443 --token qaz523.5rfzhjnbm0q5jca2 \  
    --discovery-token-ca-cert-hash sha256:df24a4377ea43b18bfcab79559c94afc472bd3eb89e007e60a5cef83d4b55981  
[vagrant@c1-centos cka]$ sudo ./kube-join.sh

[vagrant@m1-centos cka]$ kubectl get nodes  
NAME        STATUS   ROLES    AGE     VERSION  
c1-centos   Ready    <none>   2m18s   v1.18.3  
m1-centos   Ready    master   9h      v1.18.3  

[vagrant@m1-centos cka]$ kubectl config -h  
[vagrant@m1-centos cka]$ kubectl config view  


## setup on work node
$ vagrant.exe ssh c1-centos  
[vagrant@c1-centos ~]$ sudo yum install -y vim git bash-completion  
[vagrant@c1-centos ~]$ git clone https://github.com/petercharlespcg/cka.git  
[vagrant@c1-centos ~]$ cd cka  
[vagrant@c1-centos cka]$ sudo ./setup-docker.sh  
[vagrant@c1-centos cka]$ cat /etc/fstab  
[vagrant@c1-centos cka]$ sudo ./setup-kubetools.sh  
