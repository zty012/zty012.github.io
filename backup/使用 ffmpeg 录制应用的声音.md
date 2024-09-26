然后用 ffmpeg 录制音频

```bash
➜  ~ ffmpeg -f pulse -i default output.wav

ffmpeg version n7.0.2 Copyright (c) 2000-2024 the FFmpeg developers
Press [q] to stop, [?] for help
```

然后就可以在应用里面播放音频了，会输出到 output.wav