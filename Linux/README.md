# My Linux Setup

<!-- 在这里编写你的记录 -->

1. VMware - virtual machine
   1. 这玩意下载了大概得有半年了吧
   2. 就偶尔使用一下，使用场景大多是写代码(贪图某些东西可以直接 apt install 的便利，以及命令行的便利)，其余的事情大多在windows完成，最近不想用虚拟机了，因为它老是把我的 CPU 使用率干到惊人的 99%。
2. WSL2
   1. 这个也下载挺久的了，只是之前一直有 bug 然后也没怎么用。我记得之前还不是我下面遇到的 bug。

## 关于 wsl2 连不上网的问题
起因：我在做龙芯班布置的 OS 作业时想着使用以下 wsl + visual studio code 来做作业，然后发现 clone 不了作业仓库，我就发现不对了，然后就开始疯狂的 `ping` 中

```bash
ping baidu.com
ping github.com
ping help.ubuntu.com
```

结果如下：

[![1729559528016.png](https://i.postimg.cc/nL2byz38/1729559528016.png)](https://postimg.cc/NyKzTghb)

再然后肯定就是疯狂的查询资料解决问题

[CSDN小肠文](https://blog.csdn.net/uouj3766/article/details/126596459) 等等等

**搜索得到的所有的解决方案如下**

1. `ifconfig`

    众所周知，我是刚下载的 Ubuntu 发行版，哪来的 `ifconfig` 呢？所以这当然对我没用。

2. `ip route`

    这个命令我看他们都有输出结果，为什么我的没有呢？然后就也解决不了我的问题啊。

    正常会得到以下结果

    ```bash
    default via 172.24.64.1 dev eth0
    172.24.64.0/20 dev eth0 proto kernel scope link src 172.24.66.230
    ```

    再输入 `cat /etc/resolv.conf` 查看 resolv.conf里面的nameserver，如果不是172.24.64.1修改resolv.conf
    ```
    sudo vim /etc/resolv.conf
    ```
    在文件里输入 `nameserver 172.24.64.1` 修改完之后WSL2就可以连接网络了

***痛痛痛死我了***

然后直到我突发奇想想着要不要重启一下 *虚拟机平台* 和 *适用于 Linux 的 Windows 子系统* 这两个 Windows 功能呢？然后就好了，是不是很逆天，我也这样觉得！！！

问大佬，大佬回答如下

https://github.com/microsoft/WSL/issues/10709#issuecomment-2159629182 可能还有后遗症，似乎是VMware有冲突。问题复发的话看这个

(大佬查问题都是从源头开始找，而我从 `CSDN` 找，向佬学习)