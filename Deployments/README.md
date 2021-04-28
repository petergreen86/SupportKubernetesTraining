# Deployments Demo

kubectl create deploy nginx --image=nginx:1.18-alpine

kubectl scale deploy nginx --replicas=5

kubectl set image deploy/nginx nginx=nginx:1.19-alpine

kubectl set image deploy/nginx nginx=nginx:1.20-alpine --record=true

Look at rollout history - kubectl rollout history deploy/nginx. Note the 3rd revision

Roll it back to v2

kubectl rollout undo deploy/nginx --to-revision=2

Describe deploy and look at revision and image
