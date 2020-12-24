# INSTRUCTIONS TO DEPLOY KUBEFLOW


## Create an Ubuntu VM instance through `multipass`
[Setup multipass ubuntu server instructions](multipass.md)

## Commands within the ubuntu server
```cmd 
sudo snap install microk8s --classic

mkdir $HOME/.kube

sudo usermod -a -G microk8s ubuntu
sudo chown -f -R ubuntu ~/.kube

sudo iptables -P FORWARD ACCEPT

sudo snap alias microk8s.kubectl kubectl

sudo microk8s.config > $HOME/.kube/config


exit
```

```cmd
multipass shell microk8s-vm 

microk8s.enable dns dashboard registry
microk8s.enable kubeflow --ignore-min-mem

exit
```

Check your credentials with:
```cmd
microk8s.juju config dex-auth static-username

microk8s.juju config dex-auth static-password
```
## Display kubeflow UI
```cmd 
ssh -D9999 microk8s-vm
```

Open `Firefox -> Options` and then type `proxy`. Go to `Settings` and select
`Manual proxy configuration `
- `SOCKS Host: 127.0.0.1`
- `Port: 9999`

Select also `SOCKSv5`

And also select `Proxy DNS when using SOCKS v5`


Go to http://10.64.140.43.xip.io/
