# 第 3 章 基础命令

[返回](./README.md)

菜鸟教程： https://www.runoob.com/w3cnote/linux-common-command.html

## 系统信息

```
arch 显示机器的处理器架构(1)
uname -m 显示机器的处理器架构(2)
uname -r 显示正在使用的内核版本
dmidecode -q 显示硬件系统部件 - (SMBIOS / DMI)
hdparm -i /dev/hda 罗列一个磁盘的架构特性
hdparm -tT /dev/sda 在磁盘上执行测试性读取操作
cat /proc/cpuinfo 显示CPU info的信息
cat /proc/interrupts 显示中断
cat /proc/meminfo 校验内存使用
cat /proc/swaps 显示哪些swap被使用
cat /proc/version 显示内核的版本
cat /proc/net/dev 显示网络适配器及统计
cat /proc/mounts 显示已加载的文件系统
lspci -tv 罗列 PCI 设备
lsusb -tv 显示 USB 设备
date 显示系统日期
cal 2007 显示2007年的日历表
date 041217002007.00 设置日期和时间 - 月日时分年.秒
clock -w 将时间修改保存到 BIOS
```

## 关机 (系统的关机、重启以及登出 )

```
shutdown -h now 关闭系统(1)
init 0 关闭系统(2)
telinit 0 关闭系统(3)
shutdown -h hours:minutes & 按预定时间关闭系统
shutdown -c 取消按预定时间关闭系统
shutdown -r now 重启(1)
reboot 重启(2)
logout 注销
```

## 文件和目录

```
cd /home 进入 '/ home' 目录'
cd .. 返回上一级目录
cd ../.. 返回上两级目录
cd 进入个人的主目录
cd ~user1 进入个人的主目录
cd - 返回上次所在的目录
pwd 显示工作路径
ls 查看目录中的文件
ls -F 查看目录中的文件
ls -l 显示文件和目录的详细资料
ls -a 显示隐藏文件
ls *[0-9]* 显示包含数字的文件名和目录名
tree 显示文件和目录由根目录开始的树形结构(1)
lstree 显示文件和目录由根目录开始的树形结构(2)
mkdir dir1 创建一个叫做 'dir1' 的目录'
mkdir dir1 dir2 同时创建两个目录
mkdir -p /tmp/dir1/dir2 创建一个目录树
rm -f file1 删除一个叫做 'file1' 的文件'
rmdir dir1 删除一个叫做 'dir1' 的目录'
rm -rf dir1 删除一个叫做 'dir1' 的目录并同时删除其内容
rm -rf dir1 dir2 同时删除两个目录及它们的内容
mv dir1 new_dir 重命名/移动 一个目录
cp file1 file2 复制一个文件
cp dir/* . 复制一个目录下的所有文件到当前工作目录
cp -a /tmp/dir1 . 复制一个目录到当前工作目录
cp -a dir1 dir2 复制一个目录
ln -s file1 lnk1 创建一个指向文件或目录的软链接
ln file1 lnk1 创建一个指向文件或目录的物理链接
touch -t 0712250000 file1 修改一个文件或目录的时间戳 - (YYMMDDhhmm)
file file1 outputs the mime type of the file as text
iconv -l 列出已知的编码
iconv -f fromEncoding -t toEncoding inputFile > outputFile creates a new from the given input file by assuming it is encoded in fromEncoding and converting it to toEncoding.
find . -maxdepth 1 -name *.jpg -print -exec convert "{}" -resize 80x60 "thumbs/{}" \; batch resize files in the current directory and send them to a thumbnails directory (requires convert from Imagemagick)
```

## 文件搜索

```
find / -name file1 从 '/' 开始进入根文件系统搜索文件和目录
find / -user user1 搜索属于用户 'user1' 的文件和目录
find /home/user1 -name \*.bin 在目录 '/ home/user1' 中搜索带有'.bin' 结尾的文件
find /usr/bin -type f -atime +100 搜索在过去100天内未被使用过的执行文件
find /usr/bin -type f -mtime -10 搜索在10天内被创建或者修改过的文件
find / -name \*.rpm -exec chmod 755 '{}' \; 搜索以 '.rpm' 结尾的文件并定义其权限
find / -xdev -name \*.rpm 搜索以 '.rpm' 结尾的文件，忽略光驱、捷盘等可移动设备
locate \*.ps 寻找以 '.ps' 结尾的文件 - 先运行 'updatedb' 命令
whereis halt 显示一个二进制文件、源码或man的位置
which halt 显示一个二进制文件或可执行文件的完整路径
```

