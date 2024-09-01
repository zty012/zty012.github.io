首先安装包 `fcitx5-qt`

```bash
sudo pacman -S fcitx5-qt
```

然后把 `/usr/lib/qt/plugins/platforminputcontexts/libfcitx5platforminputcontextplugin.so` 复制到项目里面

在 main 开头插入这段代码

```python
import platform
import PyQt5

# 修复fcitx5输入法
if platform.system() == "Linux":
    target_path = (
        Path(PyQt5.__file__).parent
        / "Qt5"
        / "plugins"
        / "platforminputcontexts"
        / "libfcitx5platforminputcontextplugin.so"
    )
    source_path = (
        # 这里是so文件的路径
        Path(__file__)....... / ... / ...
    )
    if not target_path.exists():
        log(f"修复fcitx5输入法: Copy {source_path} to {target_path}")
        shutil.copy(source_path, target_path)
```

## 支持 PyInstaller

在 PyInstaller 参数里面加上 `--add-data <so文件路径>:PyQt5/Qt5/plugins/platforminputcontexts`

```python
# 打包
PyInstaller.__main__.run(
    [
        "--onefile",
        "--windowed",
        f"--icon={path / 'src' / 'project_graph' / 'assets' / 'favicon.ico'}",
        # 支持fcitx5输入法
        "--add-data",
        f"{path / 'lib'/ 'libfcitx5platforminputcontextplugin.so'}:PyQt5/Qt5/plugins/platforminputcontexts",
        "-n",
        "project-graph",
        (path / "src" / "_package.py").as_posix(),
    ]
)
```