___
- Linux as a software can work as switch or router.
	- Linux can have multiple interfaces like physical, virtual and bridge.
	- Linux comes with routing table for routing and firewalls for filtring.
- Below is example of creating a switch on Linux host with a bridge and two interfaces. In a bridge interface multiple network interfaces are combined into a single logical interface, allowing traffic to pass between them.
- Bridge behaves as a switch.
```bash
# Creating two dummy interfaces
sudo ip link add brtest1 type dummy
sudo ip link add brtest2 type dummy
sudo ip link set up brtest1
sudo ip link set up brtest2

# Creating bridge interface
sudo brctl addbr demobr1
sudo ip link set up demobr1
sudo ip addr add 172.16.0.1/24 dev demobr1

# Adding dummy interfaces to bridge
sudo brctl addif demobr1 brtest1 brtest2
sudo brctl show demobr1
```
![[container-networking-1.png|400]]
- When Docker is installed it creates a bridge docker0 and when new containers are added their interfaces are added to that bridge via vETH.
```bash
sudo brctl showmacs docker0
```
- **vETH** are virtual ethernet devices and are created in interconnected pairs.
```bash
# Create two veth pairs
sudo ip link add pair1-a type veth peer name pair1-b
sudo ip link add pair2-a type veth peer name pair2-b
sudo ip link set up pair1-a
sudo ip link set up pair1-b
sudo ip link set up pair2-a
sudo ip link set up pair2-b

# Add side a of veth interfaces to bridge
sudo brctl addif demobr1 pair1-a pair2-a
sudo brctl show bemobr1

# Give side b veth interfaces IP in bridge range
sudo ip addr add 172.16.0.2/24 dev pair1-b
sudo ip addr add 172.16.0.3/24 dev pair2-b
sudo brctl showmacs demobr1

# Test traffic from pair1-b to demobr1
ping 172.16.0.1/24 -I pair1-b
```
- Now we have brige setup for container but vETH is not connected to containers.

![[container-networking-2.png|400]]
- Containers use Linux namespace to create their own networking stack which includes interfaces, routes and firewalls. By default all processes share same network namespace from init process. Linux namespaces can be considered as virtual routing and forwarding (VRF) devices.
- A process in a network namespace can only see its own network stack it cannot see its parent or other processes stack.
- Now other side vETH can be added into container eth0 interface. 
```bash
# To list network namespaces
sudo lsns --type net
```

![[container-networking-3.png|400]]
- Running container in default network namespace will be able to see all host interfaces. All of container traffic will go through default network interface.
```bash
# Container in host namespace
sudo docker run --name con1 --network host ubuntu

# Container with no interface only loopback in its own namespace
sudo docker run --name con2 --network none ubuntu
```
- When container ports are mapped with host port Docker adds an entry in iptables for NAT that routes all traffic on host eht0 port to docker0 IP .
```bash
sudo docker run --con -p8000:8000 ubuntue
```
- For multi host container cluster setup we can use manual routing or a network plugin. Manual routing is a hard process so network plugins are recommended.

![[container-networking-4.png|700]]
- Calico is network plugin for container connectivity that uses BGP.

![[container-networking-5.png|700]]
- There are multiple plugin avalible for multi host container connectivity so container networking interface CNI defines a standerd that all plugins must use. Kubernertes uses CNI while docker has its own standerd that in container network model CNM. 
- Kubernetes network policies are executed by CNI plugins that uses iptables under the hood. 
___