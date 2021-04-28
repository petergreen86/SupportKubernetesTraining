# Simple RBAC demo

create a developer namespace

```Kubectl create ns developer```

generate ssh keys for a "developer role"

```
openssl genrsa -out developer.key 2048

openssl req -new -key developer.key -out developer.csr -subj "/CN=developer/O=devorg“

sudo openssl x509 -req -in developer.csr -CA /etc/kubernetes/pki/ca.crt -CAkey /etc/kubernetes/pki/ca.key -CAcreateserial -out developer.crt -days 500

```

create a new user and context file (A context is a group of access parameters. Each context contains a Kubernetes cluster, a user, and a namespace. The current context is the cluster that is currently the default for kubectl)

```

kubectl config set-credentials developer --client-certificate=developer.crt  --client-key=developer.key

kubectl config set-context developer-context --cluster=kubernetes --namespace=developer --user=developer

```

Try and get pods using the context - this will fail because there are no permissions

```kubectl --context=developer-context get pods -n developer```

Create role and rolebinding

```
kubectl apply -f developer-role.yml
kubectl apply -f developer-rolebinding.yml
```

Create a pod using the context

```kubectl --context=developer-context run nginx --image=nginx```

Try and get the pods (it will fail because we removed its permission)

```kubectl --context=developer-context get po```
