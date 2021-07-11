## Prometheus, kube-state-metrics, Metrics Server, Grafana Example

1. Run `kubectl create namespace monitoring` to create a `monitoring` namespace.
2. Run `kubectl create -f ./ -R` to get kube-state-metrics, Grafana, and Prometheus resources in place.
3. 
4. Check NODEIP using: 
   
   `kubectl get nodes --selector=kubernetes.io/role!=master -o jsonpath={.items[*].status.addresses[?\(@.type==\"InternalIP\"\)].address}`
   
   kubectl get pods --namespace=monitoring
root@GGN000153118003:~/Monitoring-Kubernetes-Cluster/Prometheus-Grafana# kubectl get nodes --selector=kubernetes.io/role!=master -o jsonpath={.items[*].status.addresses[?\(@.type==\"InternalIP\"\)].address}
172.18.0.2root@GGN000153118003:~/Monitoring-Kubernetes-Cluster/Prometheus-Grafana# kubectl get pods --namespace=monitoring
NAME                                     READY   STATUS    RESTARTS   AGE
grafana-7f4d85b7c7-9trv2                 1/1     Running   0          17m
prometheus-deployment-599bbd9457-ddzgj   1/1     Running   0          17m

5. Visit http://[NODEIP]:30000 to view Prometheus. or isit http://[NODEIP]:32000/dashboard to view grafan.
6. Click on Graph. Select a metric from the drop-down (next to the Execute button) and then click Execute. You can switch between the Graph view and Console view.


**NOTE**: The Metrics Server YAML can be modified to enable it to run in more simple Kubernetes scenarios like Docker Desktop.


## Removing Resources

To remove all of the monitoring resources run `kubectl delete -f ./ -R`.

## Additional Details

Get more details on Prometheus at https://prometheus.io/docs/prometheus/latest/getting_started and https://devopscube.com/setup-prometheus-monitoring-on-kubernetes.

A list of Pod Metrics provided by kube-state-metrics can be found at https://github.com/kubernetes/kube-state-metrics/blob/master/docs/pod-metrics.md. 

