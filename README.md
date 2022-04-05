# hyposcaler-container-labs

This is currently a work in progress, and is primarily intended as a learning project for working thru workflows related to clab and ansible.

## Requirements

- Ubuntu (20.04-LTS) 
- Docker (20.10.13)  [Installation instructions](https://docs.docker.com/engine/install/)
- Containerlab (0.24.1) [Installation instructions](https://containerlab.dev/install/)
- Ansible (core 2.12.2]) [Installation instructions](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

For my personal testing I typically install on a VM running 20.04-LTS, Ubuntu 18.04-LTS may also work.

## QuickStart

### Clone the repo

```
git clone https://github.com/hyposcaler/container-labs.git
```

### Import ceos image

Note you will need to obtain the ceos-lab image from the [Support Section](https://www.arista.com/en/support/software-download) of the Arista website.  You will need an Account with Arista to do so.

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

NOTE: the default user/pass for ceos lab container is admin/admin

```
cd ansible
ansible-playbook -i inventory.yml simple-spine-leaf.yml --ask-pass
```

### Tear down lab

From the top level of the repo

```
cd clab/eos-simple-spine-leaf
sudo containerlab deploy -t ./eos-simple-spine-leaf.yml
```

