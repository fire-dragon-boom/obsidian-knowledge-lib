---
tags:
  - android
  - compose
---
# Modifier

## graphicsLayer

> [!NOTE]
> 图形修饰符，可以进行移动旋转变换等操作
> [官方文档](https://developer.android.google.cn/develop/ui/compose/graphics/draw/modifiers?hl=zh-cn#graphics-modifiers)

``` kotlin
Box(  
    modifier = Modifier  
        .size(5.dp)  
        .clip(CircleShape)  
        .graphicsLayer(  
            scaleX = selectedAnimation,  
            scaleY = selectedAnimation,  
            alpha = selectedAnimation  
        )  
)
```










---

# 渐变
``` kotlin
// 渐变背景，边框
modifier = Modifier  
    .fillMaxWidth()  
    .drawBehind {  
        // 先创建圆角路径  
        val cornerRadius = 10.dp.toPx()  
        val roundedRect = RoundRect(  
            rect = Rect(Offset.Zero, size),  
            cornerRadius = CornerRadius(cornerRadius, cornerRadius)  
        )  
  
        // 应用圆角裁剪  
        clipPath(  
            path = Path().apply {  
                addRoundRect(roundedRect)  
            }  
        ) {  
            // 在裁剪区域内绘制图片  
            drawImage(  
                imageBitmap,  
                dstSize = IntSize(  
                    size.width.toInt(),  
                    size.height.toInt()  
                ),  
                filterQuality = FilterQuality.High  
            )  
        }  
    }    .background(  
        brush = Brush.linearGradient(  
            colorStops = arrayOf(  
                0f to Color(119, 110, 124),  
                .2f to Color(119, 110, 124),  
                .8f to Color(49, 40, 48),  
                1f to Color(49, 40, 48)  
            ),  
        ),  
        shape = RoundedCornerShape(10.dp)  
    )  
    .border(  
        width = 1.dp,  
        brush = Brush.linearGradient(  
            colorStops = arrayOf(  
                0f to Color(0xFFC0B8B8),  
                0.15f to Color.Transparent,  
                0.85f to Color.Transparent,  
                1f to Color(0xFFC0B8B8)  
            ),  
        ),  
        shape = RoundedCornerShape(10.dp)  
    )  
    .clip(RoundedCornerShape(10.dp))
```


---

# 状态栏

### 设置状态栏颜色

``` kotlin

// 设置状态栏颜色
val view = LocalView.current
SideEffect {
	// 设置状态栏文字为白色
	WindowCompat.getInsetsController(
		window, view
	).isAppearanceLightStatusBars = false
	// 同时设置状态栏背景透明
	window.statusBarColor = android.graphics.Color.TRANSPARENT
}
```



# 系统参数信息获取

``` kotlin
val density = LocalDensity.current  // 获取屏幕密度
val windowInfo = LocalWindowInfo.current  //获取窗口信息
val configuration = LocalConfiguration.current  //获取配置信息

```





---


# splash(启动动画)

1. 导入库
	```toml
	splashscreen = "1.2.0"
	androidx-core-splashscreen = { group = "androidx.core", name = "core-splashscreen", version.ref = "splashscreen" }
	```
2. activity 中使用
	```kotlin
	// 启动页(在setContent之前)  
	installSplashScreen().apply {  
	    setKeepOnScreenCondition { false }  
	}
	```
3. 配置theme.xml
	```xml
	<!--启动页-->  
	<style name="Theme.Coldfish.Splash" parent="Theme.SplashScreen">  
	    <item name="windowSplashScreenBackground">@color/black</item>  
	    <item name="windowSplashScreenAnimatedIcon">@drawable/ic_splash</item>  
	    <item name="windowSplashScreenAnimationDuration">1000</item>  
	    <item name="postSplashScreenTheme">@style/Theme.Coldfish.Base</item>  
	</style>
	```
4. manifest文件:使用splash theme 
	```xml
	<application  
	    android:theme="@style/Theme.Coldfish.Splash">  
	</application>
	```

---





# next






---



