# security group setup for master and worker nodes
#master node: 
6443/tpc for kubernetes API server
2379-2380 for etcd server client API
6783/tcp, 6784/UDP for weavent CNI
10248-10260 for kubelet API, Kube-scheduler, kube-controller-namager etc
80, 8080, 446 generic ports
30000-32767 for nodeport services

#on slave node
6783/tcp, 6784/UDP for wavent CNI
10248-10260 for kubelt API
30000-32767 for node port service


# Installing helm cli
wget https://get.helm.sh/helm-v3.12.2-linux-amd64.tar.gz
tar zxf helm-v3.12.2-linux-amd64.tar.gz
cd linux-amd64/
sudo mv helm /usr/bin/
helm version

# add helm repository
helm repo add nginx-stable https://helm.nginx.com/stable
# update helm repository
helm repo update

# Install Nginx Ingress Controller
helm upgrade --install ingress-nginx ingress-nginx --repo https://kubernetes.github.io/ingress-nginx --namespace ingress-nginx --create-namespace

# Check is ingress is created
kubectl --namespace ingress-nginx get services -o wide ingress-nginx-controller
