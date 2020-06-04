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

[vagrant@m1-centos cka]$ sudo kubeadm init --apiserver-advertise-address=192.168.20.10 --pod-network-cidr=10.244.0.0/16  
[vagrant@m1-centos cka]$ sudo adduser student  
[vagrant@m1-centos cka]$ sudo passwd student  
New password: student  
[vagrant@m1-centos cka]$ sudo usermod -aG wheel student  
[vagrant@m1-centos cka]$ su - student  
[student@m1-centos ~]$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config  
[student@m1-centos ~]$ sudo chown $(id -u):$(id -g) $HOME/.kube/config  
[student@m1-centos ~]$ cd .kube  
[student@m1-centos .kube]$ ls -l  
[student@m1-centos .kube]$ cat config  
[student@m1-centos .kube]$ cd  
[student@m1-centos ~]$ kubectl cluster-info  
[student@m1-centos ~]$ kubectl get nodes  



## setup on work node
$ vagrant.exe ssh c1-centos  
[vagrant@c1-centos ~]$ sudo yum install -y vim git bash-completion  
[vagrant@c1-centos ~]$ git clone https://github.com/petercharlespcg/cka.git  
[vagrant@c1-centos ~]$ cd cka  
[vagrant@c1-centos cka]$ sudo ./setup-docker.sh  
[vagrant@c1-centos cka]$ cat /etc/fstab  
[vagrant@c1-centos cka]$ sudo ./setup-kubetools.sh  
