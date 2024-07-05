试图安装 GitHub CLI，打开了[官网](https://cli.github.com)复制了安装命令

```bash
(type -p wget >/dev/null || (sudo apt update && sudo apt-get install wget -y)) && sudo mkdir -p -m 755 /etc/apt/keyrings && wget -qO- https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo tee /etc/apt/keyrings/githubcli-archive-keyring.gpg > /dev/null && sudo chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg && echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null && sudo apt update && sudo apt install gh -y
```

# 坑 1

```bash
W: 校验数字签名时出错。此仓库未被更新，所以仍然使用此前的索引文件。GPG 错误：https://mirrors.tencent.com/debian bookworm InRelease: 由于没有公钥，无法验证下列签名： NO_PUBKEY 0E98404D386FA1D9 NO_PUBKEY 6ED0E7B82643E131 NO_PUBKEY F8D2585B8783D481
W: 校验数字签名时出错。此仓库未被更新，所以仍然使用此前的索引文件。GPG 错误：https://mirrors.tencent.com/debian bookworm-updates InRelease: 由于没有公钥，无法验证下列签名： NO_PUBKEY 0E98404D386FA1D9 NO_PUBKEY 6ED0E7B82643E131
W: 校验数字签名时出错。此仓库未被更新，所以仍然使用此前的索引文件。GPG 错误：https://mirrors.tencent.com/debian bookworm-backports InRelease: 由于没有公钥，无法验证下列签名： NO_PUBKEY 0E98404D386FA1D9 NO_PUBKEY 6ED0E7B82643E131
W: GPG 错误：https://mirrors.tencent.com/debian-security bookworm-security InRelease: 由于没有公钥，无法验证下列签名： NO_PUBKEY 54404762BBB6E853 NO_PUBKEY BDE6D2B9216EC7A8
E: 仓库 “https://mirrors.tencent.com/debian-security bookworm-security InRelease” 没有数字签名。
N: 无法安全地用该源进行更新，所以默认禁用该源。
N: 参见 apt-secure(8) 手册以了解仓库创建和用户配置方面的细节。
```

第一眼看到了腾讯源，我寻思这我也没设置腾讯源啊，看了一下 `sources.list.d` 目录，发现有一个 `/etc/apt/sources.list.d/debian-mirror-bookworm-tencent.list` 文件，里面写了要删除这个源得运行 `apt purge debian-mirror-bookworm-tencent-apt-source`，所以运行这个命令删除 `debian-mirror-bookworm-tencent-apt-source` 包后就正常了

# 坑 2

```bash
命中:1 https://apt.atzlinux.com/atzlinux bookworm InRelease
命中:2 https://dl.google.com/linux/chrome/deb stable InRelease                                 
命中:3 http://security.ubuntu.com/ubuntu noble-security InRelease                              
命中:4 https://packages.microsoft.com/repos/code stable InRelease                              
命中:5 https://cli.github.com/packages stable InRelease                
正在读取软件包列表... 完成
正在分析软件包的依赖关系树... 完成
正在读取状态信息... 完成                 
有 2 个软件包可以升级。请执行 ‘apt list --upgradable’ 来查看它们。
正在读取软件包列表... 完成
正在分析软件包的依赖关系树... 完成
正在读取状态信息... 完成                 
下列软件包是自动安装的并且现在不需要了：
  apper-data debian-archive-keyring
使用'sudo apt autoremove'来卸载它(它们)。
下列【新】软件包将被安装：
  gh
升级了 0 个软件包，新安装了 1 个软件包，要卸载 0 个软件包，有 2 个软件包未被升级。
需要下载 13.6 MB 的归档。
解压缩后会消耗 50.1 MB 的额外空间。
获取:1 https://cli.github.com/packages stable/main amd64 gh amd64 2.52.0 [13.6 MB]
8% [1 gh 1,441 kB/13.6 MB 11%]                                    2,726 B/s 1小时 14分 31秒
```

开始下载了，但是速度非常慢，一定是 apt 不走系统代理，Google 了一下[^1]，往 `/etc/apt/apt.conf` 文件里面加一行：

```
Acquire::http::Proxy "代理地址";
```

再运行 `sudo apt install gh -y`，很快啊，就安装好了，可以正常使用