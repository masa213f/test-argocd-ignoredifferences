# test

```console
$ kubectl create namespace argocd
$ kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.4.17/manifests/install.yaml

$ kubectl edit cm -n argocd argocd-cmd-params-cm
...
data:                          # Add
  controller.log.level: debug  # Add

$ kubectl rollout restart sts -n argocd argocd-application-controller
$ kubectl rollout status sts -n argocd argocd-application-controller

$ curl -sSL -o argocd https://github.com/argoproj/argo-cd/releases/download/v2.4.17/argocd-linux-amd64
$ chmod +x argocd
$ kubectl port-forward svc/argocd-server -n argocd 8080:443 &> /dev/null &

$ PASS=$(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d)
$ ./argocd login --insecure localhost:8080 --username admin --password ${PASS}

$ kubectl apply -f https://raw.githubusercontent.com/rook/rook/v1.10.5/deploy/examples/crds.yaml
$ kubectl apply -f https://raw.githubusercontent.com/masa213f/test/main/application.yaml

$ ./argocd app sync testapp
$ kubectl get cephcluster cluster -o yaml

$ ./argocd app set testapp --path after
$ ./argocd app sync testapp
$ kubectl get cephcluster cluster -o yaml

$ ./argocd app diff testapp

===== ceph.rook.io/CephCluster default/cluster ======
61a62,67
>         nodeAffinity:
>           requiredDuringSchedulingIgnoredDuringExecution:
>             nodeSelectorTerms:
>             - matchExpressions:
>               - key: ssd
>                 operator: Exists
```
