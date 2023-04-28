### Flutter 嵌入现有APP

### 前言
&emsp;&emsp;将 Flutter 嵌入现有的APP中，将面对这样一个问题：**如何控制 flutter 显示你想要的页面？**如何控制flutter入口显示的页面？

Flutter 官方给出了两个解决方案，在使用时发现，这三个方案都不那么切合实际需求。而咸鱼团队的 `Flutter Boost` 的方案，目前来看是flutter 嵌入现有APP的最佳方案。


###1.Flutter 官方提供的方案
根据[Flutter](https://flutter.cn/docs/development/add-to-app/ios/add-flutter-screen)的介绍,你可以在 `FlutterEngine  Run`之前，有两种方式选择flutter 页面呈现的入口。分别是：  

 - 1. 指定 Dart 入口  
 - 2. 设置初始路由

#### 1.1指定 Dart 入口  

按照官方的说明，在 FlutterEngine 上调用 run，默认将会调用 `lib/main.dart` 文件里的 main() 函数。

使用另一个入口方法 `runWithEntrypoint`，指定一个不同的 Dart 入口。


```
//Objective-C
[flutterEngine runWithEntrypoint:@"myOtherEntrypoint"]
```

```Dart
//Dart
//使用 main() 以外的 Dart 入口函数，必须使用下面的注解，防止被 tree-shaken 优化掉，而没有编译。
@pragma('vm:entry-point')
void myOtherEntrypoint() { ... };

```
在指定 Dart 函数时，可以指定特定文件的特定函数。  
使用 `lib/other_file.dart` 文件的 `myOtherEntrypoint()` 函数取代 `lib/main.dart` 的 main() 函数：

```
[flutterEngine runWithEntrypoint:@"myOtherEntrypoint" libraryURI:@"other_file.dart"];

```
指定特定文件的特定函数,这一方式在实际测试中，并没有成功，`libraryURI`的设置方式目前没有找到具体的说明。

#### 1.2 设置初始路由

当构建 engine 时，可以为你的 Flutter WidgetsApp 设置一个初始路由。

```
//OC 
FlutterEngine *flutterEngine =
    [[FlutterEngine alloc] initWithName:@"my flutter engine"];
[[flutterEngine navigationChannel] invokeMethod:@"setInitialRoute"
                                      arguments:@"/onboarding"];
[flutterEngine run];

```
`navigationChannel` 上的 `setInitialRoute` 必须在启动 FlutterEngine 前调用，才能在 Flutter 的第一帧中显示期望的路由。

####1.3 总结

Flutter官方提供的这两种方式都要求在 `Flutter Engine` 执行 `run` 方法之前调用。当 APP 中使用单例的Flutter engine时，只有一次指定的机会，这明显不能满足 每次进入 Flutter 页面时，显示指定页面需求。 





















