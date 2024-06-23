22 June 2024
============

Setting up Minikube in WSL in Office Laptop
-------------------------------------------

ref: Basic commands for WSL
	https://learn.microsoft.com/en-us/windows/wsl/basic-commands

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
-------------------------------------------------------
-------------------------------------------------------
PS C:\Users\pthapliy> wsl --export Ubuntu-22.04-minikube C:\Prasun\wsl2-images\minikube-base.tar
Export in progress, this may take a few minutes.
The operation completed successfully.

[Optionally]
wsl --import minikube-base C:\Prasun\wslDistroStorage\minikube-base\ C:\Prasun\wsl2-images\minikube-base.tar
-------------------------------------------------------
PS C:\Users\pthapliy> dir C:\Prasun\wslDistroStorage\; dir C:\Prasun\wsl2-images\


    Directory: C:\Prasun\wslDistroStorage


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----         1/25/2024  10:16 AM                basecopy01
d-----         6/16/2024   2:34 PM                dev01
d-----         6/21/2024   8:26 PM                minikube
d-----         2/15/2024   9:02 AM                teamcity


    Directory: C:\Prasun\wsl2-images


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----         6/23/2024   8:25 AM     5208719360 minikube-base.tar
-a----         1/25/2024  10:26 AM           1302 ReadMe.txt
-a----         1/25/2024   9:42 AM     1064407040 ubuntu-22.04-default.tar
-a----         1/31/2024   3:46 PM     3232819200 ubuntu-22.04-dotnetdevcontainer.tar
-a----          2/1/2024   8:04 PM           1760 zscalerRootCA.crt


PS C:\Users\pthapliy>
-------------------------------------------------------
PS C:\Users\pthapliy> wsl -l -v
  NAME                       STATE           VERSION
* Ubuntu-22.04               Stopped         2
  teamcity                   Stopped         2
  Ubuntu-22.04-minikube      Stopped         2
  Ubuntu-22.04-basecopy01    Stopped         2
  Ubuntu-22.04-dev01         Stopped         2
PS C:\Users\pthapliy>
-------------------------------------------------------
-------------------------------------------------------
ref: Using Multi-Node Clusters
	https://minikube.sigs.k8s.io/docs/tutorials/multi_node/#hello-deployment.yaml

wsl --import minikube-multi-node C:\Prasun\wslDistroStorage\minikube-multi-node\ C:\Prasun\wsl2-images\minikube-base.tar
wsl -d minikube-multi-node


minikube start --nodes 2 -p multinode-demo

prasun@DESKTOP-V99LATL:~$ minikube start --nodes 2 -p multinode-demo
😄  [multinode-demo] minikube v1.33.1 on Ubuntu 22.04 (amd64)
✨  Automatically selected the docker driver
📌  Using Docker driver with root privileges
👍  Starting "multinode-demo" primary control-plane node in "multinode-demo" cluster
🚜  Pulling base image v0.0.44 ...
🔥  Creating docker container (CPUs=2, Memory=2200MB) ...
🐳  Preparing Kubernetes v1.30.0 on Docker 26.1.1 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔗  Configuring CNI (Container Networking Interface) ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: storage-provisioner, default-storageclass

👍  Starting "multinode-demo-m02" worker node in "multinode-demo" cluster
🚜  Pulling base image v0.0.44 ...
🔥  Creating docker container (CPUs=2, Memory=2200MB) ...
🌐  Found network options:
    ▪ NO_PROXY=192.168.58.2
🐳  Preparing Kubernetes v1.30.0 on Docker 26.1.1 ...
    ▪ env NO_PROXY=192.168.58.2
🔎  Verifying Kubernetes components...
💡  kubectl not found. If you need it, try: 'minikube kubectl -- get pods -A'
🏄  Done! kubectl is now configured to use "multinode-demo" cluster and "default" namespace by default
prasun@DESKTOP-V99LATL:~$
-------------------------------------------------------
minikube status -p multinode-demo
-------------------------------------------------------
This doesnt work
	minikube kubectl -- get pods -A
	You must specify the cluster name (or whatever that -p argument is :|)

