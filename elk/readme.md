# [Kubernetes Observability: Log Aggregation Using ELK Stack](https://www.magalix.com/blog/kubernetes-observability-log-aggregation-using-elk-stack)

### Deploy
```
kubectl apply -f elk/
```

### Forward port to the Kibana service
```
kubectl port-forward -n kube-system svc/kibana-logging 5601:5601
```