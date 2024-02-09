# Iniciando com Kubernetes

### Create First Cluster with `kind`

- `kind create cluster`

```bash
➜ kind create cluster
Creating cluster "kind" ...
 ✓ Ensuring node image (kindest/node:v1.29.1) 🖼
 ✓ Preparing nodes 📦
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹️
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
Set kubectl context to "kind-kind"
You can now use your cluster with:

kubectl cluster-info --context kind-kind

Not sure what to do next? 😅  Check out https://kind.sigs.k8s.io/docs/user/quick-start/
```

### Cluser Info

- `kubectl cluster-info --context kind-kind`

```bash
kubectl cluster-info --context kind-kind
Kubernetes control plane is running at https://127.0.0.1:43485
CoreDNS is running at https://127.0.0.1:43485/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

### Configs Kubernetes

- `cat ~/.kube/config`

### Ver container `kind-control-plane`

- `docker ps`

```bash
CONTAINER ID   IMAGE                  COMMAND                  CREATED          STATUS          PORTS                       NAMES
ea202c362059   kindest/node:v1.29.1   "/usr/local/bin/entr…"   11 minutes ago   Up 11 minutes   127.0.0.1:43485->6443/tcp   kind-control-plane
```

#### Ver `nodes`

- `kubectl get nodes`

```bash
NAME                 STATUS   ROLES           AGE   VERSION
kind-control-plane   Ready    control-plane   13m   v1.29.1
```

#### Ver `clusters`

- `kind get clusters`

```bash
kind
```

#### Deletar um `cluster`

- `kind delete clusters kind`

```bash
Deleted nodes: ["kind-control-plane"]
Deleted clusters: ["kind"]
```

#### Create `clusters` with 4 `nodes` in `kind`

- `kind create cluster --config=k8s/01kind.yaml --name=williamkoller`

```bash
Creating cluster "kind-williamkoller" ...
 ✓ Ensuring node image (kindest/node:v1.29.1) 🖼
 ✓ Preparing nodes 📦 📦 📦 📦
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹️
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
 ✓ Joining worker nodes 🚜
Set kubectl context to "kind-kind"
You can now use your cluster with:

kubectl cluster-info --context kind-williamkoller

Have a nice day! 👋
```

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4

nodes:
  - role: control-plane
  - role: worker
  - role: worker
  - role: worker
```

- `kubectl get nodes`

```bash
NAME                          STATUS   ROLES           AGE     VERSION
williamkoller-control-plane   Ready    control-plane   8m21s   v1.29.1
williamkoller-worker          Ready    <none>          7m59s   v1.29.1
williamkoller-worker2         Ready    <none>          7m58s   v1.29.1
williamkoller-worker3         Ready    <none>          7m59s   v1.29.1

```

### List clusters

- `kubectl config get-clusters`

### Delete cluster

- `kubectl config delete-cluster kind-fullcycle`

### change of clusters

- `kubectl config use-context name-of-cluster`