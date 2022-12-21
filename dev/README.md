# K8s dev enviroment

185.243.55.189

## Prerequisites

- [Microk8s](https://microk8s.io/docs/)

## Setup

### Clone this repo to your local machine

### Use VPS with Ubuntu 22.04.1 LTS

### Install microk8s

```bash
sudo snap install microk8s --classic --channel=1.26
```

Propably you will be disconnected from the SSH session. Reconnect and continue.

### Join group

```bash
sudo usermod -a -G microk8s $USER
sudo chown -f -R $USER ~/.kube
```

```bash
su - $USER
```

### Check status

```bash
microk8s status
```

If microk8s in not running then start it

```bash
microk8s start
```

### Enable addons

```bash
microk8s enable dns dashboard
```

### Enable metallb

```bash
microk8s enable metallb:{place-here-your-vps-ip}/32
```

### Use kubectl remotely (optional)

Run the following command on your remote machine

```bash
microk8s config
```

Copy the output and store it to your local machine in folder `~/.kube/` as `emleria-dev` file.

update your `KUBECONFIG` environment variable

```bash
# Linux, Mac
export KUBECONFIG=~/.kube/emleria-dev:~/.kube/config

# Windows PowerShell
$env:KUBECONFIG="~/.kube/config;~/.kube/emleria-dev"
```

Switch context on your local machine

```bash
kubectl config use-context [context-namep]
```

### Install ingress-nginix

```bash
kubectl apply -f ingress-nginx.yaml
```

After that you should see

```
404 Not Found
-------------
    nginx
```

under your vps ip address.

### Install cert-manager

```bash
kubectl apply -f cert-manager.yaml
```

### Install all dev resources

```bash
kubectl apply -f dev/
```
