# Service Mesh Study

Repository to develop and tests Service Mesh Technology concepts with Istio.

## Install

SO: Linux/Windows WSL

#### Create a cluster

Install k3d, a lightweight cluster for development on Kubernetes.

```sh
curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
```

#### Create a cluster

```sh
k3d cluster create -p "8000:30000@loadbalancer" --agents 2
```

#### Install Istioctl

To manage istio inside your k8s (See [Documentation](https://istio.io/latest/docs/setup/getting-started/)).

#### Install Istio

```sh
istioctl install
```

#### Inject sidecar proxy

```sh
kubectl label namespace default istio-injection=enabled
```

Now your default namespace in k8s is ready to use Istio.

## Features

* [Canary Release](/canary-release)
