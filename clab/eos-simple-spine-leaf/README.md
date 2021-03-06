# Simple Spine Leaf Topology with cEOS devices

## Description

A simple 3-Stage folded Clos with `n=2, m=2, r=2`

All devices are running cEOS

## Diagrams

![Clos Network with n=2, m=2, r=2](docs/eos-simple-spine-leaf.jpeg)

### Graphviz

```dot
graph N {
    {
        Node[shape=box]
        Leaf1
        Leaf2
        Leaf3
        Leaf4
        Spine1
        Spine2
        Host1
        Host2
        Host3
        Host4
    }
    ordering="out"
    rank = same; Leaf1; Leaf2; Leaf3; Leaf4;
    rank = same; Spine1; Spine2;
    rank = same; Host1; Host2; Host3; Host4;
    Spine1 -- {Leaf1,Leaf2,Leaf3,Leaf4}
    Spine2 -- {Leaf1,Leaf2,Leaf3,Leaf4}
    Leaf1 -- Host1
    Leaf2 -- Host2
    Leaf3 -- Host3
    Leaf4 -- Host4
}
```


## Addressing 

The Ansible directory of this repo has a simple-spine-leaf role for configuring this lab.  Using this role will result in the following addressing.

- All hosts addresses are of the form `10.100.10${hostID}.10` 
    - as an example host1 has the ip address `10.100.101.10`
- All leaf loopback addresses are of the form `192.168.101.${leafID}` 
    - as an example lo0 of leaf1 has the ip address `192.168.100.1`
- All spine loopback addresses are of the form `192.168.100.${spineID}` 
    - as an example lo0 of spine1 has the ip address `192.168.101.1`
- The mgmt interface addresses for the spines are of the form `172.20.20.10${spineID}` 
    - as an example mgmt interface of spine1 has the ip address `172.20.20.101`
- The mgmt interface addressses for the leafs are of the form `172.20.20.1${spineID}` 
    - as an example mgmt interface of leaf1 has the ip address `172.20.20.11`
- The mgmt interface addresses for the hosts are of the form `172.20.20.20${hostID}` 
    - as an example mgmt interface of host1 has the ip address `172.20.20.21`

- All spine <-> leaf ptps are addressed from within `10.10.10.0/24`
    - spine1 `10.10.10.0/31` <-> leaf1 `10.10.10.1/31`
    - spine1 `10.10.10.2/31` <-> leaf2 `10.10.10.3/31`
    - spine1 `10.10.10.4/31` <-> leaf3 `10.10.10.5/31`
    - spine1 `10.10.10.6/31` <-> leaf4 `10.10.10.7/31`
    - spine2 `10.10.10.8/31` <-> leaf1 `10.10.10.9/31`
    - spine2 `10.10.10.10/31` <-> leaf2 `10.10.10.11/31`
    - spine2 `10.10.10.12/31` <-> leaf3 `10.10.10.13/31`
    - spine2 `10.10.10.14/31` <-> leaf4 `10.10.10.15/31`

## BGP

- BGP AS used for leafs take the form of `6452${leafID}`
  - as an example leaf1 is in the as `64521`
- BGP AS used for all spines is `65500`
    - note there is no iBGP between spines
- All loopbacks and ptp subnets are advertised via network statements
