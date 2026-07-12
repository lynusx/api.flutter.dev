# Flutter API 参考文档

> Flutter SDK 版本：3.44.4

Flutter 是 Google 推出的 SDK，用于通过单一代码库为移动端、Web 和桌面端打造美观、快速的用户体验。Flutter 可以与现有代码协同工作，被全球的开发者和组织广泛使用，并且是免费和开源的。

此 API 参考文档涵盖了 Flutter SDK 导出的所有库。

## 更多文档

本站托管 Flutter 的 API 文档。其他文档可在以下位置找到：

- [安装 Flutter](https://docs.flutter.dev/get-started)
- [Flutter 文档](https://docs.flutter.dev/)
- [稳定渠道（Stable channel）API 参考文档](https://api.flutter.dev/)
- [主渠道（Main channel）API 参考文档](https://main-api.flutter.dev/)
- [为 Flutter 做贡献](https://github.com/flutter/flutter/blob/main/CONTRIBUTING.md)

## 离线文档

除了上述在线站点之外，Flutter 的文档还可以下载为 HTML 文档 ZIP 文件，以便在离线或网络连接不佳时使用。

注意

离线文档文件相当大，压缩后约 300MB，解压后约 1GB。

离线 HTML 文档 ZIP 包：

- [稳定渠道](https://api.flutter.dev/offline/flutter.docs.zip)
- [主渠道](https://main-api.flutter.dev/offline/flutter.docs.zip)

此外，你也可以使用以下 XML 配置将 Flutter 添加到开源应用 [Zeal](https://zealdocs.org/) 中。请按照该应用中的说明添加 feed。

- 稳定渠道 Zeal XML 配置 URL：[api.flutter.dev/offline/flutter.xml](https://api.flutter.dev/offline/flutter.xml)
- 主渠道 Zeal XML 配置 URL：[main-api.flutter.dev/offline/flutter.xml](https://main-api.flutter.dev/offline/flutter.xml)

## 导入库

### 框架库

下方"库"部分（或左侧导航栏）中列出的库是 Flutter 核心框架的一部分，使用 `'package:flutter/<library>.dart'` 的方式导入，如下所示：

```dart
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
```

### Dart 库

"Dart" 部分中的库存在于 `dart:` 命名空间中，使用 `'dart:<library>'` 的方式导入，如下所示：

```dart
import 'dart:async';
import 'dart:ui';
```

除 `'dart:core'` 外，你必须先导入 Dart 库才能使用它。

### 支持库

其他部分中的库是随 Flutter 一起提供的支持库。它们按包进行组织，使用 `'package:<package>/<library>.dart'` 的方式导入，如下所示：

```dart
import 'package:flutter_test/flutter_test.dart';
import 'package:file/local.dart';
```

## pub.dev 上的包

Flutter 拥有丰富的包生态系统，这些包由 Flutter 团队和广泛的开源社区贡献到一个中央仓库中。在数以千计的包中，你可以找到对 Firebase、Google Fonts、蓝牙和摄像头等硬件服务、新组件和动画，以及与其他热门 Web 服务集成的支持。你可以在 [pub.dev](https://pub.dev/) 上浏览这些包。

## 库

- [animation](https://www.yuque.com/thyname/flutter.animation)

  Flutter 动画系统。

- [cupertino](https://www.yuque.com/thyname/flutter.cupertino)

  实现当前 iOS 设计语言的 Flutter 组件。

- [foundation](https://www.yuque.com/thyname/flutter.foundation)

  Flutter 框架的核心基元。

- [gestures](https://www.yuque.com/thyname/flutter.gestures)

  Flutter 手势识别器。

- [material](https://www.yuque.com/thyname/flutter.material)

  实现 Material Design 的 Flutter 组件。

- [painting](https://www.yuque.com/thyname/flutter.painting)

  Flutter 绘制库。

- [physics](https://www.yuque.com/thyname/flutter.physics)

  简单的一维物理模拟（如弹簧、摩擦力和重力），用于用户界面动画。

- [rendering](https://www.yuque.com/thyname/flutter.rendering)

  Flutter 渲染树。

- [scheduler](https://www.yuque.com/thyname/flutter.scheduler)

  Flutter 调度器（Scheduler）库。

- [semantics](https://www.yuque.com/thyname/flutter.semantics)

  Flutter 语义（semantics）包。

- [services](https://www.yuque.com/thyname/flutter.services)

  暴露给 Flutter 应用的平台服务。

- [widget_previews](https://www.yuque.com/thyname/flutter.widget_previews)

  Flutter 组件预览注解和数据类。

- [widgets](https://www.yuque.com/thyname/flutter.widgets)

  Flutter 组件（widgets）框架。

## Dart

- [dart:ui](https://www.yuque.com/thyname/dart.ui)

  Flutter 应用程序的内置类型和核心基元。
