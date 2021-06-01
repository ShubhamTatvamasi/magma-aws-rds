# backup-certs

backup certificates:
```bash
kubectl get secret nms-certs -o yaml > nms-certs.yaml
kubectl get secret orc8r-certs -o yaml > orc8r-certs
```


