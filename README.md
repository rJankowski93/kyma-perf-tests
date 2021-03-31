# Performance tests for Kyma

## Test cases: 
### Internal communication (beetwen pods in cluster)
![Locust -> Locust Istio sidecar -> Nginx Istio sidecar -> Nginx](internal.png)

<img src="internal.png" alt="Locust -> Locust Istio sidecar -> Nginx Istio sidecar -> Nginx" width="200"/>

```console
export CLUSTER_DOMAIN=$(kubectl get cm shoot-info -n kube-system -o jsonpath='{.data.domain}')
helm install kyma-perf-tests kyma-perf-tests-chart --set testCaseNumber=1 --set clusterDomain=$CLUSTER_DOMAIN --set namespace=perf-tests --wait
```

#### Hyperscaler: Azure

| Users | req/s | avg  | mediana |p(99)|p(99.9)|p(99.99)|
| ------|:-----:| :---:|:----:  |---: |-----:|-----: |
| 10    | 2280  | 4   | 4       | 15  | 21   | 27    |
| 20    | 2336  | 7   | 6       | 28  | 34   | 39    |
| 30    | 2340  | 11  | 10      | 36  | 43   | 49    |
| 40    | 2419  | 14  | 12      | 41  | 49   | 56    |
| 50    | 2461  | 18  | 16      | 46  | 55   | 63    |

#### Hyperscaler: AWS

| Users | req/s | avg  | mediana |p(99)|p(99.9)|p(99.99)|
| ------|:-----:| :---:|:----:  |---: |-----:|-----: |
| 10    | 2271  | 4   | 4       | 12  | 18   | 22    |
| 20    | 2293  | 7   | 7       | 25  | 30   | 36    |
| 30    | 2355  | 11  | 10      | 30  | 36   | 42    |
| 40    | 2375  | 14  | 13      | 36  | 43   | 49    |
| 50    | 2411  |  18 | 17      | 40  | 47   | 54    |


### External communication 
![Locust -> ApiRule -> Nginx Istio sidecar -> Nginx](external.png)

```console
export CLUSTER_DOMAIN=$(kubectl get cm shoot-info -n kube-system -o jsonpath='{.data.domain}')
helm install kyma-perf-tests kyma-perf-tests-chart --set testCaseNumber=2 --set clusterDomain=$CLUSTER_DOMAIN --set namespace=perf-tests --wait
```

#### Hyperscaler: Azure

| Users | req/s | avg  | mediana |p(99)|p(99.9)|p(99.99)|
| ------|:-----:| :---:|:----:  |---: |-----:|-----:  |
| 10    | 1215  | 7    | 7      | 17  | 27   | 37     |
| 20    | 1388  | 14   | 13     | 26  | 35   | 43     |
| 30    | 1364  | 20   | 20     | 33  | 41   | 49     |
| 40    | 1383  | 27   | 26     | 41  | 50   | 59     |
| 50    | 1406  | 34   | 32     | 58  | 69   | 81     |


#### Hyperscaler: AWS

| Users | req/s | avg  | mediana |p(99)|p(99.9)|p(99.99)|
| ------|:-----:| :---:|:----:  |---: |-----:|-----:  |
| 10    |  1074 | 9    | 9      | 17  | 26   | 46     |
| 20    | 1233  | 15   | 15     | 26  | 39   | 69     |
| 30    |  1266 | 22   | 21     | 35  | 47   | 83     |
| 40    | 1274  | 29   | 28     | 44  | 55   | 120    |
| 50    | 1276  | 36   | 36     | 54  | 68   | 110    |