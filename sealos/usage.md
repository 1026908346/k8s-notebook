# sealos

https://github.com/labring/sealos

一条命令部署kubernetes集群

## 使用

```shell
# 下载并安装sealos, sealos是个golang的二进制工具，直接下载拷贝到bin目录即可, release页面也可下载
$ wget -c https://sealyun-home.oss-cn-beijing.aliyuncs.com/sealos/latest/sealos && \
    chmod +x sealos && mv sealos /usr/bin

# 下载离线资源包
$ wget -c https://sealyun.oss-cn-beijing.aliyuncs.com/05a3db657821277f5f3b92d834bbaf98-v1.22.0/kube1.22.0.tar.gz

# 安装一个三master的kubernetes集群
$ sealos init --passwd '123456' \
	--master 192.168.0.2 \
	--pkg-url /root/kube1.22.0.tar.gz \
	--version v1.22.0
# 检查安装是否成功
$ kubectl get node -owide
```





