```sh
#!/bin/zsh

# 检查参数是否有效
if [ $# -eq 0 ]; then
  # 如果没有参数，使用zenity获取值
  n=$(zenity --entry --title="Install latest APKs" --text="Count:")
  if [ $? -ne 0 ]; then
    echo "Zenity canceled."
    exit 1
  fi

  # 检查返回值是否为数字
  if ! [[ "$n" =~ ^[0-9]+$ ]]; then
    n=1  # 如果不是数字，则设置为1
  fi
else
  # 如果有参数，直接使用参数值
  n=$1
fi

# 初始化进度条
{
  # 使用 find、sort 和 head 获取 APK 文件列表，并逐行读取
  find ~/Downloads -type f -name "*.apk" | sort -rn | head -n "$n" | while read -r apk_file; do
    # 显示正在安装的文件名
    echo "# Installing: $(basename "$apk_file")"  # 显示文件名
    # 计算进度
    echo $(( (i + 1) * 100 / n )) # 更新进度
    ((i++))  # 增加计数器

    # 执行安装命令
    adb install "$apk_file"
  done
} | zenity --progress --title="Installing APKs" --text="Installing APKs..." --percentage=0 --width=300 --auto-close

# 检查进度条是否被取消
if [ $? -ne 0 ]; then
  echo "Installation canceled."
  exit 1
fi