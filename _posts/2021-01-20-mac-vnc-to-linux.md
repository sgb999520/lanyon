---
layout: post
title: 使用 Mac Screen shareing 共享遠端 Linux 螢幕 by VNC
---

### 如何使用 ssh 遠端登入電腦

## 兩端的電腦皆須先安裝 ssh (Linux 系統安裝 ssh)

  >Ricky:$ [sudo apt-get install ssh]()
  ```(即開始安裝 ssh)```

### VNC & Teamviewer
    

## 先於 Linux 安裝 VNC (x11vnc for ubuntu mate 16.04)

  >Ricky:$ [sudo apt-get install x11vnc]()
  ```(即開始安裝 x11vnc , 有試過 wdmycloud 無法安裝)```

  >Ricky:$ [x11vnc -storepasswd]()
  ```(設定一組密碼)```
  
  ```
  Enter VNC password:
  Verify password:
  Write password to /home/ricky/.vnc/passwd? [y]/n y
  Password written to: /home/ricky/.vnc/passwd
  ```

  >Ricky:$ [x11vnc -usepw -forever]()
  ```(啟用密碼及 Server)```

## 使用 Mac Screen shareing (Ctrl + Space : search app)

  >開啟新連結，並輸入 server IP : 192.168.1.110
  ![vnc ip](/assets/images/screen_shareing_ip.png "VNC IP")

  >接著再輸入 Linux VNC 所儲存的密碼
  ![vnc password](/assets/images/vnc_passwd.png "passwd")

## 使用 ssh 完成遠端運算

  >使用 Text editor 新增一個檔案 mv02.py:
    
    import platform
    a = 0
    for i in range(9999):
        a += i
    print("Finish job, result=%i" % a)
    print("This is", platform.system())

  (base) Ricky:mypy3 rickyhsu$ [python mv02.py]()
    
    Finish job, result=49985001
    This is Darwin

  (base) Ricky:mypy3 rickyhsu$ [ssh ricky@192.168.1.110 python3 < mv02.py]()
    
    Finish job, result=49985001
    This is Linux

```(此時可看出是分別在不同平台 Run 的)```
  
  (base) Ricky:mypy3 rickyhsu$ 

### 同時執行兩個檔案以上 -- 方法 1

(base) Ricky:mypy3 rickyhsu$ [cat a.py]()

```
#This is a.py

from b import inner_func
inner_func()
```

(base) Ricky:mypy3 rickyhsu$ nano b.py

(base) Ricky:mypy3 rickyhsu$ [cat b.py]()

```
# This is b.py

def inner_func():
    print("This is a function in b")
```

(base) Ricky:mypy3 rickyhsu$ [python a.py]()

```
This is a function in b
```

(base) Ricky:mypy3 rickyhsu$ [scp {a,b}.py ricky@192.168.1.110:~/Desktop/]()

```
a.py                                          100%   54     4.9KB/s   00:00    
b.py                                          100%   71    14.9KB/s   00:00    
```

(base) Ricky:mypy3 rickyhsu$ [ssh ricky@192.168.1.110 "python3 ~/Desktop/a.py"]()

```
This is a function in b
```

(base) Ricky:mypy3 rickyhsu$ 

## 設置網路文件共享

安裝Samba

```
sudo apt-get install samba
```

配置Samba

```
sudo pluma /etc/samba/smb.conf
```

在 smb.conf 文件尾添加：

```
[share]
comment=this is Linux share directory
path=/home/
public=yes
writable=yes
guest ok = yes
```
保存並退出
注意：在Unbuntu Mate系统中用pluma打开smb.conf，在Raspbian则用nano，即命令行输入：

```
sudo nano /etc/samba/smb.conf
```

>以下可以不用設置:

```
關閉防火墙：
 $ service iptables stop

 $ chmod 777 /home/wind
 $ chmod 777 /home/wind/smbShare
```

重新啟動 Samba 服務：
 sudo /etc/init.d/samba restart (ubuntu 17.4)
 sudo /etc/init.d/smbd restart (ubuntu 20.04)
```
sudo /etc/in
New SMB password:
Retype new SMB password:
Added user ricky.
```

ricky@ricky-desktop:~/Desktop/Shared$ 


---


