## 一、破解并开启SSH（最困难的部分）

##### 1.R2200前：向目标服务器发送一个 JSON-RPC 请求，启动dropbear的SSH服务端。R2200前，建议参考这篇，https://phyng.com/2024/05/05/ax1800-openwrt.html 很简单，不再赘述。

##### 2.R2262版前：利用外置存储设置的一个漏洞，利用WebDAV开启SSH。

##### 3.R2262版本以上（包含R2262）：暂时需要拆机并TLL，

#### 本文重点过一遍利用WebDAV漏洞实现SSH破解的流程：

**1、外置U盘的制作**

- 将U盘制作成MBR格式，并创建两个ext4格式的分区（1个主分区，1个逻辑分区）。
- 将U盘插入到路由器，使用“京东云无线宝”启动智能加速服务。
- 弹出U盘或者移动硬盘，插入linux（最好是openWRT）中，创建两条软链接。

```
ln -s /etc/rc.local /mnt/sda5/rc.local
ln -s /etc/init.d/done  /mnt/sda5/done 
```

##### 利用到的一些素材：

- 博通VMware Workstation Pro免费下载地址：https://support.broadcom.com/
- openWRT vmware vmdk 官方下载地址：https://openwrt.org/docs/guide-user/virtualization/vmware

博主这边做好了一个openWRT的vmware虚拟机，原始的openWRT缺少一些调试的命令，在这里面已经补全。解压即可使用。

[openwrt-x64-vmware.zip](https://watermelonwater.tech/upload/openwrt-x64-vmware.zip)

**2、开启路由器的WebDAV的功能**

需要在无线宝APP端操作，通过APP将我们刚刚完成分区的主分区开通智能加速服务。

**！！！路由器必须连网才能操作，路由器连网后！！！务必！！！关闭系统自动更新的选项！！！**

[<img src="https://watermelonwater.tech/upload/image-igjc.png" alt="img" style="zoom: 33%;" />](https://watermelonwater.tech/upload/image-igjc.png)

[<img src="https://watermelonwater.tech/upload/image-qath.png" alt="img" style="zoom:33%;" />](https://watermelonwater.tech/upload/image-qath.png)

**此时我们的逻辑分区就开通WebDAV了。**

**使用Windows，添加网络位置进入WebDAV。**

[**http://192.168.68.1:56589**](http://192.168.68.1:56589/) **如果56589端口不行，换56590端口试试。**

**3、更改开机脚本，启动dropbear**

建议使用notepad++ ，这边给大家准备了最新的版本，点击可下载：[npp.8.6.6.Installer.x64.exe](https://watermelonwater.tech/upload/npp.8.6.6.Installer.x64.exe)

改开机启动的逻辑。

首先是/etc/init.d/done 解开下边三行的注释

```bash
[ -f /etc/rc.local ] && {
	sh /etc/rc.local
}
```

其次是/etc/rc.local新增dropbear启动

```bash
/usr/sbin/dropbear
```



这样的情况下，Linux系统重启后，会自动的启动我们的/usr/sbin/dropbear服务端

## 二、刷入Uboot

```bash
cd /tmp
curl -o u-boot.mbn https://watermelonwater.tech/upload/u-boot.mbn
dd if=/tmp/u-boot.mbn of=/dev/mmcblk0p13
dd if=/tmp/u-boot.mbn of=/dev/mmcblk0p14
```

进入u-boot界面：

网线接入路由器LAN口，断电，按住rest按键后，插电，大概10秒左右，红灯闪烁变成蓝灯，松开！

设置 IP 为 192.168.1.X 网关为 192.168.1.1 掩码为 255.255.255.0

访问地址：[http://192.168.1.1](http://192.168.1.1/)

## 三、选系统，刷固件

[![img](https://watermelonwater.tech/upload/image-noft.png)](https://watermelonwater.tech/upload/image-noft.png)

建议使用这个固件：[istoreos-squashfs-factory.bin](https://watermelonwater.tech/upload/istoreos-squashfs-factory.bin)

固件更新的过程大约需要1分钟，系统启动后，管理界面为 192.168.1.1 用户 root 密码 password

## 视频教程

- YouTube：https://www.youtube.com/watch?v=0iqGjrfynTc
- bilibili：https://www.bilibili.com/video/BV1tm421L7kB/

其余固件参考，我没测过，各位专家有兴趣可以试试看：

- iStoreOS：https://fw.koolcenter.com/Lean/JDC_AX1800_Pro/
- openwrt.ai：https://openwrt.ai/?target=qualcommax%2Fipq60xx&id=jdc_ax1800-pro
- koksaver：https://github.com/koksaver/OpenWrt360_6.1/
- 恩山论坛：https://www.right.com.cn/forum/thread-8366456-1-1.html

- 