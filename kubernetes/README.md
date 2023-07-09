## Kubernetes quick notes

[What actually worked w/ ArgoCD](https://trilium.perfectra1n.com/share/m990xINlhaIc)



### What I manually ran to set up the cluster
1. Used Kubespray, with the values [here](https://gitea.perfectra1n.com/perf3ct/kubespray-new-cluster-values).
   1. With this, I told Kubespray to install ArgoCD as well.
2. I then wanted to use Kustomized Helm so I ran the file [here](kubernetes/bootstrap/config/argocm.yaml).
3. Set up repos and their credentials (file [here](https://nas.jonathonfuller.com/f/3979539))
4. Created the root app file (and deployed it) so that it would deploy all the other apps ("app in apps" architecture).
5. Deploy the "root-apps", in [root-apps-app.yaml](kubernetes/bootstrap/root-apps-app.yaml) and [root-system-app.yaml](kubernetes/bootstrap/root-system-app.yaml)
6. Needed to run `sudo apt install nfs-common` on the nodes, for `nfs-subdir-external-provisioner`


## Examples

### Create PV and PVC
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nfs-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteMany
  nfs:
    server: 192.168.2.155
    path: /mnt/data/example1

---

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nfs-pvc
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 1Gi
  selector:
    matchLabels:
      type: nfs-pv

```