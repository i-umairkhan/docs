___
# Pod creation workflow
![[Pasted image 20240504194314.png|800]]
___
# Calico 
- Calico uses dynamic subnet allocation scheme using Kubernetes API server or its own etcd cluster.
- Calico assigns each node a block of IP to assign to pods on that node.
- Default encapsulation of Calico is IP-in-IP which involves wrapping Layer 3 packet in an extra IP header.

![[Pasted image 20240504195449.png]]
- Above scheme is used when pods are communicating on different nodes.
- Calico uses Broad Gateway Protocol BGP to share and exchange routes info between nodes to facilite POD network communication.
- Every time pod is created Calico creates a route for it.
- Calico creates atunnel that provides connecticity for pods on different nodes.

![[Pasted image 20240504212236.png|800]]
___
# BGP 
- It is standarized gateway protocol designed to exchange routing and rechangeblity information among autonomus systems on internet.
- It makes routing decisions based on paths and network polices.
- It has two main functions:
	- Who on internet can i send packet to.
	- Make decision which route packet should take. Router in participating BGP piers pereodically exchange route information about what autonomus system they have direct access to.

![[Pasted image 20240505181552.png]]