prasun@DESKTOP-V99LATL:~$ minikube -p multinode-demo kubectl -- get pods -A
NAMESPACE     NAME                                     READY   STATUS    RESTARTS      AGE
kube-system   coredns-7db6d8ff4d-jf4qj                 1/1     Running   4 (49m ago)   50m
kube-system   etcd-multinode-demo                      1/1     Running   0             51m
kube-system   kindnet-2r82s                            1/1     Running   0             50m
kube-system   kindnet-jh886                            1/1     Running   0             50m
kube-system   kube-apiserver-multinode-demo            1/1     Running   0             51m
kube-system   kube-controller-manager-multinode-demo   1/1     Running   0             51m
kube-system   kube-proxy-4z24q                         1/1     Running   0             50m
kube-system   kube-proxy-k7jp9                         1/1     Running   0             50m
kube-system   kube-scheduler-multinode-demo            1/1     Running   0             51m
kube-system   storage-provisioner                      1/1     Running   1 (50m ago)   51m
prasun@DESKTOP-V99LATL:~$
-------------------------------------------------------
-------------------------------------------------------
-------------------------------------------------------
prasun@DESKTOP-V99LATL:~$ minikube delete
🔥  Deleting "minikube" in docker ...
🔥  Deleting container "minikube" ...
🔥  Removing /home/prasun/.minikube/machines/minikube ...
💀  Removed all traces of the "minikube" cluster.
prasun@DESKTOP-V99LATL:~$ minikube delete  -p multinode-demo
🔥  Deleting "multinode-demo" in docker ...
🔥  Deleting container "multinode-demo" ...
🔥  Deleting container "multinode-demo-m02" ...
🔥  Removing /home/prasun/.minikube/machines/multinode-demo ...
🔥  Removing /home/prasun/.minikube/machines/multinode-demo-m02 ...
💀  Removed all traces of the "multinode-demo" cluster.
prasun@DESKTOP-V99LATL:~$
-------------------------------------------------------
-------------------------------------------------------
This time I'll create the cluster without giving -p argument. Hopefully then rest of the commands should also not require -p
And lets say, node count = 3
So 2x3 = 6 GB RAM would be used in running this cluster (or maybe max 6 GB)

prasun@DESKTOP-V99LATL:~$ minikube start --nodes 3
😄  minikube v1.33.1 on Ubuntu 22.04 (amd64)
✨  Automatically selected the docker driver
📌  Using Docker driver with root privileges
👍  Starting "minikube" primary control-plane node in "minikube" cluster
🚜  Pulling base image v0.0.44 ...
🔥  Creating docker container (CPUs=2, Memory=2200MB) ...
❗  This container is having trouble accessing https://registry.k8s.io
💡  To pull new external images, you may need to configure a proxy: https://minikube.sigs.k8s.io/docs/reference/networking/proxy/
🐳  Preparing Kubernetes v1.30.0 on Docker 26.1.1 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔗  Configuring CNI (Container Networking Interface) ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: storage-provisioner, default-storageclass

👍  Starting "minikube-m02" worker node in "minikube" cluster
🚜  Pulling base image v0.0.44 ...
🔥  Creating docker container (CPUs=2, Memory=2200MB) ...
🌐  Found network options:
    ▪ NO_PROXY=192.168.49.2
❗  This container is having trouble accessing https://registry.k8s.io
💡  To pull new external images, you may need to configure a proxy: https://minikube.sigs.k8s.io/docs/reference/networking/proxy/
🐳  Preparing Kubernetes v1.30.0 on Docker 26.1.1 ...
    ▪ env NO_PROXY=192.168.49.2
🔎  Verifying Kubernetes components...

👍  Starting "minikube-m03" worker node in "minikube" cluster
🚜  Pulling base image v0.0.44 ...
🔥  Creating docker container (CPUs=2, Memory=2200MB) ...
🌐  Found network options:
    ▪ NO_PROXY=192.168.49.2,192.168.49.3
