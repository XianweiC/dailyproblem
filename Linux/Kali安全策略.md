本来说是这个寒假好好学习一下渗透测试的，可随着了解的深入，发现渗透测试需要的知识储备太多了，因此好长时间都没有真正的去学习渗透工具的使用，今天上午装了一个kali，装上之后第一件事就是执行apt-get update && apt-get upgrade，结果却出现了这样的错误
这里写图片描述
我添加的是中科大的更新源，在浏览器中是可以正常打开的：

deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib  
deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib

    1
    2
    3

可是添加到 /etc/apt/source.list之后，执行apt-update就会出现上面的错误提示
这个问题折磨了我一整天，直到刚刚才解决掉，去网上搜，关于这种错误的帖子只有一两个，而且还都是提问的帖子，都挂在那没有解决。。。。因此我在解决了这个问题之后，立马就过来写了这篇博客，供各位网友参考，说不定就能解决你的问题

在多方搜索无果之后，我决定静下心来认真阅读一下kali中提供的文档，根据上面的提示，我查看了apt-secure(8)------>命令man 8 apt-secure

DESCRIPTION
       Starting with version 0.6, APT contains code that does signature
       checking of the Release file for all repositories. This ensures that
       data like packages in the archive can't be modified by people who have
       no access to the Release file signing key. Starting with version 1.1
       APT requires repositories to provide recent authentication information
       for unimpeded usage of the repository. Since version 1.5 changes in the
       information contained in the Release file about the repository need to
       be confirmed before APT continues to apply updates from this
       repository.

       Note: All APT-based package management front-ends like apt-get(8),
       aptitude(8) and synaptic(8) support this authentication feature, so
       this manpage uses APT to refer to them all for simplicity only.



    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17

首先阅读一下apt-secure的描述，读完之后我们可以知道，之所以一直更新不成功，是因为没有签名或者是有签名但是apt没有对应的key的package是不被信任的，安全起见，默认是不会采用这种源来进行更新的

继续往下阅读

UNSIGNED REPOSITORIES
       If an archive has an unsigned Release file or no Release file at all
       current APT versions will refuse to download data from them by default
       in update operations and even if forced to download front-ends like
       apt-get(8) will require explicit confirmation if an installation
       request includes a package from such an unauthenticated archive.

       You can force all APT clients to raise only warnings by setting the
       configuration option Acquire::AllowInsecureRepositories to true.
       Individual repositories can also be allowed to be insecure via the
       sources.list(5) option allow-insecure=yes. Note that insecure
       repositories are strongly discouraged and all options to force apt to
       continue supporting them will eventually be removed. Users also have
       the Trusted option available to disable even the warnings, but be sure
       to understand the implications as detailed in sources.list(5). 
    
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15

第二段的标题正是没有签名的仓库，这正是我们需要的说明
You can force all APT clients to raise only warnings by setting the
configuration option Acquire::AllowInsecureRepositories to true.
这句话就是解决问题的关键，虽然国内的源没有签名，或者签名过期（失效），但是我们可以强制apt进行更新，忽略仓库的安全性，而想要达到这个目的，我们就需要对APT的配置文件进行修改
我搜索了apt.conf这个关键字，但相关网页都是英文的，硬着头皮读完之后发现我的kali中并没有apt.conf文件，在我的/etc/apt目录下，只有一个apt.conf.d目录，cd进该目录：
这里写图片描述
那么多配置文件，我也不知道到底该改哪一个，然后又去百度了一会儿，看到了这篇文章
https://wiki.debian.org/AptConf
然后我就抱着试一试的心态打开了70debconf文件，按照前面man文档的指导，在里面输入了Acquire::AllowInsecureRepositories “true”;
然后执行apt-config dump，查看apt的对应配置有无生效
这里写图片描述
Acquire::AllowInsecureRepositories的属性值由最初的"0"变成了"true"
说明更改配置成功，然后赶紧敲入apt-get update && apt-get upgrade,万分激动地按下回车键

看着一行行的提示快速滚动，那种感觉真的是无与伦比。。。。

可能我的分析有不到位的地方，不过不管怎样，问题是解决了，欢迎各位指正
希望能帮助遇到同样问题的小伙伴**：）**