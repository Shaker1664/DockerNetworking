## Definition

Whenever a docker container is spun up, under the hood the container configures the networking. It caters to the network namespace, virtual ethernet, and route table. Without this information, the containers will not be able to talk to each other or even connect to the internet.

## Prerequisites

- Linux image (Ubuntu preferred)
- net-tools
- basic understanding of Linux commands
- ifconfig
- ip addr
- telnet
- route
- arp

## Steps to follow

> install related network tools
> create namespaces
> create virtual ethernet (veth) cable
> connect the veth cable to the two network namespaces
> start/enable the ethernet devices of each network namespace
> assign ip addresses
> configure route tables if not configured
> ping to check if they are connected

# Install network tools

To create namespaces with this command

`sudo apt install net-tools`

# Create Namespaces

To create a network namespace we need net-tools command. Create a network namespace with the following command

```
sudo ip netns add red
sudo ip netns add green
```

Verify if the namespaces are created

`ip netns list`

The list should output like this

```
green (id: 1)
red (id: 0)
```

# Create a Virtual Ethernet cable

Create the virtual ethernet (veth) cable with

`sudo ip link add veth-red type veth peer name veth-green`

Verify the network interface list with `ip link list`

# Connect the networks with the veth cable

