# git ssh key创建

## SSH配置如下：

### 一 、设置Git的user name和email：

- `$ git config --global user.name "你的名字/your name"`

```
--global user.name "Dwight"
```


- `$ git config --global user.email "你的邮箱/your email"`


```
--global user.email "958689927@qq.com"
```


### 二、生成SSH密钥过程：

1. 查看是否已经有了ssh密钥：

```
cd ~/.ssh`
```

如果没有密钥则不会有此文件夹，有则备份删除
2. 生存密钥：

```
$ ssh-keygen -t rsa -C "你的邮箱/your email"
```


3. 按3个回车，密码为空。

4. 在终端中显示以下描述，表示已经生产ssh key 成功；

```
Your identification has been saved in /home/tekkub/.ssh/id_rsa.
Your public key has been saved in /home/tekkub/.ssh/id_rsa.pub.
The key fingerprint is:
...
The key's randomart image is:
+---[RSA 2048]----+
|    .. ssoo o.   |
|    .o .=o.o     |
|.  .+s.+oo       |
|E o .o=+  .      |
| o . .s.S.       |
|  . .  . .. .    |
|oo .... .ooo     |
|O-ooo.     oo    |
|aB=o.     .. .   |
+----[SHA256]-----+
```


5. 最后得到了两个文件：id_rsa和id_rsa.pub

6. 添加密钥到ssh：ssh-add 文件名
需要之前输入密码。
4.在github上添加ssh密钥，这要添加的是“id_rsa.pub”里面的公钥。
或者 打开“id_rsa.pub” 复制内容到
