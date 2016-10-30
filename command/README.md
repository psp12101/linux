# linux
## 常用命令
![章节目录简介](http://www.denglm.com/images/backtotop.png)

### 1. 压缩或解压文件

#### 1.1 tar 压缩或解压文件

    压缩文件
    tar  -czvf  name-of-archive.tar.gz  /path/to/directory-or-file
    * -c: 创建压缩文件.
    * -z: 用 gzip 方式压缩.
    * -v: 显示压缩进度.
    * -f: 指定压缩的文件名.

    解压文件
    tar -xzvf archive.tar.gz   (gzip 格式)
    tar xvfJ filename.tar.xz   (xz 格式)

    或者解压到指定文件夹  例如 tmp
    tar -xzvf archive.tar.gz  -C /tmp

#### 1.2 zip 压缩或解压文件

    安装 unzip
    sudo apt-get install unzip
    或者
    yum install unzip

    压缩文件夹
    zip -r compressed_filename.zip foldername

    解压 zip 文件
    unzip frontend.zip

    无提示解压
    unzip -o frontend.zip

### 2. rm 删除文件夹或文件
#### 2.1 删除单个文件

    rm frontend.zip
    rm frontend.zip -f  // 强制删除

#### 2.2 删除空目录

    rmdir emptyFolder

#### 2.3 删除一个非空目录下的一切

    rm –rf nonemptyFolder

### 3. mv 移动文件或文件夹
#### 3.1 移动文件

    将 file/you/want/to/move.html 移到 文件夹 /var/www/
    mv  file/you/want/to/move.html     /var/www/

#### 3.2 移动文件夹

    mv -Ri ~/MyDirectory ~/OtherDirectory/

### 4. cp 复制文件

    从/home/levan/kdenlive/untitelds.mpg  复制到 /media/sda3/SkyDrive/
    cp -i /home/levan/kdenlive/untitelds.mpg    /media/sda3/SkyDrive/

### 5. mv 文件改名

    mv /home/user/oldname  /home/user/newname

### 6. mkdir 创建文件夹

    mkdir folderName

### 7. pwd  显示当前路径

    pwd

### 8. ifconfig 查看内网和外网 ip 地址

    ifconfig

### 9. LL 列出绝对路径下的文件

    ll    /Users/denglimin/.forever/

### 10. rsync 实现文件备份同步

    rsync，remote synchronize顾名思意就知道它是一款实现远程同步功能的软件，
    它在同步文件的同时，可以保持原来文件的权限、时间、软硬链接等附加信息。
    rsync是用 “rsync 算法”提供了一个客户机和远程文件服务器的文件同步的快速方法，
    而且可以通过ssh方式来传输文件，这样其保密性也非常好，另外它还是免费的软件。