## 磁盘空间

```
df -h 显示已经挂载的分区列表
ls -lSr |more 以尺寸大小排列文件和目录
du -sh dir1 估算目录 'dir1' 已经使用的磁盘空间'
du -sk * | sort -rn 以容量大小为依据依次显示文件和目录的大小
```

## 用户和群组

```
adduser
groupadd group_name 创建一个新用户组
groupdel group_name 删除一个用户组
groupmod -n new_group_name old_group_name 重命名一个用户组
useradd -c "Name Surname " -g admin -d /home/user1 -s /bin/bash user1 创建一个属于 "admin" 用户组的用户
useradd user1 创建一个新用户
userdel -r user1 删除一个用户 ( '-r' 排除主目录)
usermod -c "User FTP" -g system -d /ftp/user1 -s /bin/nologin user1 修改用户属性
passwd 修改口令
passwd user1 修改一个用户的口令 (只允许root执行)
chage -E 2005-12-31 user1 设置用户口令的失效期限
pwck 检查 '/etc/passwd' 的文件格式和语法修正以及存在的用户
grpck 检查 '/etc/passwd' 的文件格式和语法修正以及存在的群组
newgrp group_name 登陆进一个新的群组以改变新创建文件的预设群组
```

## 文件的权限 - 使用 "+" 设置权限，使用 "-" 用于取消

```
ls -lh 显示权限
ls /tmp | pr -T5 -W$COLUMNS 将终端划分成5栏显示
chmod ugo+rwx directory1 设置目录的所有人(u)、群组(g)以及其他人(o)以读（r ）、写(w)和执行(x)的权限
chmod go-rwx directory1 删除群组(g)与其他人(o)对目录的读写执行权限
chown user1 file1 改变一个文件的所有人属性
chown -R user1 directory1 改变一个目录的所有人属性并同时改变改目录下所有文件的属性
chgrp group1 file1 改变文件的群组
chown user1:group1 file1 改变一个文件的所有人和群组属性
find / -perm -u+s 罗列一个系统中所有使用了SUID控制的文件
chmod u+s /bin/file1 设置一个二进制文件的 SUID 位 - 运行该文件的用户也被赋予和所有者同样的权限
chmod u-s /bin/file1 禁用一个二进制文件的 SUID位
chmod g+s /home/public 设置一个目录的SGID 位 - 类似SUID ，不过这是针对目录的
chmod g-s /home/public 禁用一个目录的 SGID 位
chmod o+t /home/public 设置一个文件的 STIKY 位 - 只允许合法所有人删除文件
chmod o-t /home/public 禁用一个目录的 STIKY 位
```

## 文件的特殊属性 - 使用 "+" 设置权限，使用 "-" 用于取消

```
chattr +a file1 只允许以追加方式读写文件
chattr +c file1 允许这个文件能被内核自动压缩/解压
chattr +d file1 在进行文件系统备份时，dump程序将忽略这个文件
chattr +i file1 设置成不可变的文件，不能被删除、修改、重命名或者链接
chattr +s file1 允许一个文件被安全地删除
chattr +S file1 一旦应用程序对这个文件执行了写操作，使系统立刻把修改的结果写到磁盘
chattr +u file1 若文件被删除，系统会允许你在以后恢复这个被删除的文件
lsattr 显示特殊的属性
chattr +a file1 只允许以追加方式读写文件
chattr +c file1 允许这个文件能被内核自动压缩/解压
chattr +d file1 在进行文件系统备份时，dump程序将忽略这个文件
chattr +i file1 设置成不可变的文件，不能被删除、修改、重命名或者链接
chattr +s file1 允许一个文件被安全地删除
chattr +S file1 一旦应用程序对这个文件执行了写操作，使系统立刻把修改的结果写到磁盘
chattr +u file1 若文件被删除，系统会允许你在以后恢复这个被删除的文件
lsattr 显示特殊的属性
```

