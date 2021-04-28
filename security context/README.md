# Simple security context demo

Run a basic alpine pod with no options

```Kubectl run alpine-defaults --image alpine --restart Never -- /bin/sleep 99999```

exec in and run the ID command to see whats available to the user (root)

```kubectl exec alpine-defaults -- id ```

The pod is container is running as root and has access to a lot of groups

next, apply the following file which has a custom security context applied

```Kubectl apply -f alpine-user.yml```

run the exec command and notice the differences
