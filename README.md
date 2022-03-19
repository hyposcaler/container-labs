# hyposcaler-container-labs

This is currently a work in progress, and is primarily intended as a learning project for working thru workflows related to clab and ansible.

### Clone evpn repo

```
git clone https://github.com/hyposcaler/evpn-lab.git
```

### import ceos image

```
docker image import cEOS-lab-4.26.5M.tar ceos:4.26.5M
```


### Bring up evpn-lab

From the top level of the evpn-lab repo

```
cd clab
sudo containerlab deploy -t ./eos-evpn.clab.yml
```

### Configure the Devices

From the top level of the evpn-lab repo

NOTE:the default user/pass for ceos is admin/admin

```
cd ansible
ansible-playbook -i inventory.yml evpn-lab.yml --ask-pass
```

### tear down lab

From the top level of the evpn-lab repo