## 打包和压缩文件

```
bunzip2 file1.bz2 解压一个叫做 'file1.bz2'的文件
bzip2 file1 压缩一个叫做 'file1' 的文件
gunzip file1.gz 解压一个叫做 'file1.gz'的文件
gzip file1 压缩一个叫做 'file1'的文件
gzip -9 file1 最大程度压缩
rar a file1.rar test_file 创建一个叫做 'file1.rar' 的包
rar a file1.rar file1 file2 dir1 同时压缩 'file1', 'file2' 以及目录 'dir1'
rar x file1.rar 解压rar包
unrar x file1.rar 解压rar包
tar -cvf archive.tar file1 创建一个非压缩的 tarball
tar -cvf archive.tar file1 file2 dir1 创建一个包含了 'file1', 'file2' 以及 'dir1'的档案文件
tar -tf archive.tar 显示一个包中的内容
tar -xvf archive.tar 释放一个包
tar -xvf archive.tar -C /tmp 将压缩包释放到 /tmp目录下
tar -cvfj archive.tar.bz2 dir1 创建一个bzip2格式的压缩包
tar -xvfj archive.tar.bz2 解压一个bzip2格式的压缩包
tar -cvfz archive.tar.gz dir1 创建一个gzip格式的压缩包
tar -xvfz archive.tar.gz 解压一个gzip格式的压缩包
zip file1.zip file1 创建一个zip格式的压缩包
zip -r file1.zip file1 file2 dir1 将几个文件和目录同时压缩成一个zip格式的压缩包
unzip file1.zip 解压一个zip格式压缩包
```

## DEB 包 (Debian, Ubuntu 以及类似系统)

```
dpkg -i package.deb 安装/更新一个 deb 包
dpkg -r package_name 从系统删除一个 deb 包
dpkg -l 显示系统中所有已经安装的 deb 包
dpkg -l | grep httpd 显示所有名称中包含 "httpd" 字样的deb包
dpkg -s package_name 获得已经安装在系统中一个特殊包的信息
dpkg -L package_name 显示系统中已经安装的一个deb包所提供的文件列表
dpkg --contents package.deb 显示尚未安装的一个包所提供的文件列表
dpkg -S /bin/ping 确认所给的文件由哪个deb包提供
```

## APT 软件工具 (Debian, Ubuntu 以及类似系统)

```
apt-get install package_name 安装/更新一个 deb 包
apt-cdrom install package_name 从光盘安装/更新一个 deb 包
apt-get update 升级列表中的软件包
apt-get upgrade 升级所有已安装的软件
apt-get remove package_name 从系统删除一个deb包
apt-get check 确认依赖的软件仓库正确
apt-get clean 从下载的软件包中清理缓存
apt-cache search searched-package 返回包含所要搜索字符串的软件包名称
```

## 查看文件内容

```
cat file1 从第一个字节开始正向查看文件的内容
tac file1 从最后一行开始反向查看一个文件的内容
more file1 查看一个长文件的内容
less file1 类似于 'more' 命令，但是它允许在文件中和正向操作一样的反向操作
head -2 file1 查看一个文件的前两行
tail -2 file1 查看一个文件的最后两行
tail -f /var/log/messages 实时查看被添加到一个文件中的内容
```

## 文本处理

