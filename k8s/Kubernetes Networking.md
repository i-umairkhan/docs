___
# Network types in Kubernetes
- Kubernetes has three type of networks.
	- Node
		- Node network provides connectivity between master and worker nodes.
		- This is outside kubernetes scope.
	- Cluster
		- Cluster network provides connectivity to services form inside and outside of cluster.
	- Pod
		- Connectivity of pods on same node and on differnet nodes.
___
# OSI Model
- OSI model provides a standerd for different computuer and telecommunicatiom systems to able to communicate with each other.

![[kubernetes-networking-1.png|600]]
![[kubernetes-networking-2.png|800]]
- Containers and VMs use virtualized version of network devices.

![[kubernetes-networking-4.png]]
___
# Container Networking
- Container use network namespaces and vETH for connectivity.
	- Network namespaces provide isolation of resources assosiated with networking.
		- Network devices
		- IP stack
		- Firewalls
		- Ports
		- vETH (Virtual Ethernet devices created in pair of connected interfaces)
- Conteiners in same network namespave talk via loopback interface.
- Containers in different namespace talk via bridge network.

![[kubernetes-networking-5.png|500]]
- Container on a different nodes/VMs can talk via swith if both are in same subnet.

![[kubernetes-networking-6.png]]
- Container on nodes haveing diffrent subnet use overlay network for connectivity.
	- Overlay network is a virtual network built on top of underlay physical network. Routing decisions are made with the help of overlay network software. 
	- Some overlay network operate at layer 2 like flannel that uses vxlan while calico operate at layer 3 using IPinIP. 

![[kubernetes-networking-7.png]]
___
# Pod Networking
- Kubernetes imposes some networking rules.
	- All pods must communicate with other pods on all nodes.
	- Agents on node can communicate with all pods on that nodes.
	- No network address translation NAT.
- Container in a same pods communicate via localhost.
- Pods on a same host communicate via brdige.
- Pods on a different hosts communicate via overlay network.
![[kubernetes-networking-8.png|800]]
___
# Container Networking Interface CNI
- CNI consists of spacifications and libraries for writing plugins to configure network interfaces in linux containers. 
- It only concernes itself only with network connectivity of containers and removing allocated resources when containers is deleted.
- It is used by Kubernetes, podman and CRI-O.
___