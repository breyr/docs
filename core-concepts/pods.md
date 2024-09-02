# Pods

## What is a Pod?

Pods are what encapsulate your application containers.

A pod is a single instance of an application and is the smallest object you can create in k8s

Pods usually have a 1 to 1 relationship with containers running your application

When scaling you are adding and removing pods

* you can have multiple containers in the same pod, but these containers are not the same

## Deploying a Pod

### kubectl

kubectl run nginx - creates a pod and runs the specified docker container inside

```
kubectl run nginx --image nginx
```

kubectl get pods - list all pods in the cluster

## Pods with YAML

A kubernetes definition file always has 4 items

1. apiVersion

| Kind       | Version |
| ---------- | ------- |
| POD        | v1      |
| Service    | v1      |
| ReplicaSet | apps/v1 |
| Deployment | apps/v1 |

2. kind
3. metadata
4. spec

```yaml
apiVersion: v1
kind: Pod
metadata: # dictionary
    name: myapp-pod
    labels:
        app: myapp
spec:
    containers: # list/array
        - name: nginx-controller # dash means first item in list
          image: nginx
```

### To run a definition file

`kubectl create -f pod-definition.yml`

### More useful commands

`kubectl get pods`

`kubectl describe pod myapp-pod`

* get information related to a pod

### Using kubectl run to create yaml files

```
kubectl run redis --image=redis --dry-run=client > pod-definition.yaml
```

## Editing a Pod

There are two ways of editing a pod:

{% tabs %}
{% tab title="kubectl edit " %}
To modify the properties of a pod, use `kubectl edit pod <pod-name>`

* this will open the file in vim
{% endtab %}

{% tab title="Get pod definition" %}
`kubectl get pod <pod-name> -o yaml pod-definition.yaml`

Then edit the file, delete and re-create the pod
{% endtab %}
{% endtabs %}

Note only the folowing properties are editable:

1. spec.containers\[\*].image
2. spec.initContainers\[\*].image
3. spec.activeDeadlineSeconds
4. spec.tolerations
5. spec.terminationGracePeriodSeconds

