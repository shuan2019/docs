# 1，进入openwrt后台

## 安装python3和PIP

打开系统——软件包——搜索python3——搜索pip——并安装

[![img](https://www.tweek.top/upload/image-lufw.png)](https://www.tweek.top/upload/image-lufw.png)

[![img](https://www.tweek.top/upload/image-jxch.png)](https://www.tweek.top/upload/image-jxch.png)

## 安装依赖requests

终端——安装依赖

```
pip install requests
```

[![img](https://www.tweek.top/upload/image-kqwv.png)](https://www.tweek.top/upload/image-kqwv.png)

# 2，代码放进root文件夹

代码地址

所有代码仓库地址：[**点击进入、附带其他系统使用方法**](https://github.com/dockkkk/api-cfcdn/)

cf官方移动延迟低于100M的ip：https://github.com/dockkkk/api-cfcdn/blob/main/345673.py (15分钟一更新)

CF官方IP:[https://github.com/dockkkk/api-cfcdn/blob/main/ymyuuubestcf.py ](https://github.com/dockkkk/api-cfcdn/blob/main/ymyuuubestcf.py)(30分钟一更新)

CF反代IP（香港）：https://github.com/dockkkk/api-cfcdn/blob/main/ymyuuuproxy.py (30分钟一更新)

放到/root文件夹

设置权限

```
chmod +x /root/*****.py
```

端口问题

非TLS = `[80, 8080, 8880, 2052, 2086, 2095, 2082]`

TLS= `[443, 8443, 2053, 2096, 2087, 2083]`

二级域名问题

# 3，运行python3 youxuan.py

检验是否成功 终端——root——密码——python3 youxuan.py

# 4,设置自动运行

查看python3路径

```
which python3
```

自定义6小时一运行代码

```
0 */6 * * * /usr/bin/python3 /root/youxuan.py
```

代码放入计划任务

### 视频教程：[点击进入YOUTUBE视频](https://youtu.be/cKf8e9M_VXQ)