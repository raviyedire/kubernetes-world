Step1: On Master Node Only
## Install Docker

sudo wget https://raw.githubusercontent.com/puneetgavri/kubernetes-world/main/installation/scripts/installDocker.sh -P /tmp
sudo chmod 755 /tmp/installDocker.sh
sudo bash /tmp/installDocker.sh

## Install kubeadm,kubelet,kubectl

sudo wget https://raw.githubusercontent.com/puneetgavri/kubernetes-world/main/installation/scripts/installK8S-v1-23.sh -P /tmp
sudo chmod 755 /tmp/installK8S-v1-23.sh
sudo bash /tmp/installK8S-v1-23.sh

## Initialize kubernetes Master Node
 
   sudo kubeadm init --ignore-preflight-errors=all

   sudo mkdir -p $HOME/.kube
   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   sudo chown $(id -u):$(id -g) $HOME/.kube/config

   ## install networking driver -- Weave/flannel/canal/calico etc... 

   ## below installs weave networking driver 
    
   sudo kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.24.1/manifests/calico.yaml

   # Validate:  kubectl get nodes
   -------------------------------------------------------------------------------
Step2: On All Worker Nodes
## Install Docker

sudo wget https://raw.githubusercontent.com/puneetgavri/kubernetes-world/main/installation/scripts/installDocker.sh -P /tmp
sudo chmod 755 /tmp/installDocker.sh
sudo bash /tmp/installDocker.sh

## Install kubeadm,kubelet,kubectl

sudo wget https://raw.githubusercontent.com/puneetgavri/kubernetes-world/main/installation/scripts/installK8S-v1-23.sh -P /tmp
sudo chmod 755 /tmp/installK8S-v1-23.sh
sudo bash /tmp/installK8S-v1-23.sh

## Run Below on Master Node to get join token 

kubeadm token create --print-join-command 

    copy the kubeadm join token from master & run it on all nodes

    Ex: kubeadm join 10.128.15.231:6443 --token mks3y2.v03tyyru0gy12mbt \
           --discovery-token-ca-cert-hash sha256:3de23d42c7002be0893339fbe558ee75e14399e11f22e3f0b34351077b7c4b56