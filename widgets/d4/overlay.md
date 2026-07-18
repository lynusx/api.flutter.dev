# OverlayChildLayoutBuilder

```dart
typedef OverlayChildLayoutBuilder = Widget Function(BuildContext context, OverlayChildLayoutInfo info)
```

[OverlayPortal.overlayChildLayoutBuilder] 中使用的组件构建器回调的签名。

# OverlayChildLayoutInfo

```dart
extension type OverlayChildLayoutInfo._((Size childSize, Matrix4 childPaintTransform, Size overlaySize) _info) {}
```

[OverlayPortal.overlayChildLayoutBuilder] 回调可用的附加布局信息。

### childSize

```dart
Size get childSize
```

[OverlayPortal.child] 在其自身坐标系中的尺寸。

### childPaintTransform

```dart
Matrix4 get childPaintTransform
```

[OverlayPortal.child] 在目标 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 坐标系中的绘制变换。

### overlaySize

```dart
Size get overlaySize
```

目标 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 在其自身坐标系中的尺寸。

# OverlayEntry

```dart
class OverlayEntry implements Listenable {}
```

[Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中可以容纳一个组件的位置。

Overlay entry 使用 [OverlayState.insert] 或 [OverlayState.insertAll] 函数插入到 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中。若要查找给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 最近的封闭 overlay，可使用 [Overlay.of] 函数。

一个 overlay entry 在同一时间最多只能属于一个 overlay。若要从其 overlay 中移除某个 entry，可对该 overlay entry 调用 [remove] 函数。

由于 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 使用 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 布局，overlay entry 可以使用 [Positioned](https://www.yuque.com/thyname/flutter.widgets/positioned) 和 [AnimatedPositioned](https://www.yuque.com/thyname/flutter.widgets/animatedpositioned) 在 overlay 中定位自身。

例如，[Draggable](https://www.yuque.com/thyname/flutter.widgets/draggable) 使用 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 来显示拖动开始后跟随用户手指移动的拖动化身（drag avatar）。使用 overlay 来显示拖动化身，可以让该化身悬浮在应用中的其他组件之上。当用户的手指移动时，draggable 会对 overlay entry 调用 [markNeedsBuild]，使其重新构建。在其构建过程中，该 entry 包含一个 [Positioned](https://www.yuque.com/thyname/flutter.widgets/positioned)，其 top 和 left 属性被设置为使拖动化身靠近用户的手指定位。当拖动结束时，[Draggable](https://www.yuque.com/thyname/flutter.widgets/draggable) 会将该 entry 从 overlay 中移除，从而将拖动化身从视图中移除。

默认情况下，如果在此 entry 之上存在一个完全 [opaque]（不透明）的 entry，则此 entry 将不会包含在组件树中（特别是，该 overlay entry 内的有状态组件将不会被实例化）。若要确保即使不可见时你的 overlay entry 仍会被构建，可将 [maintainState] 设置为 true。这样做的开销更大，因此应谨慎使用。特别是，如果将 [maintainState] 设置为 true 的 overlay entry 内的组件反复调用 [State.setState]，将会不必要地消耗用户的电量。

[OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 是一个 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable)，会在 [builder] 构建的组件被挂载或卸载时通知监听者，其确切状态可通过 [mounted] 查询。在 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 的所有者调用 [remove] 之后再调用 [dispose]，该组件可能不会立即从组件树中移除。因此，[OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 的监听者在 [dispose] 调用之后、组件最终被卸载时，仍可能会收到最后一次通知。

{@macro flutter.widgets.overlayPortalVsOverlayEntry}

另请参阅：

- [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal)，一种使用构建器回调将组件插入 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 的替代 API。
- [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay)，可独立管理的一组 entry 构成的堆栈。
- [OverlayState](https://www.yuque.com/thyname/flutter.widgets/overlaystate)，Overlay 的当前状态。
- [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp)，一个封装了应用程序通常所需的若干组件的便捷组件。
- [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp)，一个封装了 Material Design 应用程序通常所需的若干组件的便捷组件。

### OverlayEntry()

```dart
OverlayEntry({required WidgetBuilder builder, bool opaque = false, bool maintainState = false, bool canSizeOverlay = false})
```

创建一个 overlay entry。

要将该 entry 插入到 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中，首先使用 [Overlay.of] 找到该 overlay，然后调用 [OverlayState.insert]。要移除该 entry，可对该 overlay entry 本身调用 [remove]。

### builder

```dart
WidgetBuilder builder
```

该 entry 会将此构建器所构建的组件包含在其所在位置的 overlay 中。

要使此构建器被再次调用，可对该 overlay entry 调用 [markNeedsBuild]。

### opaque

```dart
bool get opaque
```

此 entry 是否遮挡整个 overlay。

如果一个 entry 声明自己是不透明的，那么为了提高效率，overlay 将跳过构建该 entry 下方的其他 entry，除非它们设置了 [maintainState]。

### opaque

```dart
set opaque(bool value)
```

### maintainState

```dart
bool get maintainState
```

即使在此 entry 之上存在一个完全 [opaque] 的 entry，此 entry 是否仍必须包含在组件树中。

默认情况下，如果在此 entry 之上存在一个完全 [opaque] 的 entry，则此 entry 将不会包含在组件树中（特别是，该 overlay entry 内的有状态组件将不会被实例化）。若要确保即使不可见时你的 overlay entry 仍会被构建，可将 [maintainState] 设置为 true。这样做的开销更大，因此应谨慎使用。特别是，如果将 [maintainState] 设置为 true 的 overlay entry 内的组件反复调用 [State.setState]，将会不必要地消耗用户的电量。

[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 和 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 对象使用此属性来确保即使路由处于后台，也能保持存在，从而使后续路由所承诺的 [Future](https://www.yuque.com/thyname/dart.async/future) 在完成时能被正确处理。

### maintainState

```dart
set maintainState(bool value)
```

### canSizeOverlay

```dart
bool canSizeOverlay
```

此 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 的内容是否可用于确定 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 的尺寸。

在大多数情况下，overlay 会根据其传入的约束将自身调整为尽可能大的尺寸。但是，如果这样做会导致无限大的尺寸，它就必须依靠其中一个子组件来确定自身的尺寸。在这种情况下，overlay 会查询将此属性设置为 true 的、层级最高的非 [Positioned](https://www.yuque.com/thyname/flutter.widgets/positioned) overlay entry，使用 overlay 传入的 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints) 对其进行布局，并强制所有其他非 [Positioned](https://www.yuque.com/thyname/flutter.widgets/positioned) overlay entry 具有相同的尺寸。[Positioned](https://www.yuque.com/thyname/flutter.widgets/positioned) entry 仍会像往常一样根据计算出的 overlay 尺寸进行布局。

将此属性设置为 true 的 overlay entry 必须能够处理不受约束的 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints)。

如果该 overlay entry 使用 [Positioned](https://www.yuque.com/thyname/flutter.widgets/positioned) 组件在 overlay 中定位自身，则将此属性设置为 true 不会产生任何效果。

### mounted

```dart
bool get mounted
```

[OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 当前是否已挂载到组件树中。

当此值发生变化时，[OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 会通知其监听者。

### addListener()

```dart
void addListener(VoidCallback listener)
```

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

### remove()

```dart
void remove()
```

将此 entry 从 overlay 中移除。

此方法只能被调用一次。

此方法会立即将此 overlay entry 从 overlay 中移除。如果在本帧的 overlay 重建之前调用此方法，UI 将在同一帧内更新；否则，UI 将在下一帧更新。这意味着在构建过程中调用此方法是安全的，但如果在 overlay 重建之后调用，UI 将不会更新，直到下一帧（即许多毫秒之后）。

### markNeedsBuild()

```dart
void markNeedsBuild()
```

使此 entry 在下一次管线刷新（pipeline flush）时重新构建。

如果 [builder] 的输出发生了变化，则需要调用此函数。

### dispose()

```dart
void dispose()
```

释放此 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 所使用的资源。

如果该 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 已插入到 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中，则必须先调用 [remove] 方法，然后才能调用此方法。

调用此方法后，该对象将不再处于可用状态，应当被丢弃（在该对象被释放后调用 [addListener] 将会抛出异常）。但是，已注册的监听者可能不会立即被释放，直到使用此 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 构建的组件从组件树中卸载为止。

此方法只能由该对象的所有者调用。

### toString()

```dart
String toString()
```

# Overlay

```dart
class Overlay extends StatefulWidget {}
```

可独立管理的一组 entry 构成的堆栈。

Overlay 让独立的子组件可以通过将视觉元素插入到 overlay 的堆栈中，实现在其他组件之上“悬浮”显示。overlay 让这些组件中的每一个都可以使用 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 对象来管理自己在 overlay 中的参与情况。

尽管你可以直接创建一个 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay)，但更常见的做法是使用 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp)、[CupertinoApp](https://www.yuque.com/thyname/flutter.cupertino/cupertinoapp) 或 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 中由 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 创建的 overlay。navigator 使用其 overlay 来管理其路由的视觉呈现。

[Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 组件使用一种与 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 组件非常相似的自定义堆栈实现。[Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 的主要用例与导航相关，即能够在应用中的页面之上插入组件。对于与导航无关的布局用途，请考虑改用 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack)。

[Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 组件需要在组件树中存在一个作用域内的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 组件，以便能够解析其任何 [Positioned.directional] 子组件的方向敏感坐标。

对于在 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 中绘制的组件，不要假设 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 的尺寸就是 [MediaQuery.sizeOf] 返回的尺寸。嵌套的 overlay 可以具有不同的尺寸。

{@tool dartpad} 此示例展示了如何使用 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 来高亮显示 [NavigationBar](https://www.yuque.com/thyname/flutter.material/navigationbar) 的目的地（destination）。

** See code in examples/api/lib/widgets/overlay/overlay.0.dart ** {@end-tool}

另请参阅：

- [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry)，用于描述 overlay entry 的类。
- [OverlayState](https://www.yuque.com/thyname/flutter.widgets/overlaystate)，用于将 entry 插入到 overlay 中。
- [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp)，通过其 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 间接插入 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 组件。
- [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp)，通过其 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 间接插入 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 组件。
- [CupertinoApp](https://www.yuque.com/thyname/flutter.cupertino/cupertinoapp)，通过其 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 间接插入 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 组件。
- [Stack](https://www.yuque.com/thyname/flutter.widgets/stack)，允许直接显示一组堆叠的组件。

### Overlay()

```dart
Overlay({dynamic key, List<OverlayEntry> initialEntries = const <OverlayEntry>[], Clip clipBehavior = Clip.hardEdge, bool alwaysSizeToContent = false})
```

创建一个 overlay。

初始 entry 将在其关联的 [OverlayState](https://www.yuque.com/thyname/flutter.widgets/overlaystate) 初始化时被插入到 overlay 中。

与其创建一个新的 overlay，不如考虑为应用程序使用 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp)、[CupertinoApp](https://www.yuque.com/thyname/flutter.cupertino/cupertinoapp) 或 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 所创建的 overlay。

### wrap()

```dart
Widget wrap({Key? key, Clip clipBehavior = Clip.hardEdge, bool alwaysSizeToContent = false, required Widget child})
```

将提供的 `child` 包裹在一个 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中，以便其他视觉元素（打包在 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 中）可以悬浮在该 child 之上。

这是对常规 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 构造函数的一种便捷封装：它会创建一个 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay)，并将提供的 `child` 放置在这个新创建的 Overlay 底部的一个 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 中。

### initialEntries

```dart
List<OverlayEntry> initialEntries
```

最初包含在 overlay 中的 entry。

这些 entry 仅在 [OverlayState](https://www.yuque.com/thyname/flutter.widgets/overlaystate) 初始化时使用。如果你为已经存在于组件树中的 overlay 提供了新的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 描述，则新的 entry 将被忽略。

要向已经存在于组件树中的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 添加 entry，请使用 [Overlay.of] 获取 [OverlayState](https://www.yuque.com/thyname/flutter.widgets/overlaystate)（或为 Overlay 组件分配一个 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey)，并通过 [GlobalKey.currentState] 获取 [OverlayState](https://www.yuque.com/thyname/flutter.widgets/overlaystate)），然后使用 [OverlayState.insert] 或 [OverlayState.insertAll]。

要从 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中移除某个 entry，请使用 [OverlayEntry.remove]。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

默认值为 [Clip.hardEdge]。

### alwaysSizeToContent

```dart
bool alwaysSizeToContent
```

确定 overlay 是否应始终根据内容调整自身尺寸。

通常情况下，overlay 只有在传入约束为无限大且存在一个可以确定 overlay 尺寸的 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 时，才会根据内容调整尺寸。将此项设置为 `true` 会强制启用此行为，即使传入约束是有限的（但可能是宽松的）。

将此项设置为 true 需要一个能够根据自身确定 overlay 尺寸的 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry)（即 [OverlayEntry.canSizeOverlay] 设置为 true）。如果未提供此类 entry，则会抛出异常。

### of()

```dart
OverlayState of(BuildContext context, {bool rootOverlay = false, Widget? debugRequiredFor})
```

在最近的 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 范围内，从最近的封闭给定 context 的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 实例中获取 [OverlayState](https://www.yuque.com/thyname/flutter.widgets/overlaystate)；在调试模式下，如果找不到该实例，将抛出异常。

在调试模式下，如果提供了 `debugRequiredFor` 参数且未找到 overlay，则此函数将抛出一个异常，该异常在错误信息中包含给定组件的运行时类型。该异常试图说明调用方组件（即 `debugRequiredFor` 参数所指定的组件）需要一个 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 才能正常工作。如果未提供 `debugRequiredFor`，则错误信息会更为通用。

典型用法如下：

```dart
OverlayState overlay = Overlay.of(context);
```

{@template flutter.widgets.Overlay.of} 如果 `rootOverlay` 设置为 true，则会改为返回距离最远的此类实例的状态。这对于在所有后续的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 实例之上安装 overlay entry 很有用。{@endtemplate}

另请参阅：

- [Overlay.maybeOf]，一个类似的函数，如果找不到 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 则返回 null。

### maybeOf()

```dart
OverlayState? maybeOf(BuildContext context, {bool rootOverlay = false})
```

在最近的 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 范围内，从最近的封闭给定 context 的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 实例中获取 [OverlayState](https://www.yuque.com/thyname/flutter.widgets/overlaystate)（如果存在的话）。

典型用法如下：

```dart
OverlayState? overlay = Overlay.maybeOf(context);
```

{@macro flutter.widgets.Overlay.of}

另请参阅：

- [Overlay.of]，一个类似的函数，返回一个不可为空的结果，如果找不到 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 则抛出异常。

### createState()

```dart
OverlayState createState()
```

# OverlayState

```dart
class OverlayState extends State<Overlay> with TickerProviderStateMixin {}
```

[Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 的当前状态。

用于通过 [insert] 和 [insertAll] 函数将 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 插入到 overlay 中。

### initState()

```dart
void initState()
```

### insert()

```dart
void insert(OverlayEntry entry, {OverlayEntry? below, OverlayEntry? above})
```

将给定的 entry 插入到 overlay 中。

如果 `below` 非空，则该 entry 将被插入到 `below` 的正下方。如果 `above` 非空，则该 entry 将被插入到 `above` 的正上方。否则，该 entry 将被插入到最上层。

同时指定 `above` 和 `below` 是错误的用法。

### insertAll()

```dart
void insertAll(Iterable<OverlayEntry> entries, {OverlayEntry? below, OverlayEntry? above})
```

插入给定可迭代对象中的所有 entry。

如果 `below` 非空，则这些 entry 将被插入到 `below` 的正下方。如果 `above` 非空，则这些 entry 将被插入到 `above` 的正上方。否则，这些 entry 将被插入到最上层。

同时指定 `above` 和 `below` 是错误的用法。

### rearrange()

```dart
void rearrange(Iterable<OverlayEntry> newEntries, {OverlayEntry? below, OverlayEntry? above})
```

移除给定可迭代对象中列出的所有 entry，然后按照给定的顺序将它们重新插入到 overlay 中。

在 `newEntries` 中提及但不存在于 overlay 中的 entry，将按照 [insertAll] 的方式被插入。

未在 `newEntries` 中提及、但存在于 overlay 中的 entry，将作为一个整体，相对于被移动的 entry，按照 `below` 或 `above` 之一指定的方式在结果列表中定位；如果指定了 `below` 或 `above`，则它们必须是 `newEntries` 中的某个 entry：

如果 `below` 非空，则该组 entry 将被定位在 `below` 的正下方。如果 `above` 非空，则该组 entry 将被定位在 `above` 的正上方。否则，该组 entry 将保留在最上层，所有被重新排列的 entry 都位于其下方。

同时指定 `above` 和 `below` 是错误的用法。

### debugIsVisible()

```dart
bool debugIsVisible(OverlayEntry entry)
```

（仅限调试）检查给定的 entry 是否可见（即未被不透明的 entry 遮挡）。

这是一个 O(N) 的算法，除了调试断言之外不应有其他必要用途。为避免有人依赖它，此函数仅在调试模式下实现，在发布模式下始终返回 false。

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# OverlayPortalController

```dart
class OverlayPortalController {}
```

用于显示、隐藏和将 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 的 overlay 子组件置于最上层的类，作用于目标 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay)。

一个 [OverlayPortalController](https://www.yuque.com/thyname/flutter.widgets/overlayportalcontroller) 在同一时间最多只能提供给一个 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal)。当一个 [OverlayPortalController](https://www.yuque.com/thyname/flutter.widgets/overlayportalcontroller) 从一个 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 移动到另一个时，其 [isShowing] 状态不会被保留。

[OverlayPortalController.show] 和 [OverlayPortalController.hide] 可以在控制器被分配给任何 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 之前调用，但通常不应在组件树正在重建时调用它们。

### OverlayPortalController()

```dart
OverlayPortalController({String? debugLabel})
```

创建一个 [OverlayPortalController](https://www.yuque.com/thyname/flutter.widgets/overlayportalcontroller)，可以选择性地提供一个字符串标识符 `debugLabel`。

### show()

```dart
void show()
```

显示此控制器所关联的 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 的 overlay 子组件，将其置于目标 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 的最上层。

当有多个 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 以同一个 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 为目标时，最后一个调用 [show] 的 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 的 overlay 子组件将出现在最顶层，不受遮挡。

如果 [isShowing] 已经为 true，则调用此方法会将其控制的 overlay 子组件置于最上层。

此方法通常不应在组件树正在重建时调用。

### hide()

```dart
void hide()
```

隐藏 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 的 overlay 子组件。

一旦隐藏，overlay 子组件将在组件树下一次重建时从组件树中移除，有状态组件可能因此丢失其状态。

此方法通常不应在组件树正在重建时调用。

### isShowing

```dart
bool get isShowing
```

此控制器所关联的 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 是否应该使用其 `overlayChildBuilder` 构建并显示其 overlay 子组件。

### toggle()

```dart
void toggle()
```

用于切换当前 [isShowing] 状态的便捷方法。

此方法通常不应在组件树正在重建时调用。

### toString()

```dart
String toString()
```

# OverlayChildLocation

```dart
enum OverlayChildLocation {}
```

[OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 用于渲染其 overlay 子组件的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 所在的位置。

这通常在 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 中使用。

[OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 会在组件树中距离自身最近的祖先 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 上渲染其 overlay 子组件。

[OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 会在组件树中最顶层的根 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 上渲染其 overlay 子组件。

在多视图应用的情况下，根 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 指的是 View 下方的第一个 Overlay。

# OverlayPortal

```dart
class OverlayPortal extends StatefulWidget {}
```

一个将其 overlay 子组件渲染到 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 上的组件。

在对关联的 [controller] 调用 [OverlayPortalController.show] 之前，overlay 子组件最初处于隐藏状态。[OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 使用 [overlayChildBuilder] 构建其 overlay 子组件，并将其渲染到指定的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 上，效果如同使用 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 插入一样，同时它可以依赖与此组件相同的一组 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)（例如 [Theme](https://www.yuque.com/thyname/flutter.material/theme)）。

此组件在其 overlay 子组件显示时，需要在组件树中存在一个 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 祖先。overlay 子组件由 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 祖先渲染，而非由该组件自身渲染。这使得 overlay 子组件可以悬浮在其他组件之上，而不受其在组件树中位置的限制。

当调用 [OverlayPortalController.hide] 时，使用 [overlayChildBuilder] 构建的组件将在组件树下一次重建时被移除。overlay 子组件树中的有状态后代组件可能因此丢失状态。

{@tool dartpad} 此示例使用 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 构建了一个工具提示（tooltip），当用户点击 [child] 组件时该提示会变为可见。[OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 上方有一个 [DefaultTextStyle](https://www.yuque.com/thyname/flutter.widgets/defaulttextstyle)，用于控制 [child] 组件和 [overlayChildBuilder] 所构建的组件两者的 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle)；如果该工具提示是作为 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 添加的，则无法以其他方式实现这一点。

** See code in examples/api/lib/widgets/overlay/overlay_portal.0.dart ** {@end-tool}

### 绘制顺序

在一个 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中，overlay 子组件会在其 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 所关联的 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry)（即组件树中距离该 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 最近的 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry)，通常代表封闭的 [Route](https://www.yuque.com/thyname/flutter.widgets/route)）之后、下一个 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 之前进行绘制。

当一个 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 关联了多个 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 时，它们的 overlay 子组件之间的绘制顺序由调用 [OverlayPortalController.show] 的顺序决定。最后一个调用 `show` 的 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 会将其 overlay 子组件绘制在前景中。

### 语义（Semantics）

由 overlay 子组件生成的语义子树被视为附属于 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal)，而非目标 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay)。由于不可见性，[OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 的语义子树可能会从语义树中被移除（例如，当 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 在 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview) 中完全不可见，但由于 [KeepAlive](https://www.yuque.com/thyname/flutter.widgets/keepalive) 组件而被保持存活时）。发生这种情况时，即使 overlay 子组件在屏幕上仍然可见，由其生成的语义子树也会一并被移除。

{@template flutter.widgets.overlayPortalVsOverlayEntry}

### [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 与 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 的区别

[OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 与 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 之间的主要区别在于：[OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 将其组件子树构建为目标 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 的子组件，而 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 使用 [OverlayPortal.overlayChildBuilder] 构建其自身的子组件。这使得 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 的 overlay 子组件可以依赖与 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 相同的一组 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)，并且还能保证 overlay 子组件的生命周期不会超出其 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal)。

另一方面，[OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 的实现更为复杂。例如，在全局键（global key）重新父级化过程中，它比常规组件做了更多的工作。如果要在 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 上显示的内容并不需要成为 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 子树的一部分，可以考虑改用 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry)。{@endtemplate}

另请参阅：

- [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry)，用于将组件插入 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 的另一种 API。
- [Positioned](https://www.yuque.com/thyname/flutter.widgets/positioned)，可用于相对于目标 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 的边界对 overlay 子组件进行尺寸设置和定位。
- [CompositedTransformFollower](https://www.yuque.com/thyname/flutter.widgets/compositedtransformfollower)，可用于相对于链接的 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 组件对 overlay 子组件进行定位。

### OverlayPortal()

```dart
OverlayPortal({dynamic key, required OverlayPortalController controller, required WidgetBuilder overlayChildBuilder, OverlayChildLocation overlayLocation = OverlayChildLocation.nearestOverlay, Widget? child})
```

创建一个 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal)，当调用 [OverlayPortalController.show] 时，将 [overlayChildBuilder] 构建的组件渲染到最近的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 上。

[overlayLocation] 设置此组件将 [overlayChildBuilder] 返回的组件附加到哪个 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay)。默认值为 [OverlayChildLocation.nearestOverlay]。

### OverlayPortal.targetsRootOverlay()

```dart
OverlayPortal.targetsRootOverlay({dynamic key, required OverlayPortalController controller, required WidgetBuilder overlayChildBuilder, Widget? child})
```

创建一个 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal)，当调用 [OverlayPortalController.show] 时，将 [overlayChildBuilder] 构建的组件渲染到根 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 上。

### OverlayPortal.overlayChildLayoutBuilder()

```dart
OverlayPortal.overlayChildLayoutBuilder({Key? key, required OverlayPortalController controller, required OverlayChildLayoutBuilder overlayChildBuilder, OverlayChildLocation overlayLocation = OverlayChildLocation.nearestOverlay, required Widget? child})
```

创建一个 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal)，当调用 [OverlayPortalController.show] 时，将 `overlayChildBuilder` 构建的组件渲染到最近的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 上。

开发者可以使用 `overlayChildBuilder`，根据 [OverlayPortal.child] 在目标 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中的尺寸和位置，以及 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 自身的尺寸，来配置 overlay 子组件。这使得 overlay 子组件例如可以始终跟随 [OverlayPortal.child]，同时根据其与 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 边缘的距离来调整自身的尺寸。

`overlayChildBuilder` 回调在布局期间被调用。为确保届时 [OverlayPortal.child] 相对于目标 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 的绘制变换是最新的，[OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 与目标 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 之间的所有 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 都必须在布局阶段确定其绘制变换，大多数 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 都会这样做。一个例外是 [CompositedTransformFollower](https://www.yuque.com/thyname/flutter.widgets/compositedtransformfollower) 组件，其 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 仅在合成（composited）时才确定绘制变换。在 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 和 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 之间放置 [CompositedTransformFollower](https://www.yuque.com/thyname/flutter.widgets/compositedtransformfollower)，可能会导致向 `overlayChildBuilder` 提供不正确的子组件绘制变换，并会在调试模式下引发断言。

[overlayLocation] 设置此组件将 `overlayChildBuilder` 返回的组件附加到哪个 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay)。默认值为 [OverlayChildLocation.nearestOverlay]。

### controller

```dart
OverlayPortalController controller
```

用于显示、隐藏和将 overlay 子组件置于最上层的控制器。

### overlayChildBuilder

```dart
WidgetBuilder overlayChildBuilder
```

一个 [WidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/widgetbuilder)，用于构建位于此组件下方组件树中的一个组件，该组件将渲染在最近的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 上。

只有在对关联的 [controller] 调用 [OverlayPortalController.show] 之后，上述构建的组件才会被构建并显示在最近的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中。它将被绘制在组件树中距离此组件最近的 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry)（通常是封闭的 Route）的前面。

所构建的 overlay 子组件被插入到组件树中此组件的下方，使其可以依赖于其上方的 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)，并在这些 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 发生变化时收到通知。

与 [child] 不同，构建出的 overlay 子组件可以在视觉上超出此组件的边界而不会被裁剪，并且可以在此组件边界之外接收命中测试（hit-test）事件，只要它没有超出其所渲染的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 的边界。

### child

```dart
Widget? child
```

位于此组件下方组件树中的一个组件。

### overlayLocation

```dart
OverlayChildLocation overlayLocation
```

[overlayChildBuilder] 返回的组件所附加到的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay)。
