# Demo for CoreOS Fest 2017 talk State of State

## Setup Kubernetes
* Use [tectonic-installer](https://github.com/coreos/tectonic-installer) to
setup a Kubernetes cluster on AWS
* To setup support of GlusterFS on AWS use the following repo (Demo):

```
$ git clone -b gluster https://github.com/lpabon/tectonic-installer.git
```

* To setup local libvirt VMs use
[Matchbox/Bootkube](https://github.com/coreos/matchbox/blob/master/Documentation/bootkube.md)

## Deploy

### CockroachDB on AWS using EBS volumes

```
$ kubectl create -f storage/aws-storageclass.yaml
```

Ensure `cockroachdb-demo.yaml` points to the `aws-ebs` storage class.

```
$ kubectl create -f cockroachdb-demo.yaml
```

### CockroachDB on AWS using GlusterFS volumes

### CockroachDB on VMs using GlusterFS volumes

# Credits

* CockroachDB yaml comes from [Orchestrate CockroachDB with Kubernetes](https://www.cockroachlabs.com/docs/orchestrate-cockroachdb-with-kubernetes.html)
* [Quartermaster](https://github.com/coreos/quartermaster)

