# ETCD 

## What does ETCD do?

ETCD is a distributed key-value store that is used to store the configuration data of the cluster and the service discovery of the cluster. 
It is the core component of the kubernetes cluster. It is used to store the cluster configuration information and the state of the cluster. It is also used to store the information of the cluster serv


## Backup and Restore ETCD


### ETCDCTL 

ETCDCTL is a command-line tool that is used to interact with the ETCD cluster. It is used to backup and restore the ETCD cluster. It is also used to view the status of the ETCD cluster.

Install ETCDCTL

```bash
sudo apt-get update && sudo apt-get install -y etcd-client
```



### Backup ETCD

The following command can be used to backup the ETCD cluster:

```bash
ETCDCTL_API=3 etcdctl --endpoints=XX.XX.XX.XX \
--cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
snapshot save /tmp/snapshot-pre-boot.db
```

### Restore ETCD

The following command can be used to restore the ETCD cluster:

```bash
ETCDCTL_API=3 etcdctl --endpoints=XX.XX.XX.XX \
--cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
snapshot restore /tmp/snapshot-pre-boot.db \
--data-dir=/var/lib/etcd-from-backup \
```
