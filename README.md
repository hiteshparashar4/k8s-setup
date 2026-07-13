# k8s-setup on bare metal from scratch using `kubeadm`. Uses `flannel` as CNI plugin
- I was learning creating k8s cluster on bare metal. All the commands are at single place to create and destory the cluster.
- The commands were tested on Ubuntu 22-24 versions
- You can either use a cloud server or a VM running on your local machine
- I ran these commands on Virtual Box Ubuntu VM
- Ideally control plane and worker nodes are supposed to be two different server/computer systems, i.e. multi node cluster
- This setup allows you to create single node cluster as well, if you want. It means you would have just a single control plane and you would schedule your worker pods on the control plane itself.


## `k8installation.txt` contains commands to create a new cluster.
- Create both a worker and control plane.
<img width="1046" height="386" alt="image" src="https://github.com/user-attachments/assets/f1b1866e-8942-46a5-afe1-b3e151ec0648" />

- If you DO NOT want Pod scheduling on the control plane then DO NOT run the following commands
```
kubectl taint nodes --all node-role.kubernetes.io/control-plane- || true
kubectl taint nodes --all node-role.kubernetes.io/master- || true
```
## Delete or reset the cluster and delete any leftover files/binaries
- Obviously a lot of things can go wrong while creating the cluster
- Sometimes I wanted to start a fresh
- But the leftover binaries created a lot of conflict if I ran the cluster creation commands again
- To fix this I either had to destory the entire cloud server instance or destory the local VM instance  and recreate them to restart cluster creation process
- Obviously this was very tidious and time consuming. Hence a cluster reset script was created that destroys the cluster and deletes any leftover binaries
- This gives you a fresh start without really destroying the machine
- `reset-control-plane.txt` `reset-worker.txt`
