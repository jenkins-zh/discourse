> [discourse](https://github.com/discourse/discourse) 是一个比较受欢迎的开源论坛，[Jenkins 中文社区](https://jenkins-zh.cn) 的论坛决定使用 discourse 进行部署。
在此将部署安装过程记录一下。

## 准备安装环境
基础环境为 Ubuntu 18.04，需要预先安装 ruby、redis、postgresql、docker 等环境
```
# sudo apt-cache search ruby
# apt-get upgrade
# apt-get update 
# apt-get upgrade 
# apt-cache search ruby
# apt-get install ruby
# ruby -v
# apt-get install postgresql
# wget -qO- https://get.docker.com/ | sh
# wget http://download.redis.io/releases/redis-3.2.6.tar.gz
# tar xzf redis-3.2.6.tar.gz
# cd redis-3.2.6
# make
# make install
```


当前是在阿里云服务器上进行部署，当前主机仅有2G内存，阿里默认不分配swap，资源不够用，固为虚机分配2G虚拟内存
```
free -m
mkdir /opt/images/
rm -rf /opt/images/swap
dd if=/dev/zero of=/opt/images/swap bs=1024 count=2048000
mkswap /opt/images/swap
swapon /opt/images/swap
free -m
```

安装redis时，[遇到问题](https://blog.csdn.net/galaxiansheng/article/details/100657139)
到此，预安装环境准备就绪

## 部署 discourse
参照[官方步骤](https://github.com/discourse/discourse/blob/master/docs/INSTALL-cloud.md)