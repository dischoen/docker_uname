# docker_uname
Provide simulated uname for builds inside of docker

This script can be used as a replacement for the builtin uname to simulate
a different kernel.
This is sufficient (at least for some of my projects) to cross-compile
projects inside of a docker container, e.g. build a driver for a 4.4.0 kernel
on a 4.15.0 docker host.

Example usage in a Dockerfile:
```
RUN mv /bin/uname /bin/uname-host
COPY uname /bin/uname
COPY uname.txt.$KERNEL_VERSION /etc/uname.txt
```
