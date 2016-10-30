# linux
## ssh 免密码登录
![章节目录简介](http://www.denglm.com/images/backtotop.png)

### 1.

    先在mac terminal 下执行： ssh-keygen -t rsa  如果的提示 Enter passphrase， 不要输入，直接回车

### 2.

    cd ~/.ssh    进入  ssh 文件夹  有两个文件 一个是 id_rsa (私钥) ，一个是 id_rsa.pub(公钥)

### 3.

    进入远程服务器，cd ~/.ssh    如果目录不存在，那么要自己创建mkdir -p ~/.ssh

### 4.

    有了.ssh目录后，进去，然后把id_rsa.pub传过去，可以用scp命令，这里要做的一个主要操作，
    就是将id_rsa.pub，的文件内容，写到一个叫authorized_keys的文件中去
    如果目标主机的相应用户名下已经有了.ssh目录和authorized_keys文件，
    那你操作要小心一点，可能别人也做过免登陆的设置，这个时候你要小心不要把别人的设置给覆盖了。
    如果没有的话，就创建文件touch ~/.ssh/authorized_keys，
    然后执行cat id_rsa.pub >> authorized_keys，将你的公钥写入到authorized_keys中，
    公钥文件.pub里面只有一行信息，上面的命令相当于把那一行信息追加到authorized_keys文件最后一行。
    如果.ssh目录是你主机刚刚创建的，那么可能还需要改变一下这个目录的权限，将权限放低，
    chmod -R 0600 ~/.ssh，到此，所有设置就算做完了，你可以退出登录，
    在自己的主机上试一下了，现在再敲入ssh命令后，不用密码就可以登录主机了。

### 5.

    然后：scp -r id_rsa.pub admin@114.55.238.239:/home/admin/.ssh  复制过去了，
    然后 cat id_rsa.pub >> authorized_keys