```
cat file1 file2 ... | command <> file1_in.txt_or_file1_out.txt general syntax for text manipulation using PIPE, STDIN and STDOUT
cat file1 | command( sed, grep, awk, grep, etc...) > result.txt 合并一个文件的详细说明文本，并将简介写入一个新文件中
cat file1 | command( sed, grep, awk, grep, etc...) >> result.txt 合并一个文件的详细说明文本，并将简介写入一个已有的文件中
grep Aug /var/log/messages 在文件 '/var/log/messages'中查找关键词"Aug"
grep ^Aug /var/log/messages 在文件 '/var/log/messages'中查找以"Aug"开始的词汇
grep [0-9] /var/log/messages 选择 '/var/log/messages' 文件中所有包含数字的行
grep Aug -R /var/log/* 在目录 '/var/log' 及随后的目录中搜索字符串"Aug"
sed 's/stringa1/stringa2/g' example.txt 将example.txt文件中的 "string1" 替换成 "string2"
sed '/^$/d' example.txt 从example.txt文件中删除所有空白行
sed '/ *#/d; /^$/d' example.txt 从example.txt文件中删除所有注释和空白行
echo 'esempio' | tr '[:lower:]' '[:upper:]' 合并上下单元格内容
sed -e '1d' result.txt 从文件example.txt 中排除第一行
sed -n '/stringa1/p' 查看只包含词汇 "string1"的行
sed -e 's/ *$//' example.txt 删除每一行最后的空白字符
sed -e 's/stringa1//g' example.txt 从文档中只删除词汇 "string1" 并保留剩余全部
sed -n '1,5p;5q' example.txt 查看从第一行到第5行内容
sed -n '5p;5q' example.txt 查看第5行
sed -e 's/00*/0/g' example.txt 用单个零替换多个零
cat -n file1 标示文件的行数
cat example.txt | awk 'NR%2==1' 删除example.txt文件中的所有偶数行
echo a b c | awk '{print $1}' 查看一行第一栏
echo a b c | awk '{print $1,$3}' 查看一行的第一和第三栏
paste file1 file2 合并两个文件或两栏的内容
paste -d '+' file1 file2 合并两个文件或两栏的内容，中间用"+"区分
sort file1 file2 排序两个文件的内容
sort file1 file2 | uniq 取出两个文件的并集(重复的行只保留一份)
sort file1 file2 | uniq -u 删除交集，留下其他的行
sort file1 file2 | uniq -d 取出两个文件的交集(只留下同时存在于两个文件中的文件)
comm -1 file1 file2 比较两个文件的内容只删除 'file1' 所包含的内容
comm -2 file1 file2 比较两个文件的内容只删除 'file2' 所包含的内容
comm -3 file1 file2 比较两个文件的内容只删除两个文件共有的部分
```

## 备份

```
dump -0aj -f /tmp/home0.bak /home 制作一个 '/home' 目录的完整备份
dump -1aj -f /tmp/home0.bak /home 制作一个 '/home' 目录的交互式备份
restore -if /tmp/home0.bak 还原一个交互式备份
rsync -rogpav --delete /home /tmp 同步两边的目录
rsync -rogpav -e ssh --delete /home ip_address:/tmp 通过SSH通道rsync
rsync -az -e ssh --delete ip_addr:/home/public /home/local 通过ssh和压缩将一个远程目录同步到本地目录
rsync -az -e ssh --delete /home/local ip_addr:/home/public 通过ssh和压缩将本地目录同步到远程目录
dd bs=1M if=/dev/hda | gzip | ssh user@ip_addr 'dd of=hda.gz' 通过ssh在远程主机上执行一次备份本地磁盘的操作
dd if=/dev/sda of=/tmp/file1 备份磁盘内容到一个文件
tar -Puf backup.tar /home/user 执行一次对 '/home/user' 目录的交互式备份操作
( cd /tmp/local/ && tar c . ) | ssh -C user@ip_addr 'cd /home/share/ && tar x -p' 通过ssh在远程目录中复制一个目录内容
( tar c /home ) | ssh -C user@ip_addr 'cd /home/backup-home && tar x -p' 通过ssh在远程目录中复制一个本地目录
tar cf - . | (cd /tmp/backup ; tar xf - ) 本地将一个目录复制到另一个地方，保留原有权限及链接
find /home/user1 -name '*.txt' | xargs cp -av --target-directory=/home/backup/ --parents 从一个目录查找并复制所有以 '.txt' 结尾的文件到另一个目录
find /var/log -name '*.log' | tar cv --files-from=- | bzip2 > log.tar.bz2 查找所有以 '.log' 结尾的文件并做成一个bzip包
dd if=/dev/hda of=/dev/fd0 bs=512 count=1 做一个将 MBR (Master Boot Record)内容复制到软盘的动作
dd if=/dev/fd0 of=/dev/hda bs=512 count=1 从已经保存到软盘的备份中恢复MBR内容
```

## 网络 - （以太网和 WIFI 无线）

