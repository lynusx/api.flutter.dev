@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

# PageTransitionsBuilder

```dart
abstract class PageTransitionsBuilder {}
```

为 [PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute) 定义页面切换动画。

PageTransitionsBuilder 可直接与任意设计体系中的 widget 层基础组件一起使用。自定义的 [PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute) 子类可以接受一个 PageTransitionsBuilder，并在重写 [ModalRoute.buildTransitions] 时委托给其 [buildTransitions] 方法。这样便可以创建可复用的过渡动画，并与 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 及其他导航基础组件配合使用。

## 用法示例

{@tool dartpad} 此示例展示了如何创建一个自定义的 [PageTransitionsBuilder](https://www.yuque.com/thyname/flutter.widgets/pagetransitionsbuilder)，使新页面在滑入的同时从右侧淡入，并展示了如何将其与自定义的 [PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute) 配合使用。

** See code in examples/api/lib/widgets/page_transitions_builder/page_transitions_builder.0.dart ** {@end-tool}

作为用法示例，在 Material 库中，[PageTransitionsTheme](https://www.yuque.com/thyname/flutter.material/pagetransitionstheme) 使用此类来定义 [MaterialPageRoute](https://www.yuque.com/thyname/flutter.material/materialpageroute) 的页面切换动画。应用可以为 [ThemeData.pageTransitionsTheme] 配置构建器映射表，以自定义不同平台上 [MaterialPageRoute](https://www.yuque.com/thyname/flutter.material/materialpageroute) 的默认页面切换动画。

另请参阅：

- [PageTransitionsTheme](https://www.yuque.com/thyname/flutter.material/pagetransitionstheme)，使用此类配置页面切换动画。
- [MaterialPageRoute](https://www.yuque.com/thyname/flutter.material/materialpageroute)，使用此类构建其过渡动画。
- [FadeUpwardsPageTransitionsBuilder](https://www.yuque.com/thyname/flutter.widgets/fadeupwardspagetransitionsbuilder)，定义了一种与 Android O 提供的效果类似的页面切换动画。
- [OpenUpwardsPageTransitionsBuilder](https://www.yuque.com/thyname/flutter.widgets/openupwardspagetransitionsbuilder)，定义了一种与 Android P 提供的效果类似的页面切换动画。
- [ZoomPageTransitionsBuilder](https://www.yuque.com/thyname/flutter.material/zoompagetransitionsbuilder)，定义了默认的页面切换动画，与 Android Q 中提供的效果类似。
- [CupertinoPageTransitionsBuilder](https://www.yuque.com/thyname/flutter.cupertino/cupertinopagetransitionsbuilder)，定义了一种与原生 iOS 页面切换效果一致的水平过渡动画。
- [FadeForwardsPageTransitionsBuilder](https://www.yuque.com/thyname/flutter.material/fadeforwardspagetransitionsbuilder)，定义了一种与 Android U 提供的效果类似的页面切换动画。

### PageTransitionsBuilder()

```dart
PageTransitionsBuilder()
```

抽象的 const 构造函数。此构造函数使子类能够提供 const 构造函数，从而可在 const 表达式中使用。

### delegatedTransition

```dart
DelegatedTransitionBuilder? get delegatedTransition
```

为前一个路由提供一个附加的过渡动画。

{@macro flutter.widgets.delegatedTransition}

### transitionDuration

```dart
Duration get transitionDuration
```

{@macro flutter.widgets.TransitionRoute.transitionDuration}

默认为 300 毫秒。

### reverseTransitionDuration

```dart
Duration get reverseTransitionDuration
```

{@macro flutter.widgets.TransitionRoute.reverseTransitionDuration}

默认为 300 毫秒。

### buildTransitions()

```dart
Widget buildTransitions<T>(PageRoute<T> route, BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```

用一个或多个过渡组件包装 child，用于定义 [route] 如何进入和离开屏幕。

子类应重写此方法以创建过渡动画。

[MaterialPageRoute.buildTransitions] 方法就是使用此方法构建过渡动画的一个示例。它通过 `Theme.of(context).pageTransitionsTheme` 查找当前的 [PageTransitionsTheme](https://www.yuque.com/thyname/flutter.material/pagetransitionstheme)，并根据主题的 [ThemeData.platform] 委托给基于该平台的 [PageTransitionsBuilder](https://www.yuque.com/thyname/flutter.widgets/pagetransitionsbuilder) 来调用此方法。

# FadeUpwardsPageTransitionsBuilder

```dart
class FadeUpwardsPageTransitionsBuilder extends PageTransitionsBuilder {}
```

一种页面切换构建器，通过淡入并向上滑动来为新进入的页面添加动画效果。

此过渡动画结合了两种动画：

- 使用缓入（ease-in）曲线实现的淡入效果
- 从屏幕顶部下方 25% 处开始的向上滑动

最终形成的动画效果是：新页面在逐渐显现的同时向上升起，呈现出流畅的进场效果。

另请参阅：

- [OpenUpwardsPageTransitionsBuilder](https://www.yuque.com/thyname/flutter.widgets/openupwardspagetransitionsbuilder)，定义了一种与 Android P 提供的效果类似的页面切换动画。
- [ZoomPageTransitionsBuilder](https://www.yuque.com/thyname/flutter.material/zoompagetransitionsbuilder)，定义了默认的页面切换动画，与 Android Q 中提供的效果类似。
- [CupertinoPageTransitionsBuilder](https://www.yuque.com/thyname/flutter.cupertino/cupertinopagetransitionsbuilder)，定义了一种与原生 iOS 页面切换效果一致的水平过渡动画。
- [PredictiveBackPageTransitionsBuilder](https://www.yuque.com/thyname/flutter.material/predictivebackpagetransitionsbuilder)，定义了一种页面切换动画，可在 Android U 及以上版本中提供预览当前路由背后内容的效果。

### FadeUpwardsPageTransitionsBuilder()

```dart
FadeUpwardsPageTransitionsBuilder()
```

构造一个使页面向上滑入的页面切换动画。

### buildTransitions()

```dart
Widget buildTransitions<T>(PageRoute<T>? route, BuildContext? context, Animation<double> animation, Animation<double>? secondaryAnimation, Widget child)
```

# OpenUpwardsPageTransitionsBuilder

```dart
class OpenUpwardsPageTransitionsBuilder extends PageTransitionsBuilder {}
```

一种页面切换构建器，通过自下而上的裁剪效果将新进入的页面呈现出来，为其添加动画效果。

此过渡动画结合了多种动画：

- 一种裁剪动画，逐步自下而上地显现新页面
- 新页面的轻微向上滑动（平移 5%）
- 旧页面的轻微向上移动（平移 2.5%）
- 背景的渐暗遮罩效果

最终形成的动画效果呈现出层叠感：新页面看起来像是从屏幕底部向上展开，而前一个页面则略微向后滑动。

另请参阅：

- [FadeUpwardsPageTransitionsBuilder](https://www.yuque.com/thyname/flutter.widgets/fadeupwardspagetransitionsbuilder)，定义了一种与 Android O 提供的效果类似的页面切换动画。
- [ZoomPageTransitionsBuilder](https://www.yuque.com/thyname/flutter.material/zoompagetransitionsbuilder)，定义了默认的页面切换动画，与 Android Q 中提供的效果类似。
- [CupertinoPageTransitionsBuilder](https://www.yuque.com/thyname/flutter.cupertino/cupertinopagetransitionsbuilder)，定义了一种与原生 iOS 页面切换效果一致的水平过渡动画。
- [PredictiveBackPageTransitionsBuilder](https://www.yuque.com/thyname/flutter.material/predictivebackpagetransitionsbuilder)，定义了一种页面切换动画，可在 Android 上提供预览当前路由背后内容的效果。
- [FadeForwardsPageTransitionsBuilder](https://www.yuque.com/thyname/flutter.material/fadeforwardspagetransitionsbuilder)，定义了一种与 Android U 提供的效果类似的页面切换动画。

### OpenUpwardsPageTransitionsBuilder()

```dart
OpenUpwardsPageTransitionsBuilder()
```

构造一个与 Android P 所用效果一致的页面切换动画。
