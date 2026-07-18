# OrientationWidgetBuilder

```dart
typedef OrientationWidgetBuilder = Widget Function(BuildContext context, Orientation orientation)
```

用于根据 [Orientation](https://www.yuque.com/thyname/flutter.widgets/orientation) 构建组件的函数签名。

由 [OrientationBuilder.builder] 使用。

# OrientationBuilder

```dart
class OrientationBuilder extends StatelessWidget {}
```

构建一个可以依赖于父组件方向（orientation）的组件树（不同于设备方向）。

另请参阅：

- [LayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/layoutbuilder)，它暴露完整的约束条件，而不仅仅是方向。
- [CustomSingleChildLayout](https://www.yuque.com/thyname/flutter.widgets/customsinglechildlayout)，它在布局阶段定位其子组件。
- [CustomMultiChildLayout](https://www.yuque.com/thyname/flutter.widgets/custommultichildlayout)，借助它可以在布局阶段精确定义一组子组件的布局方式。
- [MediaQueryData.orientation]，它表明设备处于横屏还是竖屏模式。

### OrientationBuilder()

```dart
OrientationBuilder({dynamic key, required OrientationWidgetBuilder builder})
```

创建一个方向构建器（orientation builder）。

### builder

```dart
OrientationWidgetBuilder builder
```

根据此组件的方向，构建位于此组件之下的组件。

组件的方向取决于其宽度相对于高度的比例。例如，即使 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 组件将其子组件以纵向排列显示，只要其宽度超过高度，该组件仍会呈现横向（landscape）方向。

### build()

```dart
Widget build(BuildContext context)
```

# DeviceOrientationBuilder

```dart
class DeviceOrientationBuilder extends StatelessWidget {}
```

构建一个可以依赖于设备方向的组件树。

方向信息通过 [MediaQuery.orientationOf] 获取，该方法反映平台报告的实际设备方向。这确保了其与 [MediaQueryData.orientation] 的一致性，并能在可折叠设备等设备方向可能与布局尺寸不同的场景中表现正确。

这与 [OrientationBuilder](https://www.yuque.com/thyname/flutter.widgets/orientationbuilder) 不同，后者根据父组件的布局约束（宽度与高度的比较）来确定方向，而非设备的物理方向。

{@tool snippet} 此示例展示了如何使用 [DeviceOrientationBuilder](https://www.yuque.com/thyname/flutter.widgets/deviceorientationbuilder) 根据设备方向显示不同的组件。

```dart
DeviceOrientationBuilder(
  builder: (BuildContext context, Orientation orientation) {
    return Text(orientation == Orientation.portrait
        ? 'Device is in Portrait'
        : 'Device is in Landscape');
  },
)
```

{@end-tool}

此组件需要一个 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先节点才能获取方向信息。通常由 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 或 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 提供。

另请参阅：

- [OrientationBuilder](https://www.yuque.com/thyname/flutter.widgets/orientationbuilder)，它根据父组件的布局约束而非设备方向进行构建。
- [MediaQueryData.orientation]，它直接通过 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 提供设备方向。
- [LayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/layoutbuilder)，它暴露完整的布局约束条件。

### DeviceOrientationBuilder()

```dart
DeviceOrientationBuilder({dynamic key, required OrientationWidgetBuilder builder})
```

创建一个设备方向构建器（device orientation builder）。

### builder

```dart
OrientationWidgetBuilder builder
```

根据设备方向，构建位于此组件之下的组件。

方向信息通过 [MediaQuery.orientationOf] 获取，该方法反映平台报告的实际设备方向。
