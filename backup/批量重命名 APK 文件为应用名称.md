> [!WARNING]
> 此脚本需要安装 Android Build Tools，并且将 `~/Android/Sdk/build-tools/35.0.0/aapt` 替换为你的 aapt 位置

> 建议运行脚本以后，把 `application-label` 改成 `application-label-zh-CN`，这样文件名就是中文了

```bash
for apk in *.apk; do
    label=$(~/Android/Sdk/build-tools/35.0.0/aapt dump badging "$apk" | grep -Po "^application-label:'\K.*?(?='$)")
    if [[ -z "$label" ]]; then
        echo "error $apk"
        continue
    fi
    mv "$apk" "$label.apk"
    echo "$apk -> $label.apk"
done
```