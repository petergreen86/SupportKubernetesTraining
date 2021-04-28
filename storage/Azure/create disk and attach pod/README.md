# Using a disk with a pod

## Azure instructions

### Find the resource group ID

```az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv```

### Create the Disk

```az disk create \
  --resource-group <<RESOURCE GROUP>> \
  --name pg-mongodb \
  --size-gb 20 \
  --zone 2 \
  --query id --output tsv
```

This will return a path to be used as the DiskURI later

### Create a pod using the disk created

```kubectl apply -f mongodb-azurepd.yaml```

### exec into the pod and insert some data

```
Kubectl exec -it mongodb -- mongo

use mystore

Db.foo.insert({name: ‘foo’})
Db.foo.find()
exit
```

delete the pod and create it again - your data should still be there if you run the find command