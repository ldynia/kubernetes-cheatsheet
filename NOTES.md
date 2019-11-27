# ETCD

```bash
$ kubectl get ds -n kube-system
NAME                         DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR                 AGE
kube-proxy                   3         3         3       3            3           beta.kubernetes.io/os=linux   18d

$ kubectl get ds kube-proxy -o yaml --export
``



`/etc/kubernetes/manifests/etcd.yaml`

```bash
$ docker run -p 2379:2379 --name etcd quay.io/coreos/etcd:v3.0.16 /usr/local/bin/etcd -advertise-client-urls http://0.0.0.0:2379 -listen-client-urls http://0.0.0.0:2379

$ docker exec -it etcd /bin/ash
$ etcdctl set a one
$ etcdctl get a
$ etcdctl updated a two
```

```bash
$ kubectl exec -it etcd-master --namespace=kube-system -- /bin/ash

$ export ETCDCTL_API=3
$ etcdctl --cacert /etc/kubernetes/pki/etcd/ca.crt --key /etc/kubernetes/pki/etcd/server.key --cert /etc/kubernetes/pki/etcd/server.crt get / --prefix --keys-only
$ etcdctl --cacert /etc/kubernetes/pki/etcd/ca.crt --key /etc/kubernetes/pki/etcd/server.key --cert /etc/kubernetes/pki/etcd/server.crt get /registry/serviceaccounts/vagrant/default -w json
```

# Kubernetes Api-Server

`/etc/kubernetes/manifests/kube-apiserver.yaml`

```bash
$ APISERVER=$(kubectl config view -o jsonpath="{.clusters[0].cluster.server}")
$ TOKEN=$(kubectl get secrets -o jsonpath="{.items[?(@.metadata.annotations['kubernetes\.io/service-account\.name']=='default')].data.token}"|base64 --decode)
$ curl -X GET $APISERVER/api --header "Authorization: Bearer $TOKEN" --insecure
```

# Kubernetes Controller

`/etc/kubernetes/manifests/kube-controller-manager.yaml`

# Kubernetes Scheduler

`/etc/kubernetes/manifests/kube-scheduler.yaml`

# Kublet
service config `/etc/systemd/system/kubelet.service.d/10-kubeadm.conf`
