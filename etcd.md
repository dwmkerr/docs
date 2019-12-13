# etcd

Check the health of a cluster:

```sh
etcdctl --endpoints=https://10.0.1.244:2379,https://10.0.1.3:2379,https://10.0.1.242:2379 \
        --ca-file=/etc/ssl/etcd/ssl/ca.pem \
        --cert-file=/etc/ssl/etcd/ssl/member-master1.pem \
        --key-file=/etc/ssl/etcd/ssl/member-master1-key.pem \
        --debug cluster-health
```

Remove a member from the cluster:

```sh
etcdctl --endpoints=https://10.0.1.244:2379,https://10.0.1.3:2379,https://10.0.1.242:2379 \
        --ca-file=/etc/ssl/etcd/ssl/ca.pem \
        --cert-file=/etc/ssl/etcd/ssl/member-master1.pem \
        --key-file=/etc/ssl/etcd/ssl/member-master1-key.pem \
        member remove a0606ac27ee3d87c # this is the member id
```