```
ifconfig eth0 显示一个以太网卡的配置
ifup eth0 启用一个 'eth0' 网络设备
ifdown eth0 禁用一个 'eth0' 网络设备
ifconfig eth0 192.168.1.1 netmask 255.255.255.0 控制IP地址
ifconfig eth0 promisc 设置 'eth0' 成混杂模式以嗅探数据包 (sniffing)
dhclient eth0 以dhcp模式启用 'eth0'
route -n show routing table
route add -net 0/0 gw IP_Gateway configura default gateway
route add -net 192.168.0.0 netmask 255.255.0.0 gw 192.168.1.1 configure static route to reach network '192.168.0.0/16'
route del 0/0 gw IP_gateway remove static route
echo "1" > /proc/sys/net/ipv4/ip_forward activate ip routing
hostname show hostname of system
host www.example.com lookup hostname to resolve name to ip address and viceversa(1)
nslookup www.example.com lookup hostname to resolve name to ip address and viceversa(2)
ip link show show link status of all interfaces
mii-tool eth0 show link status of 'eth0'
ethtool eth0 show statistics of network card 'eth0'
netstat -tup show all active network connections and their PID
netstat -tupl show all network services listening on the system and their PID
tcpdump tcp port 80 show all HTTP traffic
iwlist scan show wireless networks
iwconfig eth1 show configuration of a wireless network card
hostname show hostname
host www.example.com lookup hostname to resolve name to ip address and viceversa
nslookup www.example.com lookup hostname to resolve name to ip address and viceversa
whois www.example.com lookup on Whois database
```

## 软件

### Git

Pro Git （Git 教程） https://git-scm.com/book/zh/v2

### Vim

![键盘布局图](../public/vi-vim-cheat-sheet-sch1.gif)

## 命令大全

记不清的时候，可以到这里查询

链接地址； https://www.runoob.com/linux/linux-command-manual.html

## 常用命令全拼

辅助记忆命令

链接地址： https://www.runoob.com/w3cnote/linux-command-full-fight.html

## 练习题

### 基础练习题

1. 查看当前工作目录

问题：如何查看你当前所在的目录？

2. 列出目录内容

问题：如何列出当前目录下的所有文件和文件夹？

3. 创建一个新目录

问题：如何在当前目录下创建一个名为 new_folder 的新目录？

4. 改变当前工作目录

问题：如何改变当前工作目录到/home 目录？

5. 创建一个新文件

问题：如何在当前目录下创建一个名为 test_file.txt 的空文件？

6. 复制文件

问题：如何将 test_file.txt 复制到 new_folder 目录下？

7. 移动文件

问题：如何将 new_folder 目录下的 test_file.txt 移动到当前目录？

8. 删除文件

问题：如何删除名为 test_file.txt 的文件？

9. 写入文件

问题：如何向 test_file.txt 文件中写入文本“Hello, Ubuntu!”？

10. 查看文件内容

问题：如何查看 test_file.txt 文件的内容？

11. 查找文件

问题：如何在当前目录及其子目录中查找名为 test_file.txt 的文件？

12. 查看历史命令

问题：如何查看你之前使用过的命令历史？

13. 查看磁盘使用情况

问题：如何查看当前系统的磁盘使用情况？

14. 查看进程

问题：如何查看当前运行的所有进程？

15. 杀死进程

问题：如果一个进程的 PID 是 1234，你如何杀死这个进程？

16. 改变文件权限

问题：如何将 test_file.txt 的权限设置为所有人都可以读写执行？

17. 查看系统信息

问题：如何查看你的 Ubuntu 系统的详细信息，包括版本号？

18. 查看网络配置

问题：如何查看当前系统的网络配置信息？

19. 使用 grep 命令

问题：如何在 test_file.txt 中搜索包含“Ubuntu”的行？

20. 压缩和解压文件

问题：如何将名为 new_folder 的目录压缩成 new_folder.tar.gz？又如何解压这个文件？

### 提高一点儿难度的练习题

1. 查找并排序文件

问题：如何找到/var/log 目录下所有.log 文件，并按大小排序显示？

2. 监控实时日志文件更新

问题：如何实时监控/var/log/syslog 文件的更新？

3. 使用 find 命令执行操作

问题：如何找到/home 目录下所有.txt 文件，并删除它们？

