## Kubernetes quick notes

[What actually worked w/ ArgoCD](https://trilium.perfectra1n.com/share/m990xINlhaIc)



### What I manually ran to set up the cluster
1. Used Kubespray, with the values [here](https://gitea.perfectra1n.com/perf3ct/kubespray-new-cluster-values).
   1. With this, I told Kubespray to install ArgoCD as well.
2. I then wanted to use Kustomized Helm so I ran the file [here](kubernetes/bootstrap/config/argocm.yaml).
3. Set up repos and their credentials (file [here](https://nas.jonathonfuller.com/f/3979539))
4. Created the root app file (and deployed it) so that it would deploy all the other apps ("app in apps" architecture).