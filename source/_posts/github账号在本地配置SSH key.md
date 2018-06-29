---
title: github账号在本地配置SSH key
date: 2017-07-22 20:43:48
tags: SSH key
categories: 技术
copyright: true
---
注意：在 windows 下，需要先下载 git bash ，安装之后再进行以下操作

#### 1.配置账户

```
$ git config --global user.name “your_username”  #设置用户名

$ git config --global user.email “your_registered_github_Email”  #设置邮箱地址(建议用注册giuhub的邮箱)
```

#### 2.检查 SSH key 是否存在

```
$ cd ~/.ssh 或cd .ssh
```
如果没有则提示： No such file or directory

如果有则进入~/.ssh路径下（ls查看当前路径文件，rm * 删除所有文件）

#### 3.如果不存在，生成新的 SSH key

```
$ cd ~  #保证当前路径在”~”下

$ ssh-keygen -t rsa -C "xxxxxx@yy.com"  #建议填写自己真实有效的邮箱地址

Generating public/private rsa key pair.

Enter file in which to save the key (/c/Users/xxxx_000/.ssh/id_rsa):   #不填直接回车

Enter passphrase (empty for no passphrase):   #输入密码（可以为空）

Enter same passphrase again:   #再次确认密码（可以为空）

Your identification has been saved in /c/Users/xxxx_000/.ssh/id_rsa.   #生成的密钥

Your public key has been saved in /c/Users/xxxx_000/.ssh/id_rsa.pub.  #生成的公钥

The key fingerprint is:

e3:51:33:xx:xx:xx:xx:xxx:61:28:83:e2:81 xxxxxx@yy.com
```
*本机已完成ssh key设置，其存放路径为：c:/Users/xxxx_000/.ssh/下。

注释：可生成ssh key自定义名称的密钥，默认id_rsa。

#### 4.添加 SSH key 到 github 站点

4.1 登录GitHub，点击右上角账号头像的“▼”→Settings→SSH kyes→Add SSH key。

4.2 复制id_rsa.pub的公钥内容

(1) 查看你本地的公钥

```
$ cat ~/.ssh/id_rsa.pub

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC0X6L1zLL4VHuvGb8aJH3ippTozmReSUzgntvk434aJ/v7kOdJ/MTyBlWXFCR+HAo3FXRitBqxiX1nKhXpHAZsMciLq8vR3c8E7CjZN733f5AL8uEYJA+YZevY5UCvEg+umT7PHghKYaJwaCxV7sjYP7Z6V79OMCEAGDNXC26IBMdMgOluQjp6o6j2KAdtRBdCDS/QIU5THQDxJ9lBXjk1fiq9tITo/aXBvjZeD+gH/Apkh/0GbO8VQLiYYmNfqqAHHeXdltORn8N7C9lOa/UW3KM7QdXo6J0GFlBVQeTE/IGqhMS5PMln3 admin@admin-PC
```

(2) 复制id_rsa.pub的公钥内容，粘贴进“Key”文本域内。 title的话，起个名字可以方便自己辨认是那一台电脑的公钥。

(3) 点击 Add key

#### 5.测试ssh连接

```
ssh -T git@github.com 

Hi username! You have successfully authenticated, but GitHub does not
provide shell access.
```
看到这个，就表示成功了。