4. 批量重命名文件

问题：如何将当前目录下所有.txt 文件批量重命名为.text 文件？

5. 查看端口使用情况

问题：如何查看哪个进程在使用 80 端口？

6. 使用 crontab 设置计划任务

问题：如何设置一个每天早上 6 点自动备份/home 目录到/backup 的计划任务？

7. 查找大文件

问题：如何查找/目录下所有大于 100MB 的文件？

8. 查看命令输出的尾部

问题：如何查看/var/log/syslog 文件的最后 20 行？

9. 使用 awk 处理文本

问题：如何使用 awk 命令从/etc/passwd 中提取所有用户名？

10. 修改文件所有者

问题：如何将/data 目录及其子目录下所有文件的所有者更改为用户 tom？

11. 链接库管理

问题：如何查看某个特定程序依赖哪些共享库？

12. 查找并替换文本

问题：如何在/var/www/html/index.html 文件中查找“Welcome”并替换为“Welcome to Our Website”？

13. 压缩多个目录

问题：如何将/logs 和/backup 两个目录压缩成一个名为 archives.tar.gz 的文件？

14. 分割和合并文件

问题：如何将一个大文件 bigfile.iso 分割成多个 100MB 的小文件，并在需要时重新合并它们？

15. 使用 sed 命令

问题：如何使用 sed 命令删除 test_file.txt 中的所有空白行？

16. 网络流量监控

问题：如何监控 Ubuntu 服务器的实时网络流量？

17. 查找特定用户运行的进程

问题：如何查找由用户 alice 运行的所有进程？

18. 备份和还原 MySQL 数据库

问题：如何备份名为 mydb 的 MySQL 数据库到 mydb_backup.sql 文件，并如何从该备份文件恢复数据库？

19. 批量修改文件权限

问题：如何将当前目录下所有.sh 文件的执行权限赋予所有用户？

20. 使用 diff 比较文件差异

问题：如何比较两个配置文件 config_old.txt 和 config_new.txt 的差异？

### 练习题答案

基础命令练习题答案

1. `pwd`
2. `ls -la`
3. `mkdir new_folder`
4. `cd /home`
5. `touch test_file.txt`
6. `cp test_file.txt new_folder/`
7. `mv new_folder/test_file.txt ./`
8. `rm test_file.txt`
9. `echo "Hello, Ubuntu!" > test_file.txt`
10. `cat test_file.txt`
11. `find . -name test_file.txt`
12. `history`
13. `df -h`
14. `ps -aux`
15. `kill 1234`
16. `chmod 777 test_file.txt`
17. `uname -a`
18. `ifconfig 或 ip addr`
19. `grep "Ubuntu" test_file.txt`
20. 压缩：`tar -czvf new_folder.tar.gz new_folder/` 解压：`tar -xzvf new_folder.tar.gz`

提高难度的练习题答案

1. `find /var/log -name "*.log" | xargs ls -lSh`
2. `tail -f /var/log/syslog`
3. `find /home -name "*.txt" -exec rm {} \;`
4. `rename 's/\.txt$/.text/' *.txt`
5. `sudo lsof -i :80 或 sudo netstat -tulnp | grep :80`
6. `crontab -e 然后添加 0 6 * * * tar -czf /backup/home_$(date +\%Y\%m\%d).tar.gz /home`
7. `find / -size +100M`
8. `tail -n 20 /var/log/syslog`
9. `awk -F':' '{ print $1 }' /etc/passwd`
10. `chown -R tom:tom /data`
11. `ldd /path/to/program`
12. `sed -i 's/Welcome/Welcome to Our Website/g' /var/www/html/index.html`
13. `tar -czvf archives.tar.gz /logs /backup`
14. 分割：`split -b 100m bigfile.iso bigfile_part_` 合并：`cat bigfile_part_* > bigfile.iso`
15. `sed -i '/^$/d' test_file.txt`
16. `iftop` 或 `nload`
17. `ps -u alice`
18. 备份：`mysqldump -u root -p mydb > mydb_backup.sql` 恢复：`mysql -u root -p mydb < mydb_backup.sql`
19. `chmod +x *.sh`
20. `diff config_old.txt config_new.txt`
