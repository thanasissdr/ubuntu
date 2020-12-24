# Multipass
1. Install multipass
2. > Make sure that `multipassd.exe, multipass.exe, svchost.exe` are in the firewall exception list, otherwise there might be problems when trying to log into the instance.
```cmd
multipass launch 18.04 --name microk8s-vm --mem 8G --cpus 3 --disk 50G
```

Make sure that the instance has a proper `IPv4` address when 
```cmd
multipass list
```

By default the location where the instances are saved is:
`C:\Windows\System32\config\systemprofile\AppData\Roaming\multipassd\vault`
## Connection
```cmd
multipass shell microk8s
```

## Connection through `ssh`

```cmd
ssh-keygen
```

**Server**
```cmd
sudo chmod 700 ~/.ssh
sudo chmod 700 ~/.ssh/authorized_keys
```
 
**Client**

- Copy the conntents of the corresponding `.pub` file from the client to the server under `~/.ssh/authorized_keys`
- Create a `config` file under `~/.ssh/` and put the following (example):  

```
Host microk8s-vm-server # Friendly host name
HostName 172.18.42.97
IdentityFile ~/.ssh/id_rsa # private key
User ubuntu
```

### Connect through ssh
```
ssh -i ~/.ssh/id_rsa ubuntu@172.18.42.97
```
or
```
ssh microk8s-vm-server
```