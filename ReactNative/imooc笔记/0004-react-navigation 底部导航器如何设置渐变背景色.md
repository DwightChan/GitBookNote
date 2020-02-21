[toc]

---

# 如何设置渐变背景色

1、react-navigation底部导航器如何设置渐变背景色？
2、顶部标题栏如何设置渐变背景色？

帮你实现了下：

1. 按照https://github.com/react-native-community/react-native-linear-gradient 的说明安装react-native-linear-gradient

2. 在DynamicTabNavigator中做如下改动：


```
class TabBarComponent extends React.Component {
  ...
 
    render() {
        return <BottomTabBar
            {...this.props}
            activeTintColor={this.props.theme.themeColor}
        />
    }
}
//改成
class TabBarComponent extends React.Component {
    ...
 
    render() {
        return <LinearGradient
            colors={['#4c669f', '#3b5998', '#192f6a']}
        >
 
            <BottomTabBar
                {...this.props}
                activeTintColor={this.props.theme.themeColor}
                style={{
                    backgroundColor: 'transparent',
                }}
            />
        </LinearGradient>;
 
    }
}
```

另外，顶部导航的渐变实现思路和底部导航是一样的，你可以参考DynamicTabNavigator的实现，为顶部导航自定义个tabBarComponent，其他的步骤都是一样的。