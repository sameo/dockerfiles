# Running Clear Containers on Fedora

```
$ docker build -t fedora-cc .
$ docker run -ti --privileged fedora-cc bash
[root@b7112bca1772 /]# ./run_dockerd
[root@b7112bca1772 /]# docker pull busybox
[root@b7112bca1772 /]# docker run -ti busybox
```
