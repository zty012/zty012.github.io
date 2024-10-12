首先需要安装一个插件 [Stunkymonkey/nautilus-open-any-terminal](https://github.com/Stunkymonkey/nautilus-open-any-terminal)，我这边用的是 AUR 安装

然后用 `dconf-editor`，编辑插件的配置

![image](https://github.com/user-attachments/assets/0024de1c-4957-4bb1-b1aa-ab8ac19f415f)

其中 `custom-local-command` 可以填写终端可执行文件的路径，如果在 PATH 里面可以直接写文件名，比如 `foot`

然后打开 Nautilus，发现插件根本没用，找到了这篇 Issue [#125](https://github.com/Stunkymonkey/nautilus-open-any-terminal/issues/125)

执行 `nautilus -q`，然后再打开 Nautilus，就可以用了