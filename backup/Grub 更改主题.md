1. [下载一个主题](https://www.gnome-look.org/browse?cat=109&ord=latest)
2. 解压
3. `sudo cp -r 文件夹名称 /usr/share/grub/themes`
4. 编辑 `/etc/default/grub`，在结尾添加 `GRUB_THEME="/usr/share/grub/themes/文件夹名称/theme.txt"`
5. `sudo grub-mkconfig -o /boot/grub/grub.cfg`
6. 重启