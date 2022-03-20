# hyposcaler-container-labs

This is currently a work in progress, and is primarily intended as a learning project for working thru workflows related to clab and ansible.

## Requirements

- Docker (20.10.13)
- Containerlab (0.24.1)
- Ansible (core 2.12.2])

## QuickStart

### Clone the repo

```
git clone https://github.com/hyposcaler-container-labs/evpn-lab.git
```

### Import ceos image

```
docker image import cEOS-lab-4.26.5M.tar ceos:4.26.5M
```


### Bring up the eos-simple-spine-leaf lab

From the top level of the repo

```
cd clab/eos-simple-spine-leaf
sudo containerlab deploy -t ./eos-simple-spine-leaf.yml
```

### Configure the Devices

From the top level of the repo

NOTE:the default user/pass for ceos is admin/admin

```
cd ansible
ansible-playbook -i inventory.yml simple-spine-leaf.yml --ask-pass
```

### Tear down lab

From the top level of the repo
