# CoreOS-OpenStack Beginner

This contains my experiences while learning CoreOS on an OpenStack infrastructure. This project usages HEAT templates to provision multi node cluster in our infrastructure. 

Follow these commands:

```
alok@remote $ heat stack-create -f heat-template.yaml -P discovery_token_url=`curl -q https://discovery.etcd.io/new?size=3` -P public_network_uuid=87cb4819-33d4-4f2d-86d2-6970c11962da -P key_name=myoskey trycoreos
```

This provides a three machine cluster. Find ip address of control node using 
`heat output-show trycoreos control_ip`. Lets say it is `108.182.62.205`.

```
alok@remote $ export FLEETCTL_TUNNEL="108.182.62.205"
alok@remote $ fleetctl list-machines
```

```
alok@remote $ export ETCDCTL_PEERS="https://108.182.62.205:2379"
alok@remote $ etcdctl ls --recursive
alok@remote $ etcdctl set coreos/network/config “192.168.3.0/24”
alok@remote $ etcdctl ls --recursive
# too ssh to one of the machines
alok@remote $ fleetctl ssh e7d9f87f
core@core-control ~ $
```



