___
- To check IP of machine `ifconfig` and `ip addr`.
- To check route table `ip route`.
- DNS is used to convert domain names to actual IPs.
- `ping` is a basic tool to test DNS.
- Other DNS troubleshooting tools:
	- `dig @server host`.
	- `nslookup host server`.
	- `host host server`.
- `/etc/hosts` is where DNS records are stored locally.
- `hosts` key in `/etc/nsswitch.conf` contains entries in priority where DNS looks up. 
- `/etc/resolv.conf` contains entries for name servers. It is handled by network manager and not recommended to edit directly.
- To manage interfaces:
	- `/etc/network/interfaces`.
	- `/etc/netplan/*`
	- Or using network manager `nmtui`. 
	- On Red hat systems `/etc/sysconfig/network-scripts` is place where all interface files are placed. 
___
