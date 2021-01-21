---
layout: post
title: 使用 Mac SSH 遠端登入 WDMYCLOUD
---

## WDMYCLOUD
    > ID : root
    > password : welc0me

## 使用 Mac terminal SSH 登入

  >Ricky:documents rickyhsu$ [ssh root@192.168.1.108]()
  root@192.168.1.108's password: 
  Linux Ricky-WDMyCloud 3.2.26 #1 SMP Thu Jul 9 11:14:15 PDT 2015 wd-2.4-rel armv7l
  >
  >The programs included with the Debian GNU/Linux system are free software;
  the exact distribution terms for each program are described in the
  individual files in /usr/share/doc/*/copyright.
  >
  >Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
  permitted by applicable law.
  >
  >Ricky-WDMyCloud:~#

## 使用 ssh keygen 產生 key


Ricky:.ssh rickyhsu$ ***ssh-keygen***

Generating public/private rsa key pair.
Enter file in which to save the key (/Users/rickyhsu/.ssh/id_rsa): 
<font color="red">(不輸入 file name , 則以內訂 id_rsa 為主)</font>

Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
<font color="red">(不輸入 passphrase , 則表示不需輸入密碼)</font>

Your identification has been saved in /Users/rickyhsu/.ssh/id_rsa.
Your public key has been saved in /Users/rickyhsu/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:88lRIm54Rk8k8cDs4RXQ0TQJkeRuwOBEcanPGX8AJNc rickyhsu@Ricky.local
The key's randomart image is:
```
+---[RSA 2048]----+
|     .*=OBBOo.   |
|     o ***E o.   |
|      .+=+= .    |
|      .++*.o     |
|      .oS+=.     |
|       ++=.o.    |
|          +.     |
|                 |
|                 |
+----[SHA256]-----+
```
Ricky:.ssh rickyhsu$ <font color="red">ssh-copy-id root@192.168.1.108</font>

/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/Users/rickyhsu/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@192.168.1.108's password: 
<font color="red">(第一次設定須輸入一次密碼)</font>

Number of key(s) added:        1

Now try logging into the machine, with:   "ssh 'root@192.168.1.108'"
and check to make sure that only the key(s) you wanted were added.

Ricky:.ssh rickyhsu$ ***ssh root@192.168.1.108***
<font color="red">(這裡就不用再輸入密碼了)</font>

Linux Ricky-WDMyCloud 3.2.26 #1 SMP Thu Jul 9 11:14:15 PDT 2015 wd-2.4-rel armv7l

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Ricky-WDMyCloud:~# ***exit***
logout
Connection to 192.168.1.108 closed.

Ricky:rickyhsu rickyhsu$

### 正統 SSH keygen way :

在macOS下使用ssh命令就可以連接到樹莓派：

# 注意：rpi2b是安裝系統配置時候設置的用戶名
ssh rpi2b@192.168.0.123

# 輸入密碼
配置免密登錄
在macOS生成ssh密鑰：

ssh-keygen -t  rsa # 一路按回車，生成ssh密鑰，如果以前生成過一次，無視這條命令
cat ~/.ssh/id_rsa.pub # 顯示公鑰，複製到粘貼板
在樹莓派中輸入命令生成ssh密鑰並儲存macOS的公鑰：

sudo apt-get install vim # 安裝vim
touch ~/.ssh/authorized_keys # 創建文件
vim ~/.ssh/authorized_keys # 把剛剛的公鑰粘貼進來後保存退出
chmod 600 ~/.ssh/authorized_keys # 修改權限
下次用這臺電腦遠程登錄到樹莓派就不需要輸入密碼了

---

