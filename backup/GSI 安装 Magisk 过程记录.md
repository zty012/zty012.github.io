> [!WARNING]
> 本教程适用于 **小米/红米/POCO** 手机

先从 [hyperos.fans](https://hyperos.fans/zh/devices) 下载你设备的**卡刷包**

![下载卡刷包](https://s2.loli.net/2024/07/16/r59BM73JWCXyTaU.png)


> [!TIP]
> Linux 用户可以使用 Wine 运行 [Neat Download Manager](https://www.neatdownloadmanager.com/index.php/en/) 以获得最快下载速度

下载 tgz 系统包后，把 `/images/init_boot.img` 解压出来，传输到手机上（**切记在电脑上也要留一份**）

![提取 init_boot.img](https://s2.loli.net/2024/07/16/72KrY18bgUzpBA5.png)

打开 Magisk，修补 `init_boot.img` 文件

![Magisk 修补结果](https://s2.loli.net/2024/07/16/eEcMnNrPlTq5DsQ.png)

把 Magisk 中显示的 img 文件路径传输到电脑上

接下来开始施法：

[![asciicast](https://asciinema.org/a/Pz6Er5zV8KsGhFcOQ5lVGCSRJ.svg)](https://asciinema.org/a/Pz6Er5zV8KsGhFcOQ5lVGCSRJ)

> [!WARNING]
> 刷入 `init_boot_*` 分区时，`*` 表示你的系统槽位，如果你不知道的话那就 a 和 b 都试一下

> [!WARNING]
> 如果手机一直重启，请按住音量下+开机键进入 fastboot，把 init_boot 分区刷回没有经过 Magisk 修复的镜像

开机后打开 Magisk，弹出这个就说明成功了，点击确定就完工了

![Magisk 弹窗](https://s2.loli.net/2024/07/16/keWwNF2GYfLTh3O.png)