# coba-cd-argocd-k8s
continous delivery golang api (https://github.com/lintang-b-s/chat-be), postgres, redis ke kubernetes cluster pake argocd.

### create pg cluster
1. add cnpg operator
```
helm repo add cloudnative-pg https://cloudnative-pg.io/charts/

helm install my-cloudnative-pg cloudnative-pg/cloudnative-pg --version 0.20.2
```
2. add private repo di node argocd anda
https://argo-cd.readthedocs.io/en/stable/user-guide/private-repositories/

3. install semua *-app.yaml di argocd node


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

### Teknologi
1. kubernetes
2. cloudnative pg (https://cloudnative-pg.io/)
3. redis bitnami helm chart (https://artifacthub.io/packages/helm/bitnami/redis)
4. golang

### redis helm values config
```
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

### Hasil
#### argocd


![argocd chat app](https://res.cloudinary.com/tutorial-lntng/image/upload/v1713867602/chat_mmq1cd.png)

![postgres app](https://res.cloudinary.com/tutorial-lntng/image/upload/v1713867602/postgres_kircv2.png)

![redis app](https://res.cloudinary.com/tutorial-lntng/image/upload/v1713867602/redis_mkvs9v.png)

#### my golang chat api
![chat api](https://res.cloudinary.com/tutorial-lntng/image/upload/v1713867608/Screenshot_from_2024-04-23_17-18-40_wlzvkx.png)


## TODO 
1. bikin jenkins CI (buat push image baru ke dockerhub & ganti versi image di deployment file golang-chat), di repo golang-chatny
2. tambahin service mesh linkerd?
