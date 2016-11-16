# Running Clear Containers on Fedora

```
$ docker build -t fedora-clear-containers-devel .
$ docker run -ti --privileged fedora-clear-containers-devel
```

# Run Clear Containers with docker

```
[root@b7112bca1772 /]# docker pull busybox
[root@b7112bca1772 /]# docker run -ti busybox
```

# Build Clear Containers

```
[root@b7112bca1772 /]# cd devlp/cc-oci-runtime/
[root@b7112bca1772 /]# ./configure-cc-test
[root@b7112bca1772 /]# make
```
