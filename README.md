# coba-cd-argocd-k8s

```
helm repo add cloudnative-pg https://cloudnative-pg.io/charts/

helm install my-cloudnative-pg cloudnative-pg/cloudnative-pg --version 0.20.2
```

https://argo-cd.readthedocs.io/en/stable/user-guide/private-repositories/

### create user in pg pod
```
- kubectl exec -n pg -it my-pgsql-cluster-1 bash

- psql -U postgres

- create user usercoba with password 'asdasd';
```
