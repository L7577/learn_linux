# 磁盘相关

## 磁盘管理

命令导航
- [cd](#cd)
- [df](#df)
- [du](#du)
- [mkdir](#mkdir)
- [pwd](#pwd)
- [quota](#quota)
- [mount](#mount)
- [stat](#stat)
- [tree](#tree)

### cd
cd命令用于切换当前工作目录至 dirName(目录参数)。
其中 dirName 表示法可为绝对路径或相对路径。若目录名称省略，则变换至使用者的 home 目录 (也就是刚 login 时所在的目录)。
另外，"~" 也表示为 home 目录 的意思，"." 则是表示目前所在的目录，".." 则表示目前目录位置的上一层目录。
eg
```
cd
# 返回当前用户主目录
cd ..
# 返回上一级目录
cd /
#转到根目录
```

### df 
用于显示目前在Linux系统上的文件系统的磁盘使用情况统计
```
df [选项]...  [FILE]...
```
>-   文件-a, --all 包含所有的具有 0 Blocks 的文件系统
>-   文件--block-size={SIZE} 使用 {SIZE} 大小的 Blocks
>-   文件-h, --human-readable 使用人类可读的格式(预设值是不加这个选项的...)
>-   文件-H, --si 很像 -h, 但是用 1000 为单位而不是用 1024
>-   文件-i, --inodes 列出 inode 资讯，不列出已使用 block
>-   文件-k, --kilobytes 就像是 --block-size=1024
>-   文件-l, --local 限制列出的文件结构
>-   文件-m, --megabytes 就像 --block-size=1048576
>-   文件--no-sync 取得资讯前不 sync (预设值)
>-   文件-P, --portability 使用 POSIX 输出格式
>-   文件--sync 在取得资讯前 sync
>-   文件-t, --type=TYPE 限制列出文件系统的 TYPE
>-   文件-T, --print-type 显示文件系统的形式
>-   文件-x, --exclude-type=TYPE 限制列出文件系统不要显示 TYPE
>-   文件-v (忽略)
>-   文件--help 显示这个帮手并且离开
>-   文件--version 输出版本资讯并且离开

eg:
```
df -hT
#使用人类可读的格式打印当前磁盘使用情况，并显示文件系统的形式
```


### du
用于显示目录或者文件的大小
du会显示指定的目录或者文件所占用的磁盘空间
```
du [-abcDhHklmsSx][-L <符号连接>][-X <文件>][--block-size][--exclude=<目录或文件>][--max-depth=<目录层数>][--help][--version][目录或文件]
```
>-   -a或-all 显示目录中个别文件的大小。
>-   -b或-bytes 显示目录或文件大小时，以byte为单位。
>-   -c或--total 除了显示个别目录或文件的大小外，同时也显示所有目录或文件的总和。
>-   -D或--dereference-args 显示指定符号连接的源文件大小。
>-   -h或--human-readable 以K，M，G为单位，提高信息的可读性。
>-   -H或--si 与-h参数相同，但是K，M，G是以1000为换算单位。
>-   -k或--kilobytes 以1024 bytes为单位。
>-   -l或--count-links 重复计算硬件连接的文件。
>-   -L<符号连接>或--dereference<符号连接> 显示选项中所指定符号连接的源文件大小。
>-   -m或--megabytes 以1MB为单位。
>-   -s或--summarize 仅显示总计。
>-   -S或--separate-dirs 显示个别目录的大小时，并不含其子目录的大小。
>-   -x或--one-file-xystem 以一开始处理时的文件系统为准，若遇上其它不同的文件系统目录则略过。
>-   -X<文件>或--exclude-from=<文件> 在<文件>指定目录或文件。
>-   --exclude=<目录或文件> 略过指定的目录或文件。
>-   --max-depth=<目录层数> 超过指定层数的目录后，予以忽略。
>-   --help 显示帮助。
>-   --version 显示版本信息。

eg
```
du -ch ./
```
### mkdir
用于创建目录
>- -p若是目录不存在就创建

eg:
```
mkdir -p /usr/local/cuda
```

### pwd
用于显示工作目录。
```
$ pwd
/home/name/test
```

### quota
用于显示磁盘已使用的空间与限制。
执行quota指令，可查询磁盘空间的限制，并得知已使用多少空间。
```
quota [-quvV][用户名称...]  或 quota [-gqvV][群组名称...]
```
>-   -g 列出群组的磁盘空间限制。
>-   -q 简明列表，只列出超过限制的部分。
>-   -u 列出用户的磁盘空间限制。
>-   -v 显示该用户或群组，在所有挂入系统的存储设备的空间限制。
>-   -V 显示版本信息。


### mount
用于挂载Linux系统外的文件
```
mount [-hV] 
mount -a [-fFnrsvw]  [-t vfstype] 
mount [-fnrsvw]  [-o options [,...]] device | dir
mount [-fnrsvw]  [-t vfstype]  [-o options] device dir
```
>-   -V：显示程序版本
>-   -h：显示辅助讯息
>-   -v：显示较讯息，通常和 -f 用来除错。
>-   -a：将 /etc/fstab 中定义的所有档案系统挂上。
>-   -F：这个命令通常和 -a 一起使用，它会为每一个 mount 的动作产生一个行程负责执行。在系统需要挂上大量 NFS 档案系统时可以加快挂上的动作。
>-   -f：通常用在除错的用途。它会使 mount 并不执行实际挂上的动作，而是模拟整个挂上的过程。通常会和 -v 一起使用。
>-   -n：一般而言，mount 在挂上后会在 /etc/mtab 中写入一笔资料。但在系统中没有可写入档案系统存在的情况下可以用这个选项取消这个动作。
>-   -s-r：等于 -o ro
>-   -w：等于 -o rw
>-   -L：将含有特定标签的硬盘分割挂上。
>-   -U：将档案分割序号为 的档案系统挂下。-L 和 -U 必须在/proc/partition 这种档案存在时才有意义。
>-   -t：指定档案系统的型态，通常不必指定。mount 会自动选择正确的型态。
>-   -o async：打开非同步模式，所有的档案读写动作都会用非同步模式执行。
>-   -o sync：在同步模式下执行。
>-   -o atime、-o noatime：当 atime 打开时，系统会在每次读取档案时更新档案的『上一次调用时间』。当我们使用 flash 档案系统时可能会选项把这个选项关闭以减少写入的次数。
>-   -o auto、-o noauto：打开/关闭自动挂上模式。
>-   -o defaults:使用预设的选项 rw, suid, dev, exec, auto, nouser, and async.
>-   -o dev、-o nodev-o exec、-o noexec允许执行档被执行。
>-   -o suid、-o nosuid：
>-   允许执行档在 root 权限下执行。
>-   -o user、-o nouser：使用者可以执行 mount/umount 的动作。
>-   -o remount：将一个已经挂下的档案系统重新用不同的方式挂上。例如原先是唯读的系统，现在用可读写的模式重新挂上。
>-   -o ro：用唯读模式挂上。
>-   -o rw：用可读写模式挂上。
>-   -o loop=：使用 loop 模式用来将一个档案当成硬盘分割挂上系统。

eg:
```
mount /dev/hda1 /mnt
#挂在/dev/hda1 到/mnt下
mount -o ro /dev/hda1 /mnt
# 用只读模式挂载
```

### stat
stat以文字的格式来显示inode的内容
```
stat [文件或目录]
```


### tree
以树状图列出目录的内容。
```
tree [-aACdDfFgilnNpqstux][-I <范本样式>][-P <范本样式>][目录...]
```
>-   -a 显示所有文件和目录。
>-   -A 使用ASNI绘图字符显示树状图而非以ASCII字符组合。
>-   -C 在文件和目录清单加上色彩，便于区分各种类型。
>-   -d 显示目录名称而非内容。
>-   -D 列出文件或目录的更改时间。
>-   -f 在每个文件或目录之前，显示完整的相对路径名称。
>-   -F 在执行文件，目录，Socket，符号连接，管道名称名称，各自加上"*","/","=","@","|"号。
>-   -g 列出文件或目录的所属群组名称，没有对应的名称时，则显示群组识别码。
>-   -i 不以阶梯状列出文件或目录名称。
>-   -L level 限制目录显示层级。
>-   -l 如遇到性质为符号连接的目录，直接列出该连接所指向的原始目录。
>-   -n 不在文件和目录清单加上色彩。
>-   -N 直接列出文件和目录名称，包括控制字符。
>-   -p 列出权限标示。
>-   -P<范本样式> 只显示符合范本样式的文件或目录名称。
>-   -q 用"?"号取代控制字符，列出文件和目录名称。
>-   -s 列出文件或目录大小。
>-   -t 用文件和目录的更改时间排序。
>-   -u 列出文件或目录的拥有者名称，没有对应的名称时，则显示用户识别码。
>-   -x 将范围局限在现行的文件系统中，若指定目录下的某些子目录，其存放于另一个文件系统上，则将该子目录予以排除在寻找范围外。



### ls
用于显示指定工作目录下之内容（列出目前工作目录所含之文件及子目录)。
```
ls [-alrtAFR]  [name...]
```
>-   -a 显示所有文件及目录 (ls内定将文件名或目录名称开头为"."的视为隐藏档，不会列出)
>-   -l 除文件名称外，亦将文件型态、权限、拥有者、文件大小等资讯详细列出
>-   -r 将文件以相反次序显示(原定依英文字母次序)
>-   -t 将文件依建立时间之先后次序列出
>-   -A 同 -a ，但不列出 "." (目前目录) 及 ".." (父目录)
>-   -F 在列出的文件名称后加一符号；例如可执行档则加 "*", 目录则加 "/"
>-   -R 若目录下有文件，则以下之文件亦皆依序列出


## 磁盘维护
命令导航
- [dd](#dd)
- [fdisk](#fdisk)

### dd
dd可从标准输入或文件中读取数据，根据指定的格式来转换数据，再输出到文件、设备或标准输出。
> -   if=文件名：输入文件名，默认为标准输入。即指定源文件。
> -   of=文件名：输出文件名，默认为标准输出。即指定目的文件。
> -   ibs=bytes：一次读入bytes个字节，即指定一个块大小为bytes个字节。  
    obs=bytes：一次输出bytes个字节，即指定一个块大小为bytes个字节。  
    bs=bytes：同时设置读入/输出的块大小为bytes个字节。
 >-   cbs=bytes：一次转换bytes个字节，即指定转换缓冲区大小。
 >-   skip=blocks：从输入文件开头跳过blocks个块后再开始复制。
 >-   seek=blocks：从输出文件开头跳过blocks个块后再开始复制。
 >-   count=blocks：仅拷贝blocks个块，块大小等于ibs指定的字节数。
 >-   conv=<关键字>，关键字可以有以下11种:
	  -   conversion：用指定的参数转换文件。
    -   ascii：转换ebcdic为ascii
    -   ebcdic：转换ascii为ebcdic
    -   ibm：转换ascii为alternate ebcdic
    -   block：把每一行转换为长度为cbs，不足部分用空格填充
    -   unblock：使每一行的长度都为cbs，不足部分用空格填充
    -   lcase：把大写字符转换为小写字符
    -   ucase：把小写字符转换为大写字符
    -   swab：交换输入的每对字节
    -   noerror：出错时不停止
    -   notrunc：不截短输出文件
    -   sync：将每个输入块填充到ibs个字节，不足部分用空（NUL）字符补齐。
>-   --help：显示帮助信息
>-   --version：显示版本信息

### fdisk
fdisk是一个创建和维护分区表的程序，它兼容DOS类型的分区表、BSD或者SUN类型的磁盘列表。
>  必要参数
>-   -l 列出素所有分区表
>-   -u 与"-l"搭配使用，显示分区数目
选择参数
>-   -s<分区编号> 指定分区
>-   -v 版本信息
菜单操作
>-   m ：显示菜单和帮助信息
>-   a ：活动分区标记/引导分区
>-   d ：删除分区
>-   l ：显示分区类型
>-   n ：新建分区
>-   p ：显示分区信息
>-   q ：退出不保存
>-   t ：设置分区号
>-   v ：进行分区检查
>-   w ：保存修改
>-   x ：扩展应用，高级功能

```
fdisk -l
#显示当前分区
fdisk -lu
#显示每个分区
```
