https://github.com/flannel-io/flannel
___
- Each node manages a pod subent and allocates pod IPs locally.
- Pod on same node are connected via layer 2 bridge.
- Flannel uses virtual extensible LAN "VXLAN" which wraps a layer 2 ethernet packet inside a UDP packet. 
- It creates a UDP tunnel overlaying the exsisting underlying network to connect pods on different nodes.

![[flannel-cni-plugin-1.png]]
___
