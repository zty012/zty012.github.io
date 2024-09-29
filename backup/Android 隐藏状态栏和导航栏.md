修改 theme 文件

```xml
<resources>
    <style name="AppTheme.FullScreen" parent="Theme.AppCompat.DayNight.NoActionBar">
        <item name="android:windowFullscreen">true</item>
        <item name="android:windowLayoutInDisplayCutoutMode">shortEdges</item>
        <item name="android:windowActionBar">false</item>
        <item name="android:windowNoTitle">true</item>
        <item name="android:windowTranslucentNavigation">true</item>
        <item name="android:navigationBarColor">@android:color/transparent</item>
    </style>
</resources>
```

修改 MainActivity 代码文件

```kotlin
package liren.project_graph

import android.os.Bundle
import android.view.WindowInsets
import android.view.WindowInsetsController
import android.view.WindowManager
import androidx.core.view.WindowCompat

class MainActivity : TauriActivity() {
  override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)

    // 设置布局内容（确保在调用窗口相关设置之前）
    setContentView(R.layout.activity_main)

    // 全屏显示应用内容
    WindowCompat.setDecorFitsSystemWindows(window, false)

    // 隐藏系统栏 (状态栏和导航栏)
    window.decorView.windowInsetsController?.let { controller ->
      controller.hide(WindowInsets.Type.statusBars() or WindowInsets.Type.navigationBars())
      controller.systemBarsBehavior = WindowInsetsController.BEHAVIOR_SHOW_TRANSIENT_BARS_BY_SWIPE
    }

    // 防止在沉浸模式下屏幕变暗
    window.addFlags(WindowManager.LayoutParams.FLAG_KEEP_SCREEN_ON)
  }
}
```

~~不会还有人不用kotlin吧~~