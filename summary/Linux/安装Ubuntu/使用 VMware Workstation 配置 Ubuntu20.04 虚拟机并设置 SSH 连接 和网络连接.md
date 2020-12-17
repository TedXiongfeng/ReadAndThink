# 使用 VMware Workstation 配置 Ubuntu 20.04 server

## VMware 中创建虚拟机

选择自定义虚拟机

硬件兼容性选 Workstation 16.x 就是我当前使用的 VMware Workstation 版本

操作系统选择稍后安装

选择虚拟机的操作系统版本

然后指定虚拟机名称和存放的位置

设置虚拟机处理器配置，处理器数量乘以每个处理器内核数，只要不超过本机的Cpu线程数就行。

之后设置内存。网络类型选择 NAT 。后面的设置使用推荐或默认设置就行。

再将 dvd 设置为使用 iso 镜像文件。

## Ubuntu 安装

语言选择 English，Layout 和 Variant 使用默认的 English(US)。

ipv4 网络设置需要设置

subnet 子网，格式使用了无类别域间路由

address ip 地址，自己设置想要的地址

gateway 网关，可以自行设置地址，但是要将多处网关统一

name server 设置 DNS 服务器地址

设置 openSSH

### 将虚拟机通过本机连接网络

VMware 编辑——虚拟网络编辑器——更改配置

子网设置与 Ubuntu 相同，子网掩码 255.255.255.0 对应 ubuntu 中 地址后面 24。详细google无类别域间路由。

NAT 设置中指定网关，与 ubuntu 相同。

在控制面板的网络连接中，找到 VMnet8 属性——网络——IPV4

IP 地址自己设置，在子网的范围内就行。子网掩码和网关与前面的设置一样。DNS 服务器地址也与前面的一样。

选择现在正连接 Internet 的连接 属性——共享，将与 Internet 的连接共享给 VMnet8。



## 其他

##### 允许 root 用户远程登录

安装了 ssh 服务器后配置 sshd 文件:

```bash
sudo vim /etc/ssh/sshd_config
```

找到 PermitRootLogin 项 设置为 yes 默认为 \#PermitRootLogin prohibit-password

重启 ssh

```bash
service ssh restart
```



