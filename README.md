# VPC (Virtual private cloud )

Here i'll show you demo of create a VPC in GKE cluster and then we will create subnets and firewall rules.(You should have running Project and GKE cluster in GCloud)

After cloning my github repo you will get files in proper folder.
Now you need to create a cluster then create a VPC then firewall rules of VPC and lastly subnets.

## Create a VPC

To create a VPC network give the following command(VPC name = vpc-1)

```
gcloud compute networks create vpc-1 --description "vpc-1" --subnet-mode custom
```

Now we will create a firewall rules for custom VPC subnets.

## Create Firewall rules

To create firewall rules give the following command

```
gcloud compute firewall-rules create vpc-1-fw-allow-ssh --network vpc-1 --allow tcp:22
```

Now we will create a VPC subnets.

## create a VPC subnets

Here you have to see the range (IP) of custom subnets which is located in VPC networks, so first check that and add it to command.
To create a VPC subnets gitve the following command

```
gcloud compute networks subnets create vpc-1-europe-west-2-1 --network vpc-1 --region europe-west2 --range 10.10.1.0/24
```

Now you can normlly apply your persisent volume and volume claim on GKE cluster with RWX(ReadWriteMany) access mode.
So run the pv first,

```
kubectl apply -f pv.yaml
```

Now your persistent volume is created.

Let's create a volume claim,

```
kubectl apply -f pvc.yaml
```

You will get PVC with RWX access mode.

So this is all about how you can create persistent volume and volume claim in ReadWriteMany access mode.


Thank you... :)