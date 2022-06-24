# Canary Release

Study to create a canary release based on a specific HTTP Header.

## Install

Execute the following command to deploy the resources (navigate to this respective folder first).

```sh
kubectl apply -f ./config
```

## Concept

The above command will install a k8s Service with two deployments associated, one with version A and the another with version B.

By default, if you call directly the k8s Service, the load balancing is going to be round robin.

Using Istio, we create a virtual service upon the k8s, and then we apply routing and destination rules based on Istio resources.

In this example case, we are directing traffic to specific subsets based on a HTTP Header.

On of the main advantages of the Istio approach is that there's no need to modify the application layer. All the routing is configured in the infrastructure layer abstracting containers and microsservices technologies.

## Testing

### Install Addons

#### Prometheus

To gather containers execution data. See [Documentation](https://istio.io/latest/docs/ops/integrations/prometheus/).

#### Kiali

Is a dashboard to visualize traffic inside the cluster with Istio. See [Documentation](https://istio.io/latest/docs/ops/integrations/kiali/).

#### Fortio

Fortio is a lightweight tool for making http requests.

To install follow the [Documentation](https://istio.io/latest/docs/tasks/traffic-management/circuit-breaking/#adding-a-client).

To execute fortio.

```sh
kubectl exec "$FORTIO_POD" -c fortio -- fortio load -c 2 -qps 2 -t 200s -loglevel Warning http://nginx-service:8000
```

To execute fortio with filial header.

```sh
kubectl exec "$FORTIO_POD" -c fortio -- fortio load -c 2 -qps 1 -t 200s -loglevel Warning -H Filial:1000 http://nginx-service:8000
```