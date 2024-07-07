如果该版本认定为是一个整合包，那么它的游戏目录将会在它的版本目录。

如：.minecraft/versions/1.18.2 是一个整合包，那么它的游戏目录将会是 .minecraft/versions/1.18.2，而不是 .minecraft

那么，如何伪装整合包呢？

你可以通过在版本目录（即上文的 .minecraft/versions/1.18.2）新建一个名为 modpack.cfg 或 modpack.json 的空文件，以实现整合包伪装。

> [参考](https://github.com/MrShieh-X/console-minecraft-launcher/issues/11#issuecomment-1116786613)