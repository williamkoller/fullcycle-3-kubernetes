# Kubernetes

## O que é Kubernetes?

- Kubernetes (k8s) é um produto Open Source utilizado para automatizar a implantação, o dimensionamento e o gerenciamento de aplicativos em container

## De onde veio?!

- Google
  - Borg
  - Omega
  - Kubernetes

### Pontos importantes

- Kubernetes é disponibilizado atraves de um conjunto de APIs
- Normalmente acessamos a API usando o CLI: kubectl
- Tudo é baseado em estado. Voce configura o estado de cada objeto
- Kubernetes Master
  - Kube-apiserver
  - Kube-controller-manager
  - Kube-scheduler
- Outros Nodes:

  - Kubelet
  - Kubeproxy

- Cluster:
  - conjunto de maquinas (Nodes)
  - Cada maquina possui uma quantidade de vCPU e memoria
- Pods:
  - UInidade que contem os containers provisionados
  - O Pod representa os processos rodando no cluster

### Deployment

- Objetivo de provisionar os pods
- Tem que saber quantas replicas ira provisionar `ReplicasSets`

### Services

- Os Services no Kubernetes fornecem uma maneira de expor conjuntos de pods como um único ponto de acesso. Isso permite que outros componentes do seu aplicativo se comuniquem com os pods através de um endereço IP e uma porta fixa, independentemente de quantos pods estejam sendo executados. Os Services podem ser usados para agrupar conjuntos de pods e fornecer acesso a eles de forma controlada.

### Instalar

- [Kubernetes](https://kubernetes.io/releases/download/)
- [Kind](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)

