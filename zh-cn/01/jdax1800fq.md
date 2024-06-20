# 京东AX1800PRO路由器刷OPENWRT固件后，重新挂载大分区的方法

#### 1.格式化 mmcblk0p27 大分区

```
umount /dev/mmcblk0p27

mkfs.ext4 -F /dev/mmcblk0p27
```

#### 2.复制当前 overlay 文件到 mmcblk0p27

```
`mkdir -p /mnt/mmcblk0p27`

`mount /dev/mmcblk0p27 /mnt/mmcblk0p27`

`cp -r /overlay/* /mnt/mmcblk0p27`

`ls /mnt/mmcblk0p27`
```

#### 3.修改分区

```
block detect > /etc/config/fstab

sed -i s*#/mnt/mmcblk0p27#/overlay# /etc/config/fstab*

sed -i '12s/1/0/g' /etc/config/fstab
```

#### 4.重启启动路由器方可成功

```
reboot
```



#### **特别说明**

如果分区还是不生效还需要执行两段代码

1.编辑`/etc/rc.loca`这个文件

```
nano /etc/rc.loca
```

2.将里面的内容全部替换为：

```rc.loca
mount /dev/mmcblk0p27 /overlay
exit 0
```

3.保存退出并重启

```
reboot
```

