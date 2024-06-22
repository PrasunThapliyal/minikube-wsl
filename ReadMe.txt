22 June 2024
============

Setting up Minikube in WSL in Office Laptop
-------------------------------------------

wsl --import Ubuntu-22.04-minikube C:\Prasun\wslDistroStorage\minikube\ C:\Prasun\wsl2-images\ubuntu-22.04-default.tar
wsl.conf
resolv.conf
zScaler
apt-get install docker.io docker-compose
root@DESKTOP-V99LATL:~# docker -v
Docker version 24.0.7, build 24.0.7-0ubuntu2~22.04.1
apt-get update
exit
wsl --shutdown Ubuntu-22.04-minikube
wsl -d Ubuntu-22.04-minikube
sudo su -
usermod -aG docker prasun
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
mv minikube-linux-amd64 /usr/local/bin/minikube
chmod 755 /usr/local/bin/minikube
exit to go to user prasun, or su - prasun
minikube start --driver=docker
If this fails, try "minikube delete", then try again
minikube status
prasun@DESKTOP-V99LATL:~$ minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
prasun@DESKTOP-V99LATL:~$ minikube kubectl get nodes
    > kubectl.sha256:  64 B / 64 B [-------------------------] 100.00% ? p/s 0s
    > kubectl:  49.07 MiB / 49.07 MiB [-------------] 100.00% 6.37 MiB p/s 7.9s
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   94s   v1.30.0
prasun@DESKTOP-V99LATL:~$
prasun@DESKTOP-V99LATL:~$ minikube kubectl -- get pods -A
NAMESPACE     NAME                               READY   STATUS    RESTARTS   AGE
kube-system   coredns-7db6d8ff4d-7b846           1/1     Running   0          108s
kube-system   etcd-minikube                      1/1     Running   0          2m2s
kube-system   kube-apiserver-minikube            1/1     Running   0          2m3s
kube-system   kube-controller-manager-minikube   1/1     Running   0          2m2s
kube-system   kube-proxy-k8hx9                   1/1     Running   0          109s
kube-system   kube-scheduler-minikube            1/1     Running   0          2m2s
kube-system   storage-provisioner                1/1     Running   0          2m
prasun@DESKTOP-V99LATL:~$
prasun@DESKTOP-V99LATL:~$ minikube kubectl get service
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   3m25s


