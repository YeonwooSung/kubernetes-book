# K8S tools

## Retina

[repo](https://github.com/microsoft/retina)  [retina.sh](https://retina.sh/docs/installation/setup)

eBPF distributed networking observability tool for Kubernetes

## kubectl-flame

[repo](https://github.com/yahoo/kubectl-flame)

kubectl plugin to capture a flame graph of a pod's CPU profile.

### Installation

```bash
kubectl krew install flame
```

### Sample usage

```bash
# profile a Java application in pod mypod for 1 minute and save the flamegraph as /tmp/flamegraph.svg
kubectl flame mypod -t 1m --lang java -f /tmp/flamegraph.svg

# Pods that contains more than one container require specifying the target container as an argument (target langauge = Go)
kubectl flame mypod -t 1m --lang go -f /tmp/flamegraph.svg mycontainer
```
