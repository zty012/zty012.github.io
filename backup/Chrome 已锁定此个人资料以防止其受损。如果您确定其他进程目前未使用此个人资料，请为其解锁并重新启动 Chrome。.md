```
➜  ~ google-chrome
[4292:4292:0807/114332.832305:ERROR:process_singleton_posix.cc(353)] 其他计算机 (ZTY-Kubuntu) 的另一个 Google Chrome 进程 (329247) 好像正在使用此个人资料。Chrome 已锁定此个人资料以防止其受损。如果您确定其他进程目前未使用此个人资料，请为其解锁并重新启动 Chrome。
[4292:4292:0807/114332.832370:ERROR:message_box_dialog.cc(144)] Unable to show a dialog outside the UI thread message loop: Google Chrome - 其他计算机 (ZTY-Kubuntu) 的另一个 Google Chrome 进程 (329247) 好像正在使用此个人资料。Chrome 已锁定此个人资料以防止其受损。如果您确定其他进程目前未使用此个人资料，请为其解锁并重新启动 Chrome。
```

这种情况，删除 `~/.config/google-chrome/SingletonLock` 就行了