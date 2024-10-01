现象：窗口是透明的，完全没反应

首先在 `lib.rs` 里面添加打开 Devtools 的代码

```diff
use tauri::Manager;

// Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
#[tauri::command]
fn greet(name: &str) -> String {
    format!("Hello, {}! You've been greeted from Rust!", name)
}

#[cfg_attr(mobile, tauri::mobile_entry_point)]
pub fn run() {
    tauri::Builder::default()
+       .setup(|app| {
+           #[cfg(debug_assertions)] // only include this code on debug builds
+           {
+               let window = app.get_webview_window("main").unwrap();
+               window.open_devtools();
+           }
+           Ok(())
+       })
        .plugin(tauri_plugin_fs::init())
        .plugin(tauri_plugin_dialog::init())
        .plugin(tauri_plugin_os::init())
        .plugin(tauri_plugin_shell::init())
        .invoke_handler(tauri::generate_handler![greet])
        .run(tauri::generate_context!())
        .expect("error while running tauri application");
}
```

发现 Devtools 中没有任何内容，鉴定为卡了

把前端代码中有关 Tauri 的部分注释掉，用浏览器打开 http://localhost:1420/

用浏览器的 Devtools 查看报错

我 就 知 道

```
Uncaught RangeError: Maximum call stack size exceeded
```