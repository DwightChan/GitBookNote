[toc]



-----

## Flutter 必备基础知识自测小作业
### 作业1: 学习过Flutter 官方示例项目你都有哪些？

```
Flutter 官方提供了一些重要的示例项目，比如：
1. **Flutter Gallery**：这是一个展示 Flutter 组件和功能的项目，包括各种 UI 组件、动画、手势等。
2. **Counter App**：一个简单的 Flutter 入门项目，展示了基本的状态管理和 UI 更新机制。
3. **Todo App**：展示如何创建一个多页面应用，使用表单输入、路由等。
4. **Animations Sample**：展示 Flutter 中复杂的动画如何实现，使用 `AnimationController` 和 `Tween` 等。
```

### 作业2: 如何为图片设置Placeholder？

```
可以使用 Flutter 中的 `FadeInImage` 来为图片设置占位符：
```dart
FadeInImage.assetNetwork(
  placeholder: 'assets/placeholder.png', // 占位图片
  image: 'https://example.com/image.png', // 实际图片
)
```
这段代码在实际图片加载前显示一个占位符图像。

### 作业3: 如何加载不同分辨率的项目中的图片？

Flutter 支持多分辨率图片，可以通过提供不同尺寸的图片资源：
```yaml
flutter:
  assets:
    - assets/images/logo.png
    - assets/images/2.0x/logo.png
    - assets/images/3.0x/logo.png
```
Flutter 根据设备的 DPI 自动选择最合适的图像分辨率。


### 作业4:如何加载手机存储中的图片？


可以使用 `Image.file` 来加载存储在设备本地的图片：
```dart
import 'dart:io';
import 'package:flutter/material.dart';

File imageFile = File('/path/to/image');
Image.file(imageFile);
```


### 作业5: 实现一个动画都有哪些方式？


1. **隐式动画**：例如 `AnimatedContainer`、`AnimatedOpacity` 等，Flutter 会自动处理动画过渡。
2. **显式动画**：使用 `AnimationController` 和 `Tween` 实现，更加灵活，适合复杂动画。
3. **Hero 动画**：在页面切换时，让元素在两页面之间平滑过渡。


### 作业6: 简述Hero动画都有哪些应用场景？


Hero 动画适用于页面切换时共享某个 UI 元素的场景。例如：
- 列表页面点击某个项目，进入详情页面时，图片或文字可以从一个页面平滑移动到另一个页面。
- 购物车应用中，从商品页面切换到购物车页面时，商品图片可以以 Hero 动画形式过渡。


### 作业7: 你从课程中Get 到了哪些Flutter 调试技巧？


1. 使用 `Flutter DevTools` 查看内存、性能和 UI 构建情况。
2. 通过 `flutter run --debug` 启动调试模式，调试日志和断点调试。
3. 利用 `print` 或 `debugPrint` 在控制台输出调试信息。
4. 使用 `Hot Reload` 快速调试 UI 和代码逻辑。


### 作业8: 如何调试Flutter 项目中的Android 代码？


1. 使用 Android Studio，进入项目的 `android` 目录。
2. 在 Android Studio 中打开 Android 项目部分，设置断点调试 Kotlin/Java 代码。
3. 使用 `adb logcat` 查看 Android 平台的日志信息。
4. 在 Flutter 和 Android 代码之间通过平台通道（Platform Channel）调试通信问题。


### 作业9: 如何调试Flutter 项目中的iOS 代码？


1. 使用 Xcode 打开项目中的 `ios` 目录。
2. 在 Xcode 中设置断点调试 Swift/Objective-C 代码。
3. 使用 Xcode 的调试工具查看应用的性能和日志。
4. 在 Flutter 与 iOS 的 Platform Channel 间调试通信。


