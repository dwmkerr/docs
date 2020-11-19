# docs

Useful guides, documents, snippets for working with tech.


<!-- vim-markdown-toc GFM -->

* [Introduction](#introduction)
* [The Craft of Programming](#the-craft-of-programming)
* [Kubernetes](#kubernetes)
    * [Set the Current Context](#set-the-current-context)
    * [Setting Cluster Credentials on the Command Line](#setting-cluster-credentials-on-the-command-line)
    * [Deleting namespaces stuck in 'terminating'](#deleting-namespaces-stuck-in-terminating)
    * [Setting the default namespace for commands](#setting-the-default-namespace-for-commands)
    * [Dealing with broken etcd](#dealing-with-broken-etcd)
* [Vim](#vim)
    * [Quick Replace](#quick-replace)
* [Programming Languages](#programming-languages)
    * [TypeScript](#typescript)

<!-- vim-markdown-toc -->

# Introduction

This is a set of assorted documents, snippets and links I've found useful and often refer to.

# The Craft of Programming

These documents relate to the _craft_ of engineering - not how to solve specific problems, but how to _think_ about designing solutions.

- (AHA Programming 💡)[https://kentcdodds.com/blog/aha-programming/] - The dangers of DRY, the web of WET, the awesomeness of AHA.

# Kubernetes

## Set the Current Context

```sh
kubectl config use-context something
```

## Setting Cluster Credentials on the Command Line

If you don't want to create certificate files and so on and instead use fields like `certificate-authority-data`, it can be tricky to work out how to set these values from the CLI.

Here's how you do it:

```sh
K8S_CLUSTER_NAME="mycluster"
K8S_CONTEXT_NAME="mycluster"
K8S_CONTEXT_NAMESPACE="develop"
K8S_SERVER="https://whatever.com:8443"
K8S_USERNAME="pegasus-user"
K8S_CLUSTER_CERTIFICATE_AUTHORITY_DATA="<snip>"
K8S_CLUSTER_CLIENT_KEY_DATA="<snip>"
K8S_CLUSTER_TOKEN="<snip>"

# Create the cluster configuration which we can set using 'standard' commands.
kubectl config set-cluster ${K8S_CLUSTER_NAME} -server="${K8S_SERVER}"
kubectl config set-context ${K8S_CONTEXT_NAME} --user="${K8S_USERNAME}" --cluster="${CLUSTER_NAME}" --namespace="${K8S_CONTEXT_NAMESPACE}"

# Now set the credentials.
kubectl config set clusters.${CLUSTER_NAME}.certificate-authority-data "${K8S_CLUSTER_CERTIFICATE_AUTHORITY_DATA}"
kubectl config set users.${K8S_USERNAME}.client-key-data "${K8S_CLUSTER_CLIENT_KEY_DATA}"
kubectl config set users.${K8S_USERNAME}.token "${K8S_CLUSTER_TOKEN}"
```

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

# Vim

## Quick Replace

Go to the word you want to replace, then in command mode just use `Ctrl+R` `Ctrl+W` to paste the word into the command editor, e.g.

```
:%s/<now type Ctrl+R Ctrl+W>
```

This works because `CTRL-R` is used to insert a register in either command or insert mode. In command mode `CTRL-W` is the word under the cursor. Other related tricks

- `CTRL-R` + `\` - Insert the last search term
- `CTRL-R` + `a` - Insert a register named `a`
- `CTRL-R` + `=` - Insert the result of an expression (e.g. `3*78`)

More info: `:help i_CTRL-R` and `:help c_CTRL-R`.

# Programming Languages

## TypeScript

Beginner friendly and to-the-point overview of TypeScript, assuming the reader already knows JavaScript:

https://github.com/rmolinamir/typescript-cheatsheet

Other links:

- [TypeScript for JavaScript Programmers](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)
- [10 Insights from Adopting TypeScript at Scale](https://www.techatbloomberg.com/blog/10-insights-adopting-typescript-at-scale/) - very useful read for teams / projects who are looking at using TypeScript, with a particular focus on standards/consistency.
