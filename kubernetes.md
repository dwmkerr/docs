# kubernetes

## Deleting namespaces stuck in 'terminating'

Check out this excellent solution from:

https://github.com/kubernetes/kubernetes/issues/60807

(Modified a bit)

```sh
kubectl proxy &
kubectl_proxy_pid=$!

for namespace in $(kubectl get namespaces | grep Terminating | awk '{print $1}'); do
  echo "processing $namespace"
  kubectl get namespace $namespace -o json | jq 'del(.spec.finalizers)' | curl -k -H "Content-Type: application/yaml" -X PUT -d @- http://127.0.0.1:8001/api/v1/namespaces/$namespace/finalize
done

kill $kubectl_proxy_pid
```

## Setting the default namespace for commands

Easy:

```sh
k config set-context --current --namespace ingress-nginx
```

## Dealing with broken etcd

There's an excellent set of tips here:

https://github.com/kubernetes-sigs/kubespray/issues/3471#issuecomment-530036084

This was the only solution I could find when I had blatted some etcd configuration by re-creating a master node (with a new IP, but the same name). This required a new set of certificates etc to be generated. There were some persistent problems using Kubespray; following the tips here solved them.
