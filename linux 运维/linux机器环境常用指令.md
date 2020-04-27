# 常用linux硬件信息查询

## 命令：

## top(查看资源信息，相当与windows任务管理器) 
统计信息区
前五行是系统整体的统计信息。第一行是任务队列信息，同 uptime 命令的执行结果。其内容如下：

01:06:48 当前时间
up 1:22 系统运行时间，格式为时:分
1 user 当前登录用户数
load average: 0.06, 0.60, 0.48 系统负载，即任务队列的平均长度。
三个数值分别为 1分钟、5分钟、15分钟前到现在的平均值。

第二、三行为进程和CPU的信息。当有多个CPU时，这些内容可能会超过两行。内容如下：

Tasks: 29 total 进程总数
1 running 正在运行的进程数
28 sleeping 睡眠的进程数
0 stopped 停止的进程数
0 zombie 僵尸进程数
Cpu(s): 0.3% us 用户空间占用CPU百分比
1.0% sy 内核空间占用CPU百分比
0.0% ni 用户进程空间内改变过优先级的进程占用CPU百分比
98.7% id 空闲CPU百分比
0.0% wa 等待输入输出的CPU时间百分比
0.0% hi
0.0% si

最后两行为内存信息。内容如下：

Mem: 191272k total 物理内存总量
173656k used 使用的物理内存总量
17616k free 空闲内存总量
22052k buffers 用作内核缓存的内存量
Swap: 192772k total 交换区总量
0k used 使用的交换区总量
192772k free 空闲交换区总量
123988k cached 缓冲的交换区总量。
内存中的内容被换出到交换区，而后又被换入到内存，但使用过的交换区尚未被覆盖，
该数值即为这些内容已存在于内存中的交换区的大小。
相应的内存再次被换出时可不必再对交换区写入。

进程信息区
统计信息区域的下方显示了各个进程的详细信息。首先来认识一下各列的含义。

序号 列名 含义
a PID 进程id
b PPID 父进程id
c RUSER Real user name
d UID 进程所有者的用户id
e USER 进程所有者的用户名
f GROUP 进程所有者的组名
g TTY 启动进程的终端名。不是从终端启动的进程则显示为 ?
h PR 优先级
i NI nice值。负值表示高优先级，正值表示低优先级
j P 最后使用的CPU，仅在多CPU环境下有意义
k %CPU 上次更新到现在的CPU时间占用百分比
l TIME 进程使用的CPU时间总计，单位秒

m TIME+ 进程使用的CPU时间总计，单位1/100秒
n %MEM 进程使用的物理内存百分比
o VIRT 进程使用的虚拟内存总量，单位kb。VIRT=SWAP+RES
p SWAP 进程使用的虚拟内存中，被换出的大小，单位kb。
q RES 进程使用的、未被换出的物理内存大小，单位kb。RES=CODE+DATA
r CODE 可执行代码占用的物理内存大小，单位kb
s DATA 可执行代码以外的部分(数据段+栈)占用的物理内存大小，单位kb
t SHR 共享内存大小，单位kb
u nFLT 页面错误次数
v nDRT 最后一次写入到现在，被修改过的页面数。
w S 进程状态。
D=不可中断的睡眠状态
R=运行
S=睡眠
T=跟踪/停止
Z=僵尸进程
x COMMAND 命令名/命令行
y WCHAN 若该进程在睡眠，则显示睡眠中的系统函数名



## lscpu(cpu信息)

Architecture:　　　　　　i686   　　         #cpu架构    <br>
CPUop-mode(s):　　　　　32-bit, 64-bit                 
Byte Order: 　　　　　　Little Endian  　　 #小尾序     <br>
CPU(s):                　　4               　　#总共有4核  <br>
On-line CPU(s) list:   　　0-3                        <br>
Thread(s) per core:    　　1　　               #每个cpu核，只能支持一个线程，即不支持超线程<br>
Core(s) per socket:    　　4  　　             #每个cpu，有4个核><br>
Socket(s):       　　      1  　　             #总共有1一个cpu <br>
Vendor ID:   　　          GenuineIntel 　　   #cpu产商 intel <br>
CPU family:           　　 6              <br>
Model:                 　　42             <br>
Stepping:              　　7              <br>
CPU MHz:               　　1600.000       <br>
BogoMIPS:             　　 5986.12        <br>
Virtualization:        　　VT-x            #支持cpu虚拟化技术 <br>
L1d cache:             　　32K              
L1i cache:             　　32K            <br> 
L2 cache:              　　256K           <br>
L3 cache:              　　6144K          <br>

## free -m  （查看内存情况）
total　　 used 　　 free 　　 shared  　 buffers  　　 cached <br>
Mem:  　　3926  　　  3651   　　  274 　  0 　 12   　　404  <br>
-/+ buffers/cache:　3235  　 691  <br>

Swap: 　9536 　  31  　 9505<br>

