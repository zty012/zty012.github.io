1. 安装 [`git-filter-repo`](https://github.com/newren/git-filter-repo/blob/main/INSTALL.md)
2. 把仓库 clone 一份到另外一个地方
3. `git filter-repo --invert-paths --path <大文件的路径>`
4. `git push --force`

> [!CAUTION]
> `--force` 参数很重要！
