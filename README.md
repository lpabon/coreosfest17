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

* Follow [Deploying Quartermaster](https://github.com/coreos/quartermaster#deploying-quartermaster)
* Setup RBAC permissions for Heketi (The GlusterFS manager) by submitting the files in https://github.com/coreos/quartermaster/tree/master/examples/glusterfs/auth/rbac
* Create then submit a `StorageCluster` yaml using the [glusterfs aws example](https://github.com/coreos/quartermaster/blob/master/examples/glusterfs/aws.yaml)
* Get the storageclass name for the gluster cluster, most like it will be `gluster.qm.default`
* Edit `cockroachdb-demo.yaml` and change the storageclass value
* Submit cockroachdb-demo.yaml

### CockroachDB on VMs using GlusterFS volumes

* Follow [Deploying Quartermaster](https://github.com/coreos/quartermaster#deploying-quartermaster)
* Setup RBAC permissions for Heketi (The GlusterFS manager) by submitting the files in https://github.com/coreos/quartermaster/tree/master/examples/glusterfs/auth/rbac
* Create then submit a `StorageCluster` yaml using the [glusterfs matchbox example](https://github.com/coreos/quartermaster/blob/master/examples/glusterfs/matchbox-bootkube.yaml)
* Get the storageclass name for the gluster cluster, most like it will be `gluster.qm.default`
* Edit `cockroachdb-demo.yaml` and change the storageclass value
* Submit cockroachdb-demo.yaml

# Credits

* CockroachDB yaml comes from [Orchestrate CockroachDB with Kubernetes](https://www.cockroachlabs.com/docs/orchestrate-cockroachdb-with-kubernetes.html)
* [Quartermaster](https://github.com/coreos/quartermaster)

