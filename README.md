# docker_uname
Provide simulated uname for builds inside of docker

This script can be used as a replacement for the builtin uname to simulate
a different kernel.
This is sufficient (at least for some of my projects) to cross-compile
projects inside of a docker container, e.g. build a driver for a 4.4.0 kernel
on a 4.15.0 docker host, if the only dependency is switching headers, libraries, etc
based on the output of `uname`.

Example usage in a Dockerfile:
```
RUN mv /bin/uname /bin/uname-host
COPY uname /bin/uname
COPY uname.txt.$KERNEL_VERSION /etc/uname.txt
```

Result:
```
$ uname -a
Linux viertervonoben 4.15.0-45-generic #48-Ubuntu SMP Tue Jan 29 16:28:13 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux

$ docker run --rm --it space/ng-4.4.0-116-generic uname -a
Linux S5build 4.4.0-116-generic #140~14.04.1-Ubuntu SMP Fri Feb 16 09:25:20 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux

$ docker run --rm -it space/ng-4.4.0-116-generic uname-host -a
Linux dba8ca452902 4.15.0-45-generic #48-Ubuntu SMP Tue Jan 29 16:28:13 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
```