**总共内存**：3926 

## df -hl （查看硬盘大小）

第一列Filesystem，磁盘分区

第二列Size，磁盘分区的大小



第三列Used，已使用的空间

第四列Avail，可用的空间

第五列Use%，已使用的百分比



第六列Mounted on，挂载点

## nvidia-smi(GPU情况)
第一栏的Fan：N/A是风扇转速，从0到100%之间变动，这个速度是计算机期望的风扇转速，实际情况下如果风扇堵转，可能打不到显示的转速。有的设备不会返回转速，因为它不依赖风扇冷却而是通过其他外设保持低温。

第二栏的Temp：是温度，单位摄氏度。

第三栏的Perf：是性能状态，从P0到P12，P0表示最大性能，P12表示状态最小性能。

第四栏下方的Pwr：是能耗，上方的Persistence-M：是持续模式的状态，持续模式虽然耗能大，但是在新的GPU应用启动时，花费的时间更少，这里显示的是off的状态。

第五栏的Bus-Id是涉及GPU总线的东西，domain:bus:device.function

第六栏的Disp.A是Display Active，表示GPU的显示是否初始化。

第五第六栏下方的Memory Usage是显存使用率。

第七栏是浮动的GPU利用率

第八栏上方是关于ECC的东西。

第八栏下方Compute M是计算模式.

## renice 命令(控制进程优先级)

功能说明：调整优先权。

语　　法：renice [优先等级][-g <程序群组名称>…][-p <程序识别码>…][-u <用户名称>…]

补充说明：renice指令可重新调整程序执行的优先权等级。预设是以程序识别码指定程序调整其优先权，您亦可以指定程序群组或用户名称调整优先权等级， 并修改所有隶属于该程序群组或用户的程序的优先权。等级范围从-20–19，只有系统管理者可以改变其他用户程序的优先权，也仅有系统管理者可以设置负数 等级。
参　　数：
-g <程序群组名称> 　使用程序群组名称，修改所有隶属于该程序群组的程序的优先权。
-p <程序识别码> 　改变该程序的优先权等级，此参数为预设值。
-u <用户名称> 　指定用户名称，修改所有隶属于该用户的程序的优先权。

## 查看端口状态

netstat -tnlp|grep 5666


## 新建shell用户账号
  useradd -r -m -s /bin/bash yuanwei
  userdel yuanwei
  passwd  xxx



  #修改用户权限：
   sudo chmod +w /etc/sudoers
   sudo vim /etc/sudoers
      root　ALL=(ALL:ALL) ALL
      XXX ALL=(ALL:ALL) ALL    //这一行为添加的代码，XXX表示需要添加权限的用户名

# 限制用户进程数

修改 vi /etc/security/limits.conf 文件来设定：

vim /etc/security/limits.conf

vpsee hard nproc 32
@student hard nproc 32
@faculty hard nproc 64
上面的配置文件意思是说限制 vpsee 这个用户只能 fork 32 个进程；然后限制 student 这个用户组的每个成员最多能 fork 32 个进程；

# IO 监控情况

## 查看IO命令 ：iotop

 **内容** ：简单易懂，关注的是进程间的io占用



LinuxIO 详细参考： https://www.cnblogs.com/quixotic/p/3258730.html

# 设置定时任务

## 设置定时任务 <crontab -e>

 分     小时    日       月       星期     命令

    0-59   0-23   1-31   1-12     0-6     command     (取值范围,0表示周日一般一行对应一个任务)
    
    记住几个特殊符号的含义:
    “*”代表取值范围内的数字,
    “/”代表”每”,
    “-”代表从某个数字到某个数字,
    “,”分开几个离散的数字

## 查看定时任务<crontab -l> 



**具体参考内容** ： https://blog.csdn.net/xiyuan1999/article/details/8160998



# 设置挂载盘



- 保证安装了nfs

  ```
  apt-get install -y  nfs-kernel-server
  ```

**配置**

- 服务端
   (1) 在`/etc/exports`文件添加可以共享的文件夹和允许的客户端地址

```csharp
/media/alic/asus 172.31.131.151(rw,no_root_squash,async)
```

​      (2) 重启nfs服务

```shell
sudo systemctl restart nfs-server.service
```

​      (3)更新添加的内容

```
exportfs -arv
```

​      (4)查看是否加载

```
showmount -e
```

   **ps**：只有查看到有新加的挂载，才可认为挂载成功



- 客户端
   (1) 先创建挂载的目录

```undefined
 ~ sudo mkdir /home/alic/Alic/share
```

(2) 挂载远程磁盘

```ruby
 sudo mount  10.0.64.117:/media/alic/asus  /home/alic/Alic/share
```

  

# linux 命令查找大全

  Linux其他命令参考：https://www.linuxcool.com/ 

# linux 系统日志分析
linux 机器发生系统故障参考 ：https://www.cnblogs.com/yihr/p/7212641.html


