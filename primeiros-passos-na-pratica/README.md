# Primeiros passos na pratica

### Gerar imagem `docker`

- `docker build -t williamkoller/hello-golang .`

### Rodar container `docker`

- `docker run --rm -p 8080:8080 williamkoller/hello-golang`

### Subir a imagem no hub.docker

- `docker push williamkoller/hello-golang`

```bash
Using default tag: latest
The push refers to repository [docker.io/williamkoller/hello-golang]
8b683326cf31: Pushed
1f3c2906a4cc: Pushed
5f70bf18a086: Mounted from library/golang
888d9d1b4435: Mounted from library/golang
21abefad2f2c: Mounted from library/golang
6dd5a23a5acc: Mounted from library/golang
d4fc045c9e3a: Mounted from library/golang
latest: digest: sha256:712d204ad12bc394812051ba9885bc74efb0b588f2a5b0bf0f8174c05b2cf5e9 size: 1782
```

### Create pod

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: goserver
  labels:
    app: goserver

spec:
  containers:
    - name: goserver
      image: williamkoller/hello-golang:latest
```

- `kube apply -f k8s/pod.yaml`

```bash
pod/goserver created
```

### Ver pod

- `kubectl get pod`

```bash
NAME       READY   STATUS    RESTARTS   AGE
goserver   1/1     Running   0          2m59s
```

### Acessar o pod

- `kube port-forward pod/goserver 8080:8080`

```bash
Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
```

_Obs: precisa rodar o port-forward, pois nao temos nenhum network configurado_

### ReplicaSet

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: goserver
  labels:
    app: goserver

spec:
  selector:
    matchLabels:
      app: goserver
  replicas: 2

  template:
    metadata:
      name: goserver
      labels:
        app: goserver

    spec:
      containers:
        - name: goserver
          image: williamkoller/hello-golang:latest
```

- `kube apply -f k8s/replicas-set.yaml`

```bash
replicaset.apps/goserver created
```

- `kubectl get replicasets`

```bash
NAME       DESIRED   CURRENT   READY   AGE
goserver   2         2         2       4m20s
```

### Vamos apagar um dos pods para ver ele recriando automaticamente

- `kubectl get pods`

```bash
NAME             READY   STATUS    RESTARTS   AGE
goserver         1/1     Running   0          36m
goserver-p7mmb   1/1     Running   0          11m
```

- `kube delete pod goserver`

```bash
pod "goserver" deleted
```

- `kube get pods`

```bash
NAME             READY   STATUS              RESTARTS   AGE
goserver-p7mmb   1/1     Running             0          13m
goserver-x2j6z   0/1     ContainerCreating   0          4s
```

- Vamos alterar para 10 replicas

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: goserver
  labels:
    app: goserver

spec:
  selector:
    matchLabels:
      app: goserver
  replicas: 10

  template:
    metadata:
      name: goserver
      labels:
        app: goserver

    spec:
      containers:
        - name: goserver
          image: williamkoller/hello-golang:latest

```

- `kubectl get pods`

```bash
NAME             READY   STATUS              RESTARTS   AGE
goserver-87k8z   0/1     ContainerCreating   0          3s
goserver-9nbnf   0/1     ContainerCreating   0          3s
goserver-hp4xk   1/1     Running             0          3s
goserver-klpl6   0/1     ContainerCreating   0          3s
goserver-kr6vg   1/1     Running             0          3s
goserver-p7mmb   1/1     Running             0          16m
goserver-rprkj   1/1     Running             0          3s
goserver-s6jqj   0/1     ContainerCreating   0          3s
goserver-x2j6z   1/1     Running             0          2m49s
goserver-xlwdk   0/1     ContainerCreating   0          3s
```

- `kubectl get replicasets`

```bash
NAME       DESIRED   CURRENT   READY   AGE
goserver   10        10        10      18m
```