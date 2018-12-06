Docker网络学习

使用Docker时，发现公司局域网用的ip网段和容器设置的ip网段是同一个，导致了在容器内访问不了局域网。于是好好了解一下docker容器的网络知识。


Docker容器内的ip地址是由外部指定分配的

首先Docker容器启动时，可以使用--net指定网络

Docker Network命令


## 参考链接
<a href=[使用 Docker 容器网络](https://www.ibm.com/developerworks/cn/linux/l-docker-network/index.html)>使用 Docker 容器网络</a>