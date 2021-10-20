# Buildpacks in a Pod

This demonstrates running CNCF Buildpacks in a regular Kubernetes Pod.

This is effectively what Tekton, Shipwright, kpack and others do, without all that ornamentation and friendliness.

1. Set up registry credentials

```
kubectl create secret generic regcred \
    --from-file=.dockerconfigjson=~/.docker/config.json \
    --type=kubernetes.io/dockerconfigjson
```

1. Run the build

```
kubectl create -f buildpack-pod.yaml
```

This will create a new Pod with a randomly generated name like `buildpacks-a1db2`

1. Watch logs

```
kubectl logs buildpacks-a1db2 -f 
```

1. See the built image digest

```
kubectl get pod buildpacks-a1db2 -ojsonpath="{.status.containerStatuses[0].terminationMessage}"
```