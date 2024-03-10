___
- To add a user with `useradd` which is a low level tool.
	```
	useradd -d /home/umair -s /bin/bash umair
	passwd umair
	```
- `adduser` is fronted for `useradd` that is easy to use.
	```
	adduser umair
	```
- To delete user `userdel -r umair`.'
- To modify a user e.g modifying user shell.
	```
	usermod -s /bin/sh umair
	```
- Every user by default is a part of primary group same as username.
- To add a group:
	```
	groupadd group-name 
	```
- To show user groups:
	```
	groups umair
	```
- Files created by user are owned by user and its primary group.
- Adding primary and secondary group:
	```
	groupmod -g group-name user # adds secondary group
	groupmod -a -G group-name user # adds primary group while appending all previous groups
	```
- Querying user account in formations:
	```
	whoami
	who
	w
	pinky
	id
	last
	```
- `/etc/passwd` stores accounts information which is readable by all while `/etc/shadow` stores passwords which is readable by root only. 
- To edit `/etc/passwd` and `/etc/shadow`:
	```
	sudo vipw
	sudo vipw -s
	```

- To change user password `passwd umair`.
- System wide user profiles are stored in `/etc/bash.bashrc`, `/etc/profile`, `/etc/enviroment`.
- User profiles are stored in `/home/user/.bashrc` and `/home/user/profile`.
___
