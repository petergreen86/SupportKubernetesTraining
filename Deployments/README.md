# Deployments Demo

### Firstly, create the initial deployment of nginx:1.18-alpine

```kubectl create deploy nginx --image=nginx:1.18-alpine```

### Scale the deployment to 5 replicas

```kubectl scale deploy nginx --replicas=5```

### Upgrade the image to nginx:1.19-alpine

```kubectl set image deploy/nginx nginx=nginx:1.19-alpine```

### Upgrade the image again to nginx:1.20-apline using the --record option. This makes a note in the deployment of what was done

```kubectl set image deploy/nginx nginx=nginx:1.20-alpine --record=true```


### Inspect the rollout history - note that the 3rd revision has a description

```kubectl rollout history deploy/nginx```

### Roll it back to v2

```kubectl rollout undo deploy/nginx --to-revision=2```

### Describe deploy and look at revision and image

```kubectl describe deploy nginx```
