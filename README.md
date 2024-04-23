# coba-cd-argocd-k8s

### create pg cluster
1. add cnpg operator
```
helm repo add cloudnative-pg https://cloudnative-pg.io/charts/

helm install my-cloudnative-pg cloudnative-pg/cloudnative-pg --version 0.20.2
```
2. add private repo di node argocd anda
https://argo-cd.readthedocs.io/en/stable/user-guide/private-repositories/

3. install application.yaml di argocd node


### create user in pg pod
```
- kubectl exec -n pg -it my-pgsql-cluster-1 bash

- psql -U postgres
- CREATE DATABASE chat;
- create user usercoba with password 'asdasd';
- GRANT ALL PRIVILEGES ON DATABASE chat to usercoba;
- GRANT ALL ON SCHEMA public to usercoba;
- ALTER DATABASE chat OWNER  TO usercoba;
```


### redis helm values config
````
 values: |
      #  sentinel:
       #   enabled: true
       #   persistence:
       #     storageClass: local-storage
        volumePermissions:
          enabled: true
      # replica:
        ##  replicaCount: 3
        #  persistence:
        #    size: 5Gi
        #    storageClass: local-storage
        auth:
          enabled: true
          password: lintang
        master:
          livenessProbe:
            enabled: true
          persistence:
            size: 5Gi
            storageClass: local-storage
        global:
          storageClass: local-storage
```