❗  This container is having trouble accessing https://registry.k8s.io
💡  To pull new external images, you may need to configure a proxy: https://minikube.sigs.k8s.io/docs/reference/networking/proxy/
🐳  Preparing Kubernetes v1.30.0 on Docker 26.1.1 ...
    ▪ env NO_PROXY=192.168.49.2
    ▪ env NO_PROXY=192.168.49.2,192.168.49.3
🔎  Verifying Kubernetes components...
💡  kubectl not found. If you need it, try: 'minikube kubectl -- get pods -A'
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
prasun@DESKTOP-V99LATL:~$
-------------------------------------------------------
minikube kubectl -- get pods -A

prasun@DESKTOP-V99LATL:~$ minikube kubectl -- get pods -A
NAMESPACE     NAME                               READY   STATUS    RESTARTS        AGE
kube-system   coredns-7db6d8ff4d-dbtzr           1/1     Running   2 (3m50s ago)   4m21s
kube-system   etcd-minikube                      1/1     Running   0               4m49s
kube-system   kindnet-45s75                      1/1     Running   0               3m20s
kube-system   kindnet-7mqb5                      1/1     Running   0               4m21s
kube-system   kindnet-bkng8                      1/1     Running   0               4m10s
kube-system   kube-apiserver-minikube            1/1     Running   0               4m49s
kube-system   kube-controller-manager-minikube   1/1     Running   0               4m49s
kube-system   kube-proxy-5bcwj                   1/1     Running   0               3m20s
kube-system   kube-proxy-ghfhf                   1/1     Running   0               4m21s
kube-system   kube-proxy-pxwnf                   1/1     Running   0               4m10s
kube-system   kube-scheduler-minikube            1/1     Running   0               4m51s
kube-system   storage-provisioner                1/1     Running   1 (3m50s ago)   4m48s
prasun@DESKTOP-V99LATL:~$
-------------------------------------------------------
prasun@DESKTOP-V99LATL:~$ minikube kubectl get nodes
NAME           STATUS   ROLES           AGE     VERSION
minikube       Ready    control-plane   6m4s    v1.30.0
minikube-m02   Ready    <none>          5m22s   v1.30.0
minikube-m03   Ready    <none>          4m32s   v1.30.0
prasun@DESKTOP-V99LATL:~$
-------------------------------------------------------
prasun@DESKTOP-V99LATL:~$ minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

minikube-m02
type: Worker
host: Running
kubelet: Running

minikube-m03
type: Worker
host: Running
kubelet: Running

prasun@DESKTOP-V99LATL:~$
-------------------------------------------------------
PS C:\Users\pthapliy> wsl --export minikube-multi-node C:\Prasun\wsl2-images\minikube-multi-node.tar
Export in progress, this may take a few minutes.
The operation completed successfully.
PS C:\Users\pthapliy> dir C:\Prasun\wsl2-images\


    Directory: C:\Prasun\wsl2-images


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----         6/23/2024   8:25 AM     5208719360 minikube-base.tar
-a----         6/24/2024  12:09 AM     7044894720 minikube-multi-node.tar
-a----         1/25/2024  10:26 AM           1302 ReadMe.txt
-a----         1/25/2024   9:42 AM     1064407040 ubuntu-22.04-default.tar
-a----         1/31/2024   3:46 PM     3232819200 ubuntu-22.04-dotnetdevcontainer.tar
-a----          2/1/2024   8:04 PM           1760 zscalerRootCA.crt


PS C:\Users\pthapliy>
-------------------------------------------------------
-------------------------------------------------------
-------------------------------------------------------
-------------------------------------------------------
-------------------------------------------------------
-------------------------------------------------------
-------------------------------------------------------
-------------------------------------------------------
-------------------------------------------------------
-------------------------------------------------------
-------------------------------------------------------
-------------------------------------------------------



