# Create a VPC in AWS

IPv4 CIDR block: 10.10.0.0/16 [example]

# Create a Subnet in AWS

1. select vpc-id
2. select AZ
3. ipv4 CIDR block: 10.10.1.0/24

# Launch a AWS EC2 vm using VPC

select storage and AMI as previous and make sure of few important thing:

- Select the VPC that we create
- Select the subnet under the VPC
- Enable auto assign public IP

# Namespaces

Namespaces are a feature of the Linux kernel and it isolate one process from another process.

    ##    namespaces

1. Process
2. Network
3. File

## create namespaces and connect them

1. ssh to ec2 vm

```
$ ssh -i key_pair_filename ubuntu@ec2_public_IP
```

2. We can see the route table

```
$ route
```

3. to show mac address and other computers in same subnet

```
$ arp -a
```

​	4. To create a network namespace

```
$ sudo ip netns add ns1
$ sudo ip netns add ns2
```

5. to see list

```
$ sudo ip netns list
```

​	6. enter a namespace

```
$ sudo ip netns exec ns1 sh
```

​		To check its interface

​		```$ ip link```

​    7. bridge between two network namespaces

```
$ sudo ip link add veth-ns1 type veth peer name veth-ns2
```

​	8. connect namespaces using interface

```
$ sudo ip link set veth-ns1 netns ns1
$ sudo ip link set veth-ns1 netns ns2
```

 	9. To add IP address to the veth interface point

```
$ sudo ip netns exec ns1 sh
$ ip addr add [IP_ADDRESS] dev veth-ns1
```

​	10. to power up veth interface

```
$ ip link set dev veth-ns1 up
```

