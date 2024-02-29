___
- To install tar balls:
	```
	tar -zxvf my-tarball.tar.gz
	cd my-tarball
	make 
	```
- To install deb packages used for Debian based distributions:
	- `apt` can be used to install deb packages from remote repositories.
	- `aptitute` and `apt-get` can also be used but they are older.
	- `dpkg` is used to install packages from deb files. But it will resolve any dependencies. It is low level tool used by other package managers.
	```
	sudo dpkg -i my-package.deb
	sudo apt install my-package
	```
- To install rpm packages used for Red hat distributions:
	- `rpm` can be used to install packages but it is low level and do not resolve any dependencies.
	- `dnf` and `yum` can be used to install rpm packages from remote repositories.
	```
	rpm -i my-package.rpm
	yum install my-package
	```
- Adding repositories for apt:
	- `/etc/apt/souces.list` to add repositories.
	- `apt-key-add` can be used to add GPG keys.
	- `apt-key-list` to list keys.
	- For community repositories `apt-add-repository ppa:repo`.
- Adding repositories for rpm:
	- `/etc/yum.conf` is used for yum configuration and repositories can be added their as well in `/etc/yum/conf.d/app.repo`.
___
