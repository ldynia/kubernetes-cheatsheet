# Kubernetes Cheatsheet

## References
* [kubernetes cluster (virtualbox + ansible)](vagrant-ansible-k8-centos)
* [kubectl cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
* [kubernetes by example](http://kubernetesbyexample.com/)

```bash
$ kubectl
kubectl controls the Kubernetes cluster manager.

 Find more information at: https://kubernetes.io/docs/reference/kubectl/overview/

Basic Commands (Beginner):
  create         Create a resource from a file or from stdin.
  expose         Take a replication controller, service, deployment or pod and expose it as a new Kubernetes Service
  run            Run a particular image on the cluster
  set            Set specific features on objects

Basic Commands (Intermediate):
  explain        Documentation of resources
  get            Display one or many resources
  edit           Edit a resource on the server
  delete         Delete resources by filenames, stdin, resources and names, or by resources and label selector

Deploy Commands:
  rollout        Manage the rollout of a resource
  scale          Set a new size for a Deployment, ReplicaSet, Replication Controller, or Job
  autoscale      Auto-scale a Deployment, ReplicaSet, or ReplicationController

Cluster Management Commands:
  certificate    Modify certificate resources.
  cluster-info   Display cluster info
  top            Display Resource (CPU/Memory/Storage) usage.
  cordon         Mark node as unschedulable
  uncordon       Mark node as schedulable
  drain          Drain node in preparation for maintenance
  taint          Update the taints on one or more nodes

Troubleshooting and Debugging Commands:
  describe       Show details of a specific resource or group of resources
  logs           Print the logs for a container in a pod
  attach         Attach to a running container
  exec           Execute a command in a container
  port-forward   Forward one or more local ports to a pod
  proxy          Run a proxy to the Kubernetes API server
  cp             Copy files and directories to and from containers.
  auth           Inspect authorization

Advanced Commands:
  diff           Diff live version against would-be applied version
  apply          Apply a configuration to a resource by filename or stdin
  patch          Update field(s) of a resource using strategic merge patch
  replace        Replace a resource by filename or stdin
  wait           Experimental: Wait for a specific condition on one or many resources.
  convert        Convert config files between different API versions
  kustomize      Build a kustomization target from a directory or a remote url.

Settings Commands:
  label          Update the labels on a resource
  annotate       Update the annotations on a resource
  completion     Output shell completion code for the specified shell (bash or zsh)

Other Commands:
  api-resources  Print the supported API resources on the server
  api-versions   Print the supported API versions on the server, in the form of "group/version"
  config         Modify kubeconfig files
  plugin         Provides utilities for interacting with plugins.
  version        Print the client and server version information

Usage:
  kubectl [flags] [options]

Use "kubectl <command> --help" for more information about a given command.
Use "kubectl options" for a list of global command-line options (applies to all commands).
```

## Kubectl Autocompletion
```bash
$ echo $SHELL
/bin/bash

$ kubectl completion -h
$ kubectl completion bash > ~/.kube/completion.bash.inc

$ printf "
# Kubectl shell completion
source '$HOME/.kube/completion.bash.inc'
" >> $HOME/.bash_profile

$ source $HOME/.bash_profile
```

## Nodes info
```bash
$ kubectl version
$ kubectl get nodes -o json | jq .items[].status.nodeInfo
```

```bash
$ kubectl api-resources
NAME                              SHORTNAMES   APIGROUP                       NAMESPACED   KIND
bindings                                                                      true         Binding
componentstatuses                 cs                                          false        ComponentStatus
configmaps                        cm                                          true         ConfigMap
endpoints                         ep                                          true         Endpoints
events                            ev                                          true         Event
limitranges                       limits                                      true         LimitRange
namespaces                        ns                                          false        Namespace
nodes                             no                                          false        Node
persistentvolumeclaims            pvc                                         true         PersistentVolumeClaim
persistentvolumes                 pv                                          false        PersistentVolume
pods                              po                                          true         Pod
podtemplates                                                                  true         PodTemplate
replicationcontrollers            rc                                          true         ReplicationController
resourcequotas                    quota                                       true         ResourceQuota
secrets                                                                       true         Secret
serviceaccounts                   sa                                          true         ServiceAccount
services                          svc                                         true         Service
mutatingwebhookconfigurations                  admissionregistration.k8s.io   false        MutatingWebhookConfiguration
validatingwebhookconfigurations                admissionregistration.k8s.io   false        ValidatingWebhookConfiguration
customresourcedefinitions         crd,crds     apiextensions.k8s.io           false        CustomResourceDefinition
apiservices                                    apiregistration.k8s.io         false        APIService
controllerrevisions                            apps                           true         ControllerRevision
daemonsets                        ds           apps                           true         DaemonSet
deployments                       deploy       apps                           true         Deployment
replicasets                       rs           apps                           true         ReplicaSet
statefulsets                      sts          apps                           true         StatefulSet
tokenreviews                                   authentication.k8s.io          false        TokenReview
localsubjectaccessreviews                      authorization.k8s.io           true         LocalSubjectAccessReview
selfsubjectaccessreviews                       authorization.k8s.io           false        SelfSubjectAccessReview
selfsubjectrulesreviews                        authorization.k8s.io           false        SelfSubjectRulesReview
subjectaccessreviews                           authorization.k8s.io           false        SubjectAccessReview
horizontalpodautoscalers          hpa          autoscaling                    true         HorizontalPodAutoscaler
cronjobs                          cj           batch                          true         CronJob
jobs                                           batch                          true         Job
certificatesigningrequests        csr          certificates.k8s.io            false        CertificateSigningRequest
leases                                         coordination.k8s.io            true         Lease
events                            ev           events.k8s.io                  true         Event
daemonsets                        ds           extensions                     true         DaemonSet
deployments                       deploy       extensions                     true         Deployment
ingresses                         ing          extensions                     true         Ingress
networkpolicies                   netpol       extensions                     true         NetworkPolicy
podsecuritypolicies               psp          extensions                     false        PodSecurityPolicy
replicasets                       rs           extensions                     true         ReplicaSet
ingresses                         ing          networking.k8s.io              true         Ingress
networkpolicies                   netpol       networking.k8s.io              true         NetworkPolicy
runtimeclasses                                 node.k8s.io                    false        RuntimeClass
poddisruptionbudgets              pdb          policy                         true         PodDisruptionBudget
podsecuritypolicies               psp          policy                         false        PodSecurityPolicy
clusterrolebindings                            rbac.authorization.k8s.io      false        ClusterRoleBinding
clusterroles                                   rbac.authorization.k8s.io      false        ClusterRole
rolebindings                                   rbac.authorization.k8s.io      true         RoleBinding
roles                                          rbac.authorization.k8s.io      true         Role
priorityclasses                   pc           scheduling.k8s.io              false        PriorityClass
csidrivers                                     storage.k8s.io                 false        CSIDriver
csinodes                                       storage.k8s.io                 false        CSINode
storageclasses                    sc           storage.k8s.io                 false        StorageClass
volumeattachments                              storage.k8s.io                 false        VolumeAttachment
```

```bash
$ kubectl explain pods
KIND:     Pod
VERSION:  v1

DESCRIPTION:
     Pod is a collection of containers that can run on a host. This resource is
     created by clients and scheduled onto hosts.

FIELDS:
   apiVersion	<string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/api-conventions.md#resources

   kind	<string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/api-conventions.md#types-kinds

   metadata	<Object>
     Standard objects metadata. More info:
     https://git.k8s.io/community/contributors/devel/api-conventions.md#metadata

   spec	<Object>
     Specification of the desired behavior of the pod. More info:
     https://git.k8s.io/community/contributors/devel/api-conventions.md#spec-and-status

   status
     Most recently observed status of the pod. This data may not be up to date.
     Populated by the system. Read-only. More info:
     https://git.k8s.io/community/contributors/devel/api-conventions.md#spec-and-status
 ```


## Debugging

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: alpine
  namespace: phenex
spec:
  containers:
  - name: alpine
    image: alpine
    command:
      - sleep
      - "3600"
    imagePullPolicy: IfNotPresent
  restartPolicy: Always
```

```bash
$ kubectl get svc
NAME    TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)     AGE
mongo   ClusterIP   None         <none>        27017/TCP   95m
redis   ClusterIP   None         <none>        6379/TCP    95m

$ kubectl exec -it alpine /bin/sh

$ ping mongo
$ nslookup mongo
$ nslookup mongo.phenex

$ ping redis
$ nslookup reids
$ nslookup reids.phenex
```

## Pod

**YAML**
```yamla
apiVersion: v1
kind: Pod
metadata:
  name: nginx-demo
  labels:
    app: nginx-demo
spec:
  containers:
  - name: nginx-demo
    image: nginx
```

Run pod in foreground.
```bash
$ kubectl run nginx --image=nginx --generator=run-pod/v1 --dry-run -o yaml

$ kubectl run alpine -it --image=alpine --restart=Never
$ kubectl --namespace=default run alpine -it --image=alpine --restart=Never
$ kubectl run alpine -it --image=alpine --restart=Never --command -- hostname -i

$ kubectl delete pod $(kubectl get pods | grep Completed | awk '{print $1}')

```
Run pod in background.

```bash
# Busybox image
$ kubectl run alpine --image=alpine --restart=Never --command -- sleep 1d
```

Hook into pod.
```bash
$ kubectl exec -it alpine -- ash

# attach seems to not work
$ kubectl attach -it alpine
```

Label pods.
```bash
# Add label
$ kubectl label pod alpine created_by=ludd
$ kubectl get pods --show-labels

# Remove label
$ kubectl label pod alpine created_by-
```

## Debugging

```bash
# Generic way
$ kubectl get <resources>

# Describe pod
$ kubectl describe pod <podname>

# Describe pods
$ kubectl get pod alpine --output=wide
$ kubectl get pod alpine --show-labels

# Logs images
$ kubectl logs alpine
$ kubectl logs -f alpine
$ kubectl logs -p alpine

# Hook into alpine container
$ echo "Writing to stdout" >> /proc/1/fd/1
$ echo "Writing to stdout" >> /dev/stdout
```

## Delete pod
```bash
$ kubectl delete pod alpine
```

## Deployment

```bash
# Create deployment
$ kubectl create deployment nginx --image=nginx

# Get Deploymnet
$ kubectl get deployment --show-labels

# Short notation for fetching multiple resources
$ kubectl get deploy,rs,po --show-labels
NAME                          READY   UP-TO-DATE   AVAILABLE   AGE   LABELS
deployment.extensions/nginx   1/1     1            1           24m   app=nginx

NAME                                     DESIRED   CURRENT   READY   AGE   LABELS
replicaset.extensions/nginx-65f88748fd   1         1         1       24m   app=nginx,pod-template-hash=65f88748fd

NAME                         READY   STATUS    RESTARTS   AGE   LABELS
pod/nginx-65f88748fd-r9t47   1/1     Running   0          24m   app=nginx,pod-template-hash=65f88748fd

# Print yamla deployment file
$ kubectl get deployments nginx --output=yaml --export
```

## Service

```bash
# Create service type of nodeport & clusterip
$ kubectl create service nodeport nginx --tcp=80
$ kubectl create service clusterip nginx --tcp=80

# Crete service using expose command
$ kubectl expose deployment nginx --port=80 --type=NodePort
$ kubectl expose deployment nginx --port=80 --type=ClusterIP

$ kubectl get svc nginx --show-labels
NAME    TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE     LABELS
nginx   NodePort   10.98.29.213   <none>        80:31700/TCP   3m58s   app=nginx

# Print yamla deployment file
$ kubectl get svc nginx --output=yaml --export

$ curl localhost:31700
$ curl http://192.168.234.230:31700/
$ curl http://192.168.234.231:31700/
$ curl http://192.168.234.232:31700/

$ kubectl delete svc nginx
$ kubectl delete deploy nginx
```

## Ingress

To expose application to public you have to have installed [traefik.io](https://docs.traefik.io/user-guide/kubernetes/).
Additionally, your machine's host file `/etc/hosts` should point to one of the IPs of the cluster. e.g.

```bash
192.168.234.230 app.k8
192.168.234.231 app.k8
192.168.234.232 app.k8
```

Reproduce these structure on master node.

```bash
$ tree /nfs/www/demo
├── deployment.yaml
├── ingress.yaml
├── svc.yaml
└── html
    └── index.html
```

**index.html**
```html
<!DOCTYPE html>
<html>

<head>
  <title>Welcome to nginx!</title>
  <style>
      body {
          width: 35em;
          margin: 0 auto;
          font-family: Tahoma, Verdana, Arial, sans-serif;
      }
  </style>
</head>

<body>
	<h1>Hello Volumes!</h1>
</body>

</html>
```

**deployment.yaml** with volume.
```yaml
---
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  labels:
    run: nginx
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      run: nginx
  template:
    metadata:
      labels:
        run: nginx
    spec:
      containers:
      - image: nginx
        name: nginx
        volumeMounts:
        - mountPath: /usr/share/nginx/html
          name: html-volume
      volumes:
       - name: html-volume
         hostPath:
           path: /mnt/nfs/www/demo/html
           type: Directory
```

**service.yaml**
```yaml
# Create service
# kubectl expose deployment nginx --port=80 --type=ClusterIP
# kubectl expose deployment nginx --port=80 --type=NodePort
---
apiVersion: v1
kind: Service
metadata:
  labels:
    run: nginx
  name: nginx
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    run: nginx
  type: ClusterIP
```

**ingress.yaml**
```yaml
---
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: nginx
spec:
  rules:
  - host: app.k8
    http:
      paths:
      - backend:
          serviceName: nginx
          servicePort: 80
```


```bash
$ kubectl apply -f deployment.yaml
$ kubectl apply -f service.yaml
$ kubectl apply -f ingress.yaml
```


# Labels

Show labels.
```bash
$ kubectl get nodes
NAME        STATUS   ROLES    AGE     VERSION   LABELS
master      Ready    master   6h16m   v1.15.0   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=master,kubernetes.io/os=linux,node-role.kubernetes.io/master=
web01       Ready    <none>   6h15m   v1.15.0   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=web01,kubernetes.io/os=linux
compute01   Ready    <none>   6h15m   v1.15.0   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=compute01,kubernetes.io/os=linux
```

Label nodes
```bash
$ kubectl label nodes web01 node=web
node/web01 labeled

$ kubectl label nodes compute01 type=compute
node/compute01 labeled
```

Delete labels
```bash
$ kubectl label nodes web01 type-
$ kubectl label nodes compute01 type-
```

Roles
```bash
$ kubectl get nodes --show-labels
$ kubectl label nodes nebula-compute01 node-role.kubernetes.io/compute=
```

Annotate resources
```bash
$ kubectl get nodes compute01 -o jsonpath='{.metadata.annotations}'
$ kubectl annotate node compute01 compute-type=cpu
```

# Taints

Show taints
```bash
$ kubectl get nodes -o json | jq .items[].spec
$ kubectl get nodes -o json | jq .items[].spec.taints
```

Add taints
```bash
$ kubectl taint node compute01 type=compute:NoSchedule
$ kubectl taint node master node-role.kubernetes.io/master:NoSchedule
```

Delete taints
```bash
$ kubectl taint node compute01 type-
$ kubectl taint nodes --all node-role.kubernetes.io/master-
```

# Namespace
```bash
$ kubectl config view
$ kubectl create namespace vagrant

$ kubectl --namespace=vagrant run nginx --image=nginx
$ kubectl --namespace=vagrant get pods

$ kubectl config set-context vagrant --namespace=vagrant --user=kubernetes-admin

$ kubectl config set contexts.vagrant.cluster kubernetes
$ kubectl config get-contexts

$ kubectl config user-context vagrant
```

# Persistent Volumes
[persistent volume storage](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/)
[persistent volume deployment](https://kubernetes.io/docs/tasks/run-application/run-single-instance-stateful-application/)
