---
title: "Linode"
date: 2017-11-17T19:11:17+02:00
draft: true
---

# Setting up my environment

1. Created the instance (Debian9)
2. Remote connect and install:

```bash
apt-get update && apt-get upgrade
apt-get install neovim unattended-upgrades 
```

## Linode

[Guide](https://www.linode.com/docs/security/securing-your-server) from Linode is pretty good:
1. User
2. Unattended Upgrades
3. Fail2Ban
4. SSHD: no root, disable password authentication, etc...

## Caddy

1. Custom build
2. Install support tooling on host:

```bash
sudo apt-get install git libcap2-bin

go get github.com/kardianos/govendor
govendor get github.com/gohugoio/hugo
go install github.com/gohugoio/hugo
```

3. Set ENV for:
    - vwjXoiMjMQjIHOMs5mm3V4IdRS1TECuSBd7sseMBzHrCZ9wu0e1RiwEdmRT73lkq 

4. `sudo setcap 'p_net_bind_service=+ep' ./caddy

### TODO
- [iptables](https://www.linode.com/docs/security/firewalls/control-network-traffic-with-iptables)
