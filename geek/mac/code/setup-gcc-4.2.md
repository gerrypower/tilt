## Setup gcc-4.2 with a symbolic link

When trying to pip install a python package on OS X Yosemite, the compile of the Watchdog
dependency was failing as it could not find /usr/bin/gcc-4.2.

Resolution: Link the gcc compiler that is included with Xcode to /usr/bin/gcc-4.2.

```shell
sudo ln -nsf $(which gcc) /usr/bin/gcc-4.2
```
