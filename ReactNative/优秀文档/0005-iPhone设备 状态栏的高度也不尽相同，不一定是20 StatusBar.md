[toc]

---

# iPhone设备 状态栏的高度也不尽相同，不一定是20 StatusBar

> 要么动态获取，要么根据不同设备在代码里定义好不同设备的状态栏高度？

可以使用这个插件来获取状态栏的动态高度：

https://github.com/ovr/react-native-status-bar-height#readme

```
import { getStatusBarHeight } from 'react-native-status-bar-height';
 
// 44 - on iPhoneX
// 20 - on iOS device
// X - on Android platfrom (runtime value)
// 0 - on all other platforms (default)
console.log(getStatusBarHeight());
 
// will be 0 on Android, because You pass true to skipAndroid
// Android 是 0, 因为已经被系统保留了;
console.log(getStatusBarHeight(true));
```

