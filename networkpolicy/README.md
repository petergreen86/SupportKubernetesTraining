# Network Policy

### Walkthrough Guide

We want 2 deployments here, with both exposed on port 80

```

kubectl run frontend --image=nginx

kubectl run backend --image=nginx

kubectl expose pod frontend --port=80

kubectl expose pod backend --port=80

```

Next, curl from the frontend pod to the backend service

```kubectl exec frontend -- curl backend```

And vice versa

```kubectl exec backend -- curl frontend```

Next, we want to apply a "default deny" network policy to our cluster (with the exception of port 53 as we want this for DNS resolution)

```kubectl apply -f default-deny-allow-dns.yaml```

Now, curl from the frontend to the backend again. Notice that it doesn't work

Apply the frontend policy to allow communication to the backend

```kubectl apply -f frontend.yaml```

 try to curl front the fronend to the backend - you'll see that it still doesn't work. This is because the backend isn't allowing incoming traffic

Apply the backend policy to give it capability to accept incoming traffic

```kubectl apply -f backend.yaml```

you should now be able to curl from the frontend to the backend (but not the other way around)
