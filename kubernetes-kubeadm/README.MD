root@kube-admin1:~# kubectl get nodes -o wide 
NAME           STATUS   ROLES           AGE   VERSION   INTERNAL-IP   EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION      CONTAINER-RUNTIME 
kube-master1   Ready    control-plane   81m   v1.27.3   10.3.16.221   <none>        Ubuntu 22.04.2 LTS   5.15.0-75-generic   containerd://1.6.12 
kube-master2   Ready    control-plane   64m   v1.27.3   10.3.16.224   <none>        Ubuntu 22.04.2 LTS   5.15.0-75-generic   containerd://1.6.12 
kube-master3   Ready    control-plane   41m   v1.27.3   10.3.16.223   <none>        Ubuntu 22.04.2 LTS   5.15.0-75-generic   containerd://1.6.12 
kube-worker1   Ready    <none>          35m   v1.27.3   10.3.16.225   <none>        Ubuntu 22.04.2 LTS   5.15.0-75-generic   containerd://1.6.12 
kube-worker2   Ready    <none>          33m   v1.27.3   10.3.16.226   <none>        Ubuntu 22.04.2 LTS   5.15.0-75-generic   containerd://1.6.12 
kube-worker3   Ready    <none>          31m   v1.27.3   10.3.16.227   <none>        Ubuntu 22.04.2 LTS   5.15.0-75-generic   containerd://1.6.12
