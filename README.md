# Kubernetes Exercises/Labs

A practical introduction to Kubernetes.

Solutions are given at the bottom, but you are encouraged to try to do the exercises without them. Use the [Kubernetes documentation](https://kubernetes.io/docs/home/) or search the web.

## Requirements

- [Rancher Desktop](https://docs.rancherdesktop.io/getting-started/installation/)

## Setup

Follow the following guide and setup a `two-node-cluster`: https://docs.rancherdesktop.io/how-to-guides/create-multi-node-cluster/

Verify by executing:

```sh
kubectl config get-contexts

#expected output
CURRENT   NAME                   CLUSTER                AUTHINFO                     NAMESPACE
*         k3d-two-node-cluster   k3d-two-node-cluster   admin@k3d-two-node-cluster
          rancher-desktop        rancher-desktop        rancher-desktop
```

```sh
kubectl get nodes

#expected output (node names, age and version may be different for you)
NAME                            STATUS   ROLES                  AGE     VERSION
k3d-two-node-cluster-server-0   Ready    control-plane,master   6m48s   v1.28.8+k3s1
k3d-two-node-cluster-agent-0    Ready    <none>                 6m45s   v1.28.8+k3s1
k3d-two-node-cluster-agent-1    Ready    <none>                 6m45s   v1.28.8+k3s1
```

## Exercises

### Exercise 1: Checking the Kubeconfig
1. Check the current context.
2. List all contexts.

### Exercise 2: Running Pods
1. Run an Nginx Pod.
2. Verify the Pod is running.

### Exercise 3: Creating Deployments
1. Create an Nginx Deployment.
2. Check the status of the Deployment.
3. Check the pod that got created.

### Exercise 4: Scaling Deployments
1. Scale the Nginx Deployment to 3 replicas.
2. Verify the scaling.
3. Check the placement of the pods (on the nodes).

### Exercise 5: Namespacing
1. Create a new namespace. Name it whatever you want.
2. Run another Nginx Pod in the new namespace.
3. Verify the Pod is running in the new namespace.

### Exercise 6: Checking Logs
1. Check the logs of the Nginx Pod.

### Exercise 7: Describing Resources
1. Describe the Nginx Pod.
2. Describe the Nginx Deployment.

### Exercise 8: Inside a container
1. Start a shell inside the container in the Nginx Pod.
2. Check the user.
3. Check the OS details.
4. Exit out of the container again.

### Exercise 9: Viewing Cluster Information
1. Get cluster information.
2. List the nodes in the cluster.

### Exercise 10: Cleaning Up
1. Delete the Nginx Pod.
2. Delete the Nginx Deployment.
3. Delete the namespace you created. 

## Solutions

### Exercise 1: Checking the Kubeconfig

1. Check the current context:
   
```bash
kubectl config current-context
```

2. List all contexts.

```bash
kubectl config get-contexts
```

### Exercise 2: Running Pods

1. Run an Nginx Pod:

```bash
kubectl run nginx --image=nginx
```

2. Verify the Pod is running.

```bash
kubectl get pods
```

### Exercise 3: Creating Deployments

1. Create an Nginx Deployment:

```bash
kubectl create deployment nginx-deployment --image=nginx
```

2. Check the status of the Deployment.

```bash
kubectl get deployments
```

3. Check the pod that got created.

```bash
kubectl get pods
```

### Exercise 4: Scaling Deployments

1. Scale the Nginx Deployment to 3 replicas.

```bash
kubectl scale deployment nginx-deployment --replicas=3
```

2. Verify the scaling.

```bash
kubectl get deployments
kubectl get pods
```

3. Check the placement of the pods (on the nodes).

```bash
kubectl get pods -o wide
kubectl describe nodes # alternatively
```

### Exercise 5: Namespacing

1. Create a new namespace. Name it whatever you want.

```bash
kubectl create namespace <namespace-name>
```

2. Run another Nginx Pod in the new namespace.

```bash
kubectl run nginx --image=nginx --namespace=<namespace-name>
```

3. Verify the Pod is running in the new namespace.

```bash

kubectl get pods --namespace=<namespace-name>
```

### Exercise 6: Checking Logs

1. Check the logs of the Nginx Pod.

```bash
kubectl logs nginx
```

### Exercise 7: Describing Resources

1. Describe the Nginx Pod.

```bash
kubectl describe pod nginx
```

2. Describe the Nginx Deployment.

```bash
kubectl describe deployment nginx-deployment
```

### Exercise 8: Inside a container

1. Start a shell inside the container in the Nginx Pod and attach to it.

```bash
kubectl exec -it nginx -- sh
```

2. Check the user.

```bash
$ whoami
```

3. Check the OS details.

```bash
$ cat /etc/os-release
```

4. Exit out of the container again.

```bash
$ exit
```

### Exercise 9: Viewing Cluster Information

1. Get cluster information.

```bash
kubectl cluster-info
```

2. List the nodes in the cluster.

```bash
kubectl get nodes
```

### Exercise 10: Cleaning up

1. Delete the Nginx Pod.

```bash
kubectl delete pod nginx
```

2. Delete the Nginx Deployment.

```bash
kubectl delete deployment nginx-deployment
```

3. Delete the namespace you created.

```bash
kubectl delete namespace <namespace-name>
```