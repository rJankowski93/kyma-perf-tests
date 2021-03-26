# Performance tests for Kyma

## Test cases: 
### Internal communication (beetwen pods in cluster)
![Locust -> Locust Istio sidecar -> Nginx Istio sidecar -> Nginx](internal.png)

```console
export CLUSTER_DOMAIN=$(kubectl get cm shoot-info -n kube-system -o jsonpath='{.data.domain}')
helm install kyma-perf-tests kyma-perf-tests-chart --set testCaseNumber=1 --set clusterDomain=$CLUSTER_DOMAIN --set namespace=perf-tests --wait
```

### External communication 
![Locust -> ApiRule -> Nginx Istio sidecar -> Nginx](external.png)

```console
export CLUSTER_DOMAIN=$(kubectl get cm shoot-info -n kube-system -o jsonpath='{.data.domain}')
helm install kyma-perf-tests kyma-perf-tests-chart --set testCaseNumber=2 --set clusterDomain=$CLUSTER_DOMAIN --set namespace=perf-tests --wait
```
