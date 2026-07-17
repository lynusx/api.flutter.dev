# ObjectKey

```dart
class ObjectKey extends LocalKey {}
```

一个通过其值所使用的对象获取自身标识的键（key）。

用于将某个 widget 的标识与用来生成该 widget 的对象的标识绑定在一起。

另请参阅：

- [Key](https://www.yuque.com/thyname/flutter.foundation/key)，所有键的基类。
- [Widget.key] 处的讨论，了解 widget 如何使用键的更多信息。

### ObjectKey()

```dart
ObjectKey(Object? value)
```

创建一个键，该键在其 [operator==] 中对 [value] 使用 [identical](https://www.yuque.com/thyname/dart.core/identical) 进行比较。

### value

```dart
Object? value
```

该键的 [operator==] 所使用的对象标识。

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# GlobalKey

```dart
abstract class GlobalKey<T extends State<StatefulWidget>> extends Key {}
```

在整个应用中唯一的键。

全局键（Global key）唯一地标识 element。全局键提供对与这些 element 相关联的其他对象的访问，例如 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)。对于 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget)，全局键还提供对 [State](https://www.yuque.com/thyname/flutter.widgets/state) 的访问。

拥有全局键的 widget，在从树中的一个位置移动到另一个位置时会重新挂载（reparent）其子树。为了重新挂载其子树，widget 必须在其从旧位置移除的同一动画帧内到达新位置。

使用全局键重新挂载 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 的开销相对较大，因为该操作会触发对相关联的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 及其所有子孙调用 [State.deactivate]；然后强制所有依赖某个 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 的 widget 重建。

如果不需要上述功能，请考虑改用 [Key](https://www.yuque.com/thyname/flutter.foundation/key)、[ValueKey](https://www.yuque.com/thyname/flutter.foundation/valuekey)、[ObjectKey](https://www.yuque.com/thyname/flutter.widgets/objectkey) 或 [UniqueKey](https://www.yuque.com/thyname/flutter.foundation/uniquekey)。

不能同时在树中包含两个具有相同全局键的 widget。这样做会在运行时触发断言。

## 陷阱

不应在每次构建时重新创建 GlobalKey。它们通常应该是由 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象持有的长期存在的对象。

在每次构建时创建新的 GlobalKey，会丢弃与旧键关联的子树状态，并为新键创建一个全新的子树。这样做不仅会影响性能，还可能导致子树中的 widget 出现意外行为。例如，子树中的 [GestureDetector](https://www.yuque.com/thyname/flutter.widgets/gesturedetector) 将无法追踪正在进行的手势，因为它会在每次构建时被重新创建。

正确的做法是让 State 对象持有该 GlobalKey，并在 build 方法之外实例化它，例如在 [State.initState] 中。

另请参阅：

- [Widget.key] 处的讨论，了解 widget 如何使用键的更多信息。

### GlobalKey()

```dart
GlobalKey({String? debugLabel})
```

创建一个 [LabeledGlobalKey](https://www.yuque.com/thyname/flutter.widgets/labeledglobalkey)，它是带有调试标签的 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey)。

该标签仅用于调试，不用于比较键的标识。

### GlobalKey.constructor()

```dart
GlobalKey.constructor()
```

创建一个不带标签的全局键。

由子类使用，因为工厂构造函数会遮蔽隐式构造函数。

### currentContext

```dart
BuildContext? get currentContext
```

拥有此键的 widget 所在的构建上下文（build context）。

如果树中没有与该全局键匹配的 widget，则当前上下文为 null。

### currentWidget

```dart
Widget? get currentWidget
```

树中当前拥有此全局键的 widget。

如果树中没有与该全局键匹配的 widget，则当前 widget 为 null。

### currentState

```dart
T? get currentState
```

树中当前拥有此全局键的 widget 所对应的 [State](https://www.yuque.com/thyname/flutter.widgets/state)。

在以下情况下当前 state 为 null：(1) 树中没有与该全局键匹配的 widget，(2) 该 widget 不是 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget)，或其关联的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象不是 `T` 的子类型。

# LabeledGlobalKey

```dart
class LabeledGlobalKey<T extends State<StatefulWidget>> extends GlobalKey<T> {}
```

带有调试标签的全局键。

调试标签有助于文档说明和调试。该标签不影响键的标识。

### LabeledGlobalKey()

```dart
LabeledGlobalKey(String? _debugLabel)
```

创建一个带有调试标签的全局键。

该标签不影响键的标识。

### toString()

```dart
String toString()
```

# GlobalObjectKey

```dart
class GlobalObjectKey<T extends State<StatefulWidget>> extends GlobalKey<T> {}
```

一个通过其值所使用的对象获取自身标识的全局键。

用于将某个 widget 的标识与用来生成该 widget 的对象的标识绑定在一起。

针对同一对象创建的任何 [GlobalObjectKey](https://www.yuque.com/thyname/flutter.widgets/globalobjectkey) 都会相互匹配。

如果该对象不是私有的，那么可能会发生冲突：树的不同部分中相互独立的 widget 会将同一个对象复用为其 [GlobalObjectKey](https://www.yuque.com/thyname/flutter.widgets/globalobjectkey) 的值，从而导致全局键冲突。为避免此问题，可创建一个私有的 [GlobalObjectKey](https://www.yuque.com/thyname/flutter.widgets/globalobjectkey) 子类，如下所示：

```dart
class _MyKey extends GlobalObjectKey {
  const _MyKey(super.value);
}
```

由于该键的 [runtimeType] 是其标识的一部分，即便值相同，这样做也可以防止与其他 [GlobalObjectKey](https://www.yuque.com/thyname/flutter.widgets/globalobjectkey) 发生冲突。

### GlobalObjectKey()

```dart
GlobalObjectKey(Object value)
```

创建一个全局键，该键在其 [operator==] 中对 [value] 使用 [identical](https://www.yuque.com/thyname/dart.core/identical) 进行比较。

### value

```dart
Object value
```

该键的 [operator==] 所使用的对象标识。

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# Widget

```dart
abstract class Widget extends DiagnosticableTree {}
```

描述一个 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 的配置。

Widget 是 Flutter 框架中的核心类层次结构。widget 是对用户界面某一部分的不可变描述。widget 可以被"膨胀"（inflate）为 element，由 element 来管理底层的渲染树。

widget 本身没有可变状态（其所有字段都必须是 final 的）。如果希望将可变状态与某个 widget 相关联，请考虑使用 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget)，它会在被膨胀时（通过 [StatefulWidget.createState]）创建一个 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象并纳入树中。

一个给定的 widget 可以在树中被包含零次或多次。特别地，一个给定的 widget 可以在树中被放置多次。widget 每次被放置到树中时都会被膨胀为一个 [Element](https://www.yuque.com/thyname/flutter.widgets/element)，这意味着一个被多次纳入树中的 widget 也会被多次膨胀。

[key] 属性控制一个 widget 在树中替换另一个 widget 的方式。如果两个 widget 的 [runtimeType] 和 [key] 属性分别满足 [operator==]，那么新 widget 会通过更新底层 element 来替换旧 widget（即调用 [Element.update] 并传入新 widget）。否则，旧的 element 会从树中移除，新 widget 会被膨胀为一个 element，并插入到树中。

另请参阅：

- [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 和 [State](https://www.yuque.com/thyname/flutter.widgets/state)，用于在其生命周期内可以多次以不同方式构建的 widget。
- [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)，用于引入可被子孙组件读取的环境状态的 widget。
- [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget)，用于在给定特定配置和环境状态时始终以相同方式构建的 widget。

### Widget()

```dart
Widget({Key? key})
```

为子类初始化 [key]。

### key

```dart
Key? key
```

控制一个 widget 在树中替换另一个 widget 的方式。

如果两个 widget 的 [runtimeType] 和 [key] 属性分别满足 [operator==]，那么新 widget 会通过更新底层 element 来替换旧 widget（即调用 [Element.update] 并传入新 widget）。否则，旧的 element 会从树中移除，新 widget 会被膨胀为一个 element，并插入到树中。

此外，将 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 用作 widget 的 [key]，可以使该 element 在树中四处移动（改变父节点）而不丢失状态。当发现一个新 widget（其键和类型与树中同一位置的先前 widget 不匹配），但在上一帧中树的其他位置存在一个具有相同全局键的 widget 时，该 widget 的 element 会被移动到新位置。

通常，作为另一个 widget 唯一子节点的 widget 不需要显式的键。

另请参阅：

- [Key](https://www.yuque.com/thyname/flutter.foundation/key) 和 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 处的讨论。

### createElement()

```dart
Element createElement()
```

将此配置膨胀为一个具体的实例。

一个给定的 widget 可以在树中被包含零次或多次。特别地，一个给定的 widget 可以在树中被放置多次。widget 每次被放置到树中时都会被膨胀为一个 [Element](https://www.yuque.com/thyname/flutter.widgets/element)，这意味着一个被多次纳入树中的 widget 也会被多次膨胀。

### toStringShort()

```dart
String toStringShort()
```

此 widget 的简短文本描述。

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### canUpdate()

```dart
bool canUpdate(Widget oldWidget, Widget newWidget)
```

`newWidget` 是否可用于更新当前以 `oldWidget` 作为配置的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。

当且仅当两个 widget 的 [runtimeType] 和 [key] 属性满足 [operator==] 时，以某个 widget 作为配置的 element 才可以更新为以另一个 widget 作为配置。

如果这些 widget 没有键（即键为 null），那么只要类型相同即视为匹配，即使它们的子节点完全不同。

# StatelessWidget

```dart
abstract class StatelessWidget extends Widget {}
```

不需要可变状态的 widget。

无状态 widget（stateless widget）通过构建一组其他 widget 来更具体地描述用户界面的一部分。这个构建过程会递归进行，直到用户界面的描述完全具体化（例如，完全由描述具体 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 组成）。

{@youtube 560 315 https://www.youtube.com/watch?v=wE7khGHVkYY}

当你所描述的界面部分不依赖于除该对象自身的配置信息以及该 widget 被膨胀时所处的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 之外的任何内容时，无状态 widget 会非常有用。对于可以动态变化的组合，例如由于具有内部时钟驱动的状态，或依赖某些系统状态而变化的情形，请考虑使用 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget)。

## 性能考量

无状态 widget 的 [build] 方法通常只在三种情况下被调用：widget 首次插入树中时、widget 的父节点更改其配置时（参见 [Element.rebuild]），以及它所依赖的 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 发生变化时。

如果某个 widget 的父节点会频繁更改该 widget 的配置，或者该 widget 依赖的继承 widget 频繁变化，那么优化 [build] 方法的性能以保持流畅的渲染表现就非常重要。

以下是几种可用于最小化重建无状态 widget 带来的影响的技巧：

- 尽量减少 build 方法及其创建的任何 widget 所间接创建的节点数量。例如，与其用一堆精心排列的 [Row](https://www.yuque.com/thyname/flutter.widgets/row)、[Column](https://www.yuque.com/thyname/flutter.widgets/column)、[Padding](https://www.yuque.com/thyname/flutter.widgets/padding) 和 [SizedBox](https://www.yuque.com/thyname/flutter.widgets/sizedbox) 以某种巧妙的方式来定位单个子节点，不如考虑直接使用 [Align](https://www.yuque.com/thyname/flutter.widgets/align) 或 [CustomSingleChildLayout](https://www.yuque.com/thyname/flutter.widgets/customsinglechildlayout)。与其用多层 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 及其 [Decoration](https://www.yuque.com/thyname/flutter.painting/decoration) 来绘制恰到好处的图形效果，不如考虑使用单个 [CustomPaint](https://www.yuque.com/thyname/flutter.widgets/custompaint) widget。

- 尽可能使用 `const` widget，并为 widget 提供 `const` 构造函数，以便该 widget 的使用者也能这样做。

- 考虑将无状态 widget 重构为有状态 widget，以便可以使用 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 中描述的一些技巧，例如缓存子树的公共部分，以及在改变树结构时使用 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey)。

- 如果该 widget 由于使用了 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 而可能被频繁重建，请考虑将该无状态 widget 重构为多个 widget，把会发生变化的部分推向树的叶子节点。例如，与其构建一棵包含四个 widget 的树、并让最内层的 widget 依赖于 [Theme](https://www.yuque.com/thyname/flutter.material/theme)，不如考虑将 build 函数中构建最内层 widget 的那部分提取为它自己的 widget，这样当主题变化时只需要重建最内层的 widget。 {@template flutter.flutter.widgets.framework.prefer_const_over_helper}
- 在尝试创建可复用的 UI 片段时，优先使用 widget 而不是辅助方法（helper method）。例如，如果之前使用一个函数来构建 widget，那么一次 [State.setState] 调用就需要 Flutter 完全重建返回的外层 widget。而如果改用 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget)，Flutter 就能够高效地只重新渲染真正需要更新的部分。更进一步，如果所创建的 widget 是 `const` 的，Flutter 还能省去绝大部分重建工作。{@endtemplate}

这段视频进一步解释了为什么 `const` 构造函数很重要，以及为什么 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 比辅助方法更好。

{@youtube 560 315 https://www.youtube.com/watch?v=IOyq-eTRhvo}

{@tool snippet}

以下是名为 `GreenFrog` 的无状态 widget 子类的骨架。

通常情况下，widget 会有更多的构造函数参数，每个参数都对应一个 `final` 属性。

```dart
class GreenFrog extends StatelessWidget {
  const GreenFrog({ super.key });

  @override
  Widget build(BuildContext context) {
    return Container(color: const Color(0xFF2DBD3A));
  }
}
```

{@end-tool}

{@tool snippet}

下一个示例展示了更通用的 widget `Frog`，可以为其指定颜色和子节点：

```dart
class Frog extends StatelessWidget {
  const Frog({
    super.key,
    this.color = const Color(0xFF2DBD3A),
    this.child,
  });

  final Color color;
  final Widget? child;

  @override
  Widget build(BuildContext context) {
    return ColoredBox(color: color, child: child);
  }
}
```

{@end-tool}

按照惯例，widget 构造函数只使用命名参数。同样按照惯例，第一个参数是 [key]，最后一个参数是 `child`、`children` 或与之等价的参数。

另请参阅：

- [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 和 [State](https://www.yuque.com/thyname/flutter.widgets/state)，用于在其生命周期内可以多次以不同方式构建的 widget。
- [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)，用于引入可被子孙组件读取的环境状态的 widget。

### StatelessWidget()

```dart
StatelessWidget({dynamic key})
```

为子类初始化 [key]。

### createElement()

```dart
StatelessElement createElement()
```

创建一个 [StatelessElement](https://www.yuque.com/thyname/flutter.widgets/statelesselement)，以管理此 widget 在树中的位置。

子类很少需要重写此方法。

### build()

```dart
Widget build(BuildContext context)
```

描述此 widget 所表示的用户界面部分。

当此 widget 在给定的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 中被插入树中时，以及当此 widget 的依赖发生变化时（例如此 widget 所引用的某个 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 发生变化），框架会调用此方法。此方法可能在每一帧都被调用，因此除了构建 widget 之外不应有任何副作用。

框架会将此 widget 下方的子树替换为此方法返回的 widget，具体是通过更新现有子树，还是移除该子树并膨胀出一棵新的子树，取决于此方法返回的 widget 能否更新现有子树的根节点（由调用 [Widget.canUpdate] 决定）。

通常，具体实现会返回一组新创建的 widget，这些 widget 由此 widget 构造函数中的信息以及给定的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 来配置。

给定的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 包含关于此 widget 在树中被构建位置的信息。例如，该上下文提供了树中该位置的一组继承 widget。如果某个 widget 在树中被移动，或者在树中的多个位置同时被插入，那么它可能会随时间推移被赋予多个不同的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 参数进行构建。

此方法的实现必须只依赖于：

- widget 的字段，这些字段本身不得随时间变化；以及
- 通过 [BuildContext.dependOnInheritedWidgetOfExactType] 从 `context` 获取的任何环境状态。

如果一个 widget 的 [build] 方法需要依赖其他内容，请改用 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget)。

另请参阅：

- [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget)，其中包含关于性能考量的讨论。

# StatefulWidget

```dart
abstract class StatefulWidget extends Widget {}
```

具有可变状态的 widget。

状态（state）是指这样一种信息：(1) 可以在 widget 构建时被同步读取；(2) 在 widget 的生命周期内可能会发生变化。widget 的实现者有责任确保在这类状态发生变化时，使用 [State.setState] 及时通知 [State](https://www.yuque.com/thyname/flutter.widgets/state)。

有状态 widget（stateful widget）通过构建一组其他 widget 来更具体地描述用户界面的一部分。这个构建过程会递归进行，直到用户界面的描述完全具体化（例如，完全由描述具体 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 组成）。

当你所描述的界面部分可以动态变化时，例如由于具有内部时钟驱动的状态，或依赖某些系统状态而变化的情形，有状态 widget 会非常有用。对于仅依赖于该对象自身的配置信息以及该 widget 被膨胀时所处的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的组合，请考虑使用 [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget)。

{@youtube 560 315 https://www.youtube.com/watch?v=AqCMFXEmf3w}

[StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 实例本身是不可变的，它们将可变状态存储在由 [createState] 方法创建的独立 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象中，或者存储在该 [State](https://www.yuque.com/thyname/flutter.widgets/state) 所订阅的对象中，例如 [Stream](https://www.yuque.com/thyname/dart.async/stream) 或 [ChangeNotifier](https://www.yuque.com/thyname/flutter.foundation/changenotifier) 对象，对这些对象的引用则存储在 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 自身的 final 字段中。

框架每次膨胀某个 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 时都会调用 [createState]，这意味着如果同一个 widget 在树中的多个位置被插入，那么可能会有多个 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象与该同一个 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 相关联。类似地，如果某个 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 从树中移除，之后又重新插入树中，框架会再次调用 [createState] 以创建一个全新的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象，从而简化 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的生命周期。

如果创建者为其 [key] 使用了 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey)，那么当 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 从树中的一个位置移动到另一个位置时，会保留同一个 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象。由于使用 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 的 widget 在树中至多只能被使用于一个位置，因此使用 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 的 widget 至多只有一个关联的 element。当框架将带有全局键的 widget 从树中的旧位置移动到新位置时，会利用这一特性，将该 widget 对应的（唯一的）子树从旧位置嫁接（graft）到新位置（而不是在新位置重新创建该子树）。与 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 关联的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象会随子树的其余部分一起被嫁接，这意味着 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象在新位置会被复用（而不是被重新创建）。但是，为了有资格被嫁接，该 widget 必须在其从旧位置移除的同一动画帧内被插入到新位置。

## 性能考量

[StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 主要有两大类。

第一类是在 [State.initState] 中分配资源、并在 [State.dispose] 中释放这些资源，但不依赖 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)、也不调用 [State.setState] 的 widget。这类 widget 常用于应用或页面的根节点，并通过 [ChangeNotifier](https://www.yuque.com/thyname/flutter.foundation/changenotifier)、[Stream](https://www.yuque.com/thyname/dart.async/stream) 或其他此类对象与子 widget 通信。遵循这种模式的有状态 widget 相对开销较低（就 CPU 和 GPU 周期而言），因为它们只构建一次，此后就不再更新。因此，它们可以拥有相对复杂且层级较深的 build 方法。

第二类 widget 会使用 [State.setState] 或依赖 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)。这类 widget 通常会在应用的生命周期内多次重建，因此尽量减小重建此类 widget 带来的影响非常重要。（它们也可能使用 [State.initState] 或 [State.didChangeDependencies] 来分配资源，但重点在于它们会重建。）

以下是几种可用于最小化重建有状态 widget 带来的影响的技巧：

- 将状态推向叶子节点。例如，如果你的页面有一个不断跳动的时钟，与其将状态放在页面顶部、并在每次时钟跳动时重建整个页面，不如创建一个专门的时钟 widget，让它只更新自身。

- 尽量减少 build 方法及其创建的任何 widget 所间接创建的节点数量。理想情况下，一个有状态 widget 应当只创建单个 widget，且该 widget 应当是一个 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget)。（显然这并不总是可行的，但一个 widget 越接近这一理想状态，它的效率就越高。）

- 如果某个子树不会发生变化，请缓存代表该子树的 widget，并在每次可以使用时复用它。为此，可将某个 widget 赋值给一个 `final` 的状态变量，并在 build 方法中复用它。相比创建一个新的（但配置完全相同的）widget，复用一个 widget 的效率要高得多。另一种缓存策略是：将 widget 中会变化的部分提取为一个接受 child 参数的 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget)。

- 尽可能使用 `const` widget。（这等价于缓存一个 widget 并复用它。）

- 避免改变所创建子树的深度，或改变子树中 widget 的类型。例如，与其根据条件返回 child 或包裹了 [IgnorePointer](https://www.yuque.com/thyname/flutter.widgets/ignorepointer) 的 child，不如始终用 [IgnorePointer](https://www.yuque.com/thyname/flutter.widgets/ignorepointer) 包裹 child widget，并通过控制 [IgnorePointer.ignoring] 属性来实现效果。这是因为改变子树的深度需要重建、布局并绘制整个子树，而仅仅改变属性只需要对渲染树做最小程度的改动（例如对 [IgnorePointer](https://www.yuque.com/thyname/flutter.widgets/ignorepointer) 而言，根本不需要任何布局或重绘）。

- 如果出于某种原因必须改变深度，请考虑用带有 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 的 widget 包裹子树的公共部分，并在有状态 widget 的整个生命周期内保持该 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 不变。（如果没有其他方便指定键的 widget，[KeyedSubtree](https://www.yuque.com/thyname/flutter.widgets/keyedsubtree) widget 可能对此有所帮助。）

{@macro flutter.flutter.widgets.framework.prefer_const_over_helper}

这段视频进一步解释了为什么 `const` 构造函数很重要，以及为什么 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 比辅助方法更好。

{@youtube 560 315 https://www.youtube.com/watch?v=IOyq-eTRhvo}

关于重建 widget 的更多机制细节，请参见 [Element.rebuild] 处的讨论。

{@tool snippet}

以下是名为 `YellowBird` 的有状态 widget 子类的骨架。

在此示例中，[State](https://www.yuque.com/thyname/flutter.widgets/state) 没有实际的状态。状态通常表示为私有成员字段。同样，通常 widget 会有更多的构造函数参数，每个参数都对应一个 `final` 属性。

```dart
class YellowBird extends StatefulWidget {
  const YellowBird({ super.key });

  @override
  State<YellowBird> createState() => _YellowBirdState();
}

class _YellowBirdState extends State<YellowBird> {
  @override
  Widget build(BuildContext context) {
    return Container(color: const Color(0xFFFFE306));
  }
}
```

{@end-tool} {@tool snippet}

此示例展示了更通用的 widget `Bird`，可以为其指定颜色和子节点，并且它拥有一些内部状态以及一个可用于修改该状态的方法：

```dart
class Bird extends StatefulWidget {
  const Bird({
    super.key,
    this.color = const Color(0xFFFFE306),
    this.child,
  });

  final Color color;
  final Widget? child;

  @override
  State<Bird> createState() => _BirdState();
}

class _BirdState extends State<Bird> {
  double _size = 1.0;

  void grow() {
    setState(() { _size += 0.1; });
  }

  @override
  Widget build(BuildContext context) {
    return Container(
      color: widget.color,
      transform: Matrix4.diagonal3Values(_size, _size, 1.0),
      child: widget.child,
    );
  }
}
```

{@end-tool}

按照惯例，widget 构造函数只使用命名参数。同样按照惯例，第一个参数是 [key]，最后一个参数是 `child`、`children` 或与之等价的参数。

另请参阅：

- [State](https://www.yuque.com/thyname/flutter.widgets/state)，[StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 背后逻辑的载体。
- [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget)，用于在给定特定配置和环境状态时始终以相同方式构建的 widget。
- [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)，用于引入可被子孙组件读取的环境状态的 widget。

### StatefulWidget()

```dart
StatefulWidget({dynamic key})
```

为子类初始化 [key]。

### createElement()

```dart
StatefulElement createElement()
```

创建一个 [StatefulElement](https://www.yuque.com/thyname/flutter.widgets/statefulelement)，以管理此 widget 在树中的位置。

子类很少需要重写此方法。

### createState()

```dart
State createState()
```

在树中的给定位置为此 widget 创建可变状态。

子类应重写此方法，返回与其关联的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 子类的新创建实例：

```dart
@override
State<SomeWidget> createState() => _SomeWidgetState();
```

框架可能在 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 的生命周期内多次调用此方法。例如，如果该 widget 被插入树中的多个位置，框架会为每个位置创建一个单独的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象。类似地，如果该 widget 从树中移除，之后又重新插入树中，框架会再次调用 [createState] 以创建一个全新的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象，从而简化 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的生命周期。

# StateSetter

```dart
typedef StateSetter = void Function(VoidCallback fn)
```

[State.setState] 函数的签名。

# State

```dart
abstract class State<T extends StatefulWidget> with Diagnosticable {}
```

[StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 的逻辑与内部状态载体。

状态（state）是指这样一种信息：(1) 可以在 widget 构建时被同步读取；(2) 在 widget 的生命周期内可能会发生变化。widget 的实现者有责任确保在这类状态发生变化时，使用 [State.setState] 及时通知 [State](https://www.yuque.com/thyname/flutter.widgets/state)。

[State](https://www.yuque.com/thyname/flutter.widgets/state) 对象是框架在膨胀 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 以将其插入树中时，通过调用 [StatefulWidget.createState] 方法创建的。由于一个给定的 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 实例可以被多次膨胀（例如，该 widget 同时被纳入树中的多个位置），因此可能会有多个 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象与一个给定的 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 实例相关联。类似地，如果某个 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 从树中移除，之后又重新插入树中，框架会再次调用 [StatefulWidget.createState] 以创建一个全新的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象，从而简化 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的生命周期。

[State](https://www.yuque.com/thyname/flutter.widgets/state) 对象具有以下生命周期：

- 框架通过调用 [StatefulWidget.createState] 创建一个 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象。
- 新创建的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象与一个 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 相关联。这种关联是永久的：[State](https://www.yuque.com/thyname/flutter.widgets/state) 对象永远不会改变其 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)。但是，该 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 本身可以随其子树在树中移动。此时，该 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象被视为已 [mounted]（已挂载）。
- 框架调用 [initState]。[State](https://www.yuque.com/thyname/flutter.widgets/state) 的子类应重写 [initState]，以执行依赖于 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 或 widget 的一次性初始化，在调用 [initState] 方法时，二者分别以 [context] 和 [widget] 属性的形式可用。
- 框架调用 [didChangeDependencies]。[State](https://www.yuque.com/thyname/flutter.widgets/state) 的子类应重写 [didChangeDependencies]，以执行涉及 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 的初始化。如果调用了 [BuildContext.dependOnInheritedWidgetOfExactType]，那么在其后依赖的继承 widget 发生变化时，或者该 widget 在树中移动时，[didChangeDependencies] 方法会被再次调用。
- 此时，[State](https://www.yuque.com/thyname/flutter.widgets/state) 对象已完全初始化，框架可能会多次调用其 [build] 方法，以获取此子树的用户界面描述。[State](https://www.yuque.com/thyname/flutter.widgets/state) 对象可以通过调用其 [setState] 方法，自发地请求重建其子树，这表明其内部状态发生了可能影响此子树用户界面的变化。
- 在此期间，父 widget 可能会重建，并请求树中的此位置更新为显示一个具有相同 [runtimeType] 和 [Widget.key] 的新 widget。发生这种情况时，框架会将 [widget] 属性更新为指向新 widget，然后以先前的 widget 作为参数调用 [didUpdateWidget] 方法。[State](https://www.yuque.com/thyname/flutter.widgets/state) 对象应重写 [didUpdateWidget] 以响应其关联 widget 的变化（例如，启动隐式动画）。框架总是在调用 [didUpdateWidget] 之后调用 [build]，这意味着在 [didUpdateWidget] 中调用 [setState] 是多余的。（另请参见 [Element.rebuild] 处的讨论。）
- 在开发过程中，如果发生热重载（无论是从命令行 `flutter` 工具通过按下 `r` 触发，还是从 IDE 触发），都会调用 [reassemble] 方法。这提供了一个重新初始化在 [initState] 方法中准备的任何数据的机会。
- 如果包含该 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的子树从树中移除（例如，因为父节点构建了一个具有不同 [runtimeType] 或 [Widget.key] 的 widget），框架会调用 [deactivate] 方法。子类应重写此方法，以清理此对象与树中其他 element 之间的任何联系（例如，如果你向某个祖先提供了指向某个子孙 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的指针）。
- 此时，框架可能会将此子树重新插入到树的另一部分。如果发生这种情况，框架会确保调用 [build]，以便让 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象有机会适应其在树中的新位置。如果框架确实重新插入了此子树，它会在该子树从树中移除的同一动画帧结束之前完成。正因如此，[State](https://www.yuque.com/thyname/flutter.widgets/state) 对象可以将大多数资源的释放推迟到框架调用其 [dispose] 方法时再进行。
- 如果框架在当前动画帧结束之前没有重新插入此子树，框架会调用 [dispose]，这表明此 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象将永远不会再构建。子类应重写此方法，以释放此对象持有的任何资源（例如，停止任何正在进行的动画）。
- 在框架调用 [dispose] 之后，该 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象被视为已卸载（unmounted），且 [mounted] 属性为 false。此时调用 [setState] 是错误的。生命周期的这一阶段是终结性的：无法重新挂载一个已经被释放（disposed）的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象。

另请参阅：

- [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget)，[State](https://www.yuque.com/thyname/flutter.widgets/state) 当前配置的载体，其文档中包含 [State](https://www.yuque.com/thyname/flutter.widgets/state) 的示例代码。
- [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget)，用于在给定特定配置和环境状态时始终以相同方式构建的 widget。
- [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)，用于引入可被子孙组件读取的环境状态的 widget。
- [Widget](https://www.yuque.com/thyname/flutter.widgets/widget)，widget 概览。

### widget

```dart
T get widget
```

当前配置。

[State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的配置就是与之对应的 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 实例。此属性由框架在调用 [initState] 之前初始化。如果父节点将树中的此位置更新为一个与当前配置具有相同 [runtimeType] 和 [Widget.key] 的新 widget，框架会将此属性更新为指向该新 widget，然后调用 [didUpdateWidget]，并以旧配置作为参数传入。

### context

```dart
BuildContext get context
```

此 widget 构建所在的树中位置。

框架会在使用 [StatefulWidget.createState] 创建 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象之后、调用 [initState] 之前，将 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象与一个 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 相关联。这种关联是永久的：[State](https://www.yuque.com/thyname/flutter.widgets/state) 对象永远不会改变其 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)。但是，该 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 本身可以在树中移动。

在调用 [dispose] 之后，框架会切断 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象与该 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 之间的联系。

### mounted

```dart
bool get mounted
```

此 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象当前是否位于树中。

在创建一个 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象、并在调用 [initState] 之前，框架会通过将该 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象与一个 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 相关联来"挂载"它。该 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象会一直保持挂载状态，直到框架调用 [dispose]，此后框架将永远不会再要求该 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象执行 [build]。

在 [mounted] 为 true 之前调用 [setState] 是错误的。

### initState()

```dart
void initState()
```

当此对象被插入树中时调用。

框架会为它所创建的每一个 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象恰好调用一次此方法。

重写此方法以执行依赖于该对象在树中插入位置（即 [context]）或用于配置该对象的 widget（即 [widget]）的初始化。

{@template flutter.widgets.State.initState} 如果某个 [State](https://www.yuque.com/thyname/flutter.widgets/state) 的 [build] 方法依赖于一个自身可以改变状态的对象，例如 [ChangeNotifier](https://www.yuque.com/thyname/flutter.foundation/changenotifier) 或 [Stream](https://www.yuque.com/thyname/dart.async/stream)，或者其他可以订阅以接收通知的对象，那么务必在 [initState]、[didUpdateWidget] 和 [dispose] 中正确地进行订阅与取消订阅：

- 在 [initState] 中，订阅该对象。
- 在 [didUpdateWidget] 中，如果更新后的 widget 配置需要替换该对象，则取消订阅旧对象并订阅新对象。
- 在 [dispose] 中，取消订阅该对象。

{@endtemplate}

不应在此方法中使用 [BuildContext.dependOnInheritedWidgetOfExactType]。不过，[didChangeDependencies] 会紧接在此方法之后被调用，[BuildContext.dependOnInheritedWidgetOfExactType] 可以在那里使用。

此方法的实现应以调用父类方法开始，如 `super.initState()`。

### didUpdateWidget()

```dart
void didUpdateWidget(T oldWidget)
```

每当 widget 配置发生变化时调用。

如果父 widget 重建，并请求树中的此位置更新为显示一个具有相同 [runtimeType] 和 [Widget.key] 的新 widget，框架会将此 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的 [widget] 属性更新为指向新 widget，然后以先前的 widget 作为参数调用此方法。

重写此方法以响应 [widget] 的变化（例如，启动隐式动画）。

框架总是在调用 [didUpdateWidget] 之后调用 [build]，这意味着在 [didUpdateWidget] 中调用 [setState] 是多余的。

{@macro flutter.widgets.State.initState}

此方法的实现应以调用父类方法开始，如 `super.didUpdateWidget(oldWidget)`。

_关于此方法何时被调用的更多信息，请参见 [Element.rebuild] 处的讨论。_

### reassemble()

```dart
void reassemble()
```

{@macro flutter.widgets.Element.reassemble}

除了此方法会被调用之外，还可以保证在触发 reassemble 时会调用 [build] 方法。因此大多数 widget 不需要在 [reassemble] 方法中做任何事情。

另请参阅：

- [Element.reassemble]
- [BindingBase.reassembleApplication]
- [Image](https://www.yuque.com/thyname/dart.ui/image)，它利用此方法来重新加载图片。

### setState()

```dart
void setState(VoidCallback fn)
```

通知框架此对象的内部状态已发生变化。

每当更改某个 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的内部状态时，都应在传递给 [setState] 的函数中进行更改：

```dart
setState(() { _myState = newValue; });
```

所提供的回调会被立即同步调用。它不能返回一个 future（该回调不能是 `async` 的），因为那样一来状态实际何时被设置就会变得不明确。

调用 [setState] 会通知框架此对象的内部状态已发生变化，且这一变化可能会影响此子树的用户界面，从而促使框架为此 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象安排一次 [build]。

如果直接更改状态而不调用 [setState]，框架可能不会安排一次 [build]，此子树的用户界面也可能不会更新以反映新的状态。

通常建议 [setState] 方法只用于包裹对状态的实际更改，而不包裹与该更改相关的任何计算。例如，下面的例子中，[build] 函数所使用的一个值被递增，然后该更改被写入磁盘，但只有递增操作被包裹在 [setState] 中：

```dart
Future<void> _incrementCounter() async {
  setState(() {
    _counter++;
  });
  Directory directory = await getApplicationDocumentsDirectory(); // 来自 path_provider 包
  final String dirName = directory.path;
  await File('$dirName/counter.txt').writeAsString('$_counter');
}
```

有时，发生变化的状态位于某个不属于 widget [State](https://www.yuque.com/thyname/flutter.widgets/state) 所拥有的其他对象中，但 widget 仍然需要更新以响应这个新状态。这在使用 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable)（例如 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)）时尤为常见。

在这种情况下，最好在传递给 [setState] 的回调中留下注释，说明发生了什么状态变化：

```dart
void _update() {
  setState(() { /* 动画发生了变化。 */ });
}
//...
animation.addListener(_update);
```

在框架调用 [dispose] 之后调用此方法是错误的。可以通过检查 [mounted] 属性是否为 true 来判断调用此方法是否合法。不过，更好的做法是取消可能触发 [setState] 的那项工作，而不是仅仅在调用 [setState] 之前检查 [mounted]，否则会白白浪费 CPU 周期。

## 设计讨论

此 API 的最初版本是一个名为 `markNeedsBuild` 的方法，以与 [RenderObject.markNeedsLayout]、[RenderObject.markNeedsPaint] 等方法保持一致。

然而，对 Flutter 框架的早期用户测试表明，人们调用 `markNeedsBuild()` 的频率会远超实际需要。实际上，人们把它当作一种"护身符"来使用：任何时候只要不确定是否需要调用它，就会调用它，以防万一。

自然地，这导致了应用程序中的性能问题。

当该 API 被改为接受一个回调之后，这种做法大大减少了。一种猜测是，促使开发者在回调中实际更新其状态，使开发者更加谨慎地思考究竟哪些内容正在被更新，从而提升了他们对何时应当调用该方法的理解。

实际上，[setState] 方法的实现非常简单：它同步调用所提供的回调，然后调用 [Element.markNeedsBuild]。

## 性能考量

调用此函数的*直接*开销很小，而且由于预计每帧最多调用一次，这点开销基本可以忽略不计。尽管如此，最好还是避免冗余地调用此函数（例如在紧密循环中调用），因为它确实涉及创建一个闭包并调用它。此方法是幂等的，每个 [State](https://www.yuque.com/thyname/flutter.widgets/state) 每帧调用多次并不会带来任何好处。

然而，触发此函数所带来的*间接*开销很高：它会导致该 widget 重建，可能触发以该 widget 为根的整个子树的重建，并进一步触发对应 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 子树的重新布局和重绘。

因此，只有当检测到的状态变化会导致 [build] 方法的结果发生有意义的变化时，才应调用此方法。

另请参阅：

- [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget)，其 API 文档中有一节讨论了与此相关的性能考量。

### deactivate()

```dart
void deactivate()
```

当此对象从树中移除时调用。

每当框架从树中移除此 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象时，都会调用此方法。在某些情况下，框架会将该 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象重新插入到树的另一部分（例如，如果包含此 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的子树因使用了 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 而从树中的一个位置嫁接到另一个位置）。如果发生这种情况，框架会调用 [activate]，让该 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象有机会重新获取其在 [deactivate] 中释放的任何资源。随后框架还会调用 [build]，让该 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象有机会适应其在树中的新位置。如果框架确实重新插入了此子树，它会在该子树从树中移除的同一动画帧结束之前完成。正因如此，[State](https://www.yuque.com/thyname/flutter.widgets/state) 对象可以将大多数资源的释放推迟到框架调用其 [dispose] 方法时再进行。

子类应重写此方法，以清理此对象与树中其他 element 之间的任何联系（例如，如果你向某个祖先提供了指向某个子孙 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的指针）。

此方法的实现应以调用父类方法结束，如 `super.deactivate()`。

另请参阅：

- [dispose]，如果该 widget 被永久从树中移除，会在 [deactivate] 之后调用。

### activate()

```dart
void activate()
```

当此对象在通过 [deactivate] 被移除后又重新插入树中时调用。

在大多数情况下，一个 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象被停用（deactivate）之后，*不会*被重新插入树中，其 [dispose] 方法将被调用，以表明它已经可以被垃圾回收了。

但在某些情况下，一个 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象被停用之后，框架会将它重新插入到树的另一部分（例如，如果包含此 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的子树因使用了 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 而从树中的一个位置嫁接到另一个位置）。如果发生这种情况，框架会调用 [activate]，让该 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象有机会重新获取其在 [deactivate] 中释放的任何资源。随后框架还会调用 [build]，让该对象有机会适应其在树中的新位置。如果框架确实重新插入了此子树，它会在该子树从树中移除的同一动画帧结束之前完成。正因如此，[State](https://www.yuque.com/thyname/flutter.widgets/state) 对象可以将大多数资源的释放推迟到框架调用其 [dispose] 方法时再进行。

框架在 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象首次被插入树中时不会调用此方法。在这种情况下，框架调用的是 [initState]。

此方法的实现应以调用父类方法开始，如 `super.activate()`。

另请参阅：

- [Element.activate]，当某个 element 从"未激活（inactive）"状态转换为"激活（active）"状态时对应的方法。

### dispose()

```dart
void dispose()
```

当此对象被永久从树中移除时调用。

框架会在此 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象将永远不再构建时调用此方法。在框架调用 [dispose] 之后，该 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象被视为已卸载，且 [mounted] 属性为 false。此时调用 [setState] 是错误的。生命周期的这一阶段是终结性的：无法重新挂载一个已经被释放的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象。

子类应重写此方法，以释放此对象持有的任何资源（例如，停止任何正在进行的动画）。

{@macro flutter.widgets.State.initState}

此方法的实现应以调用父类方法结束，如 `super.dispose()`。

## 注意事项

此方法在开发者可能预期的某些时机*并不会*被调用，例如应用关闭或通过平台原生方法被终止时。

### 应用关闭

无法预测应用关闭何时会发生。例如，用户的电池可能会起火，用户可能会把设备掉进泳池，或者操作系统可能会由于内存压力而单方面终止应用进程。

应用程序有责任确保即使在遭遇快速的、计划外的终止时，也能保持良好的行为。

要人为地使整个 widget 树被释放，可以考虑使用诸如 [SizedBox.shrink] 之类的 widget 调用 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp)。

要监听平台关闭消息（以及其他生命周期变化），可以考虑使用 [AppLifecycleListener](https://www.yuque.com/thyname/flutter.widgets/applifecyclelistener) API。

{@macro flutter.widgets.runApp.dismissal}

有关如何更积极地释放资源的建议，请参见用于引导应用启动的方法（例如 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 或 [runWidget](https://www.yuque.com/thyname/flutter.widgets/runwidget)）。

另请参阅：

- [deactivate]，在 [dispose] 之前调用。

### build()

```dart
Widget build(BuildContext context)
```

描述此 widget 所表示的用户界面部分。

框架会在多种不同情况下调用此方法。例如：

- 在调用 [initState] 之后。
- 在调用 [didUpdateWidget] 之后。
- 在收到对 [setState] 的调用之后。
- 在此 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的某个依赖发生变化之后（例如，先前 [build] 所引用的某个 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 发生了变化）。
- 在调用 [deactivate]、然后又将该 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象重新插入树中的另一位置之后。

此方法可能在每一帧都被调用，因此除了构建 widget 之外不应有任何副作用。

框架会将此 widget 下方的子树替换为此方法返回的 widget，具体是通过更新现有子树，还是移除该子树并膨胀出一棵新的子树，取决于此方法返回的 widget 能否更新现有子树的根节点（由调用 [Widget.canUpdate] 决定）。

通常，具体实现会返回一组新创建的 widget，这些 widget 由此 widget 构造函数中的信息、给定的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)，以及此 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的内部状态来配置。

给定的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 包含关于此 widget 在树中被构建位置的信息。例如，该上下文提供了树中该位置的一组继承 widget。此 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 参数始终与此 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的 [context] 属性相同，并且在该对象的整个生命周期内保持不变。之所以在此处冗余地提供 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 参数，是为了使此方法的签名与 [WidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/widgetbuilder) 保持一致。

## 设计讨论

### 为什么 [build] 方法在 [State](https://www.yuque.com/thyname/flutter.widgets/state) 上，而不是 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 上？

将 `Widget build(BuildContext context)` 方法放在 [State](https://www.yuque.com/thyname/flutter.widgets/state) 上，而不是在 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 上放置 `Widget build(BuildContext context, State state)` 方法，可以在子类化 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 时给开发者带来更大的灵活性。

例如，[AnimatedWidget](https://www.yuque.com/thyname/flutter.widgets/animatedwidget) 是 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 的一个子类，它为其子类引入了一个抽象的 `Widget build(BuildContext context)` 方法。如果 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 本身已经有一个接受 [State](https://www.yuque.com/thyname/flutter.widgets/state) 参数的 [build] 方法，那么 [AnimatedWidget](https://www.yuque.com/thyname/flutter.widgets/animatedwidget) 就将被迫把其 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象暴露给子类，即使其 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象是 [AnimatedWidget](https://www.yuque.com/thyname/flutter.widgets/animatedwidget) 的内部实现细节。

从概念上讲，[StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget) 本身也可以以类似的方式实现为 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 的子类。如果 [build] 方法位于 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 而非 [State](https://www.yuque.com/thyname/flutter.widgets/state) 上，那么这种做法就不再可行了。

将 [build] 函数放在 [State](https://www.yuque.com/thyname/flutter.widgets/state) 而非 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 上，还有助于避免一类与闭包隐式捕获 `this` 相关的 bug。如果在 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 的 build 函数中定义一个闭包，该闭包会隐式捕获 `this`，也就是当前的 widget 实例，并且该实例的（不可变）字段会处于该闭包的作用域内：

```dart
// （这不是有效的 Flutter 代码）
class MyButton extends StatefulWidgetX {
  MyButton({super.key, required this.color});

  final Color color;

  @override
  Widget build(BuildContext context, State state) {
    return SpecialWidget(
      handler: () { print('color: $color'); },
    );
  }
}
```

举例来说，假设父节点以蓝色的 `color` 构建 `MyButton`，那么打印函数中的 `$color` 会如预期般引用蓝色。现在，假设父节点以绿色重建 `MyButton`。第一次构建时创建的闭包仍然隐式引用最初的 widget，`$color` 仍然打印蓝色，即使该 widget 已经更新为绿色；如果该闭包的生命周期超出了其 widget，它就会打印过时的信息。

相比之下，如果 [build] 函数位于 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象上，那么在 [build] 期间创建的闭包会隐式捕获 [State](https://www.yuque.com/thyname/flutter.widgets/state) 实例，而不是 widget 实例：

```dart
class MyButton extends StatefulWidget {
  const MyButton({super.key, this.color = Colors.teal});

  final Color color;
  // ...
}

class MyButtonState extends State<MyButton> {
  // ...
  @override
  Widget build(BuildContext context) {
    return SpecialWidget(
      handler: () { print('color: ${widget.color}'); },
    );
  }
}
```

现在，当父节点以绿色重建 `MyButton` 时，第一次构建时创建的闭包仍然引用 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象（该对象在多次重建之间被保留），但框架已经将该 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的 [widget] 属性更新为指向新的 `MyButton` 实例，因此 `${widget.color}` 会如预期般打印绿色。

另请参阅：

- [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget)，其中包含关于性能考量的讨论。

### didChangeDependencies()

```dart
void didChangeDependencies()
```

当此 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的某个依赖发生变化时调用。

例如，如果先前对 [build] 的调用引用了某个之后发生变化的 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)，框架就会调用此方法，以就此变化通知该对象。

此方法也会在 [initState] 之后立即被调用。在此方法中调用 [BuildContext.dependOnInheritedWidgetOfExactType] 是安全的。

子类很少重写此方法，因为框架总是会在依赖发生变化后调用 [build]。一些子类之所以重写此方法，是因为它们需要在依赖发生变化时执行一些开销较大的操作（例如网络请求），而这类操作如果每次构建都执行则代价过高。

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ProxyWidget

```dart
abstract class ProxyWidget extends Widget {}
```

拥有一个提供给它的子 widget，而不是自行构建新 widget 的 widget。

可作为其他 widget 的基类使用，例如 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 和 [ParentDataWidget](https://www.yuque.com/thyname/flutter.widgets/parentdatawidget)。

另请参阅：

- [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)，用于引入可被子孙组件读取的环境状态的 widget。
- [ParentDataWidget](https://www.yuque.com/thyname/flutter.widgets/parentdatawidget)，用于填充其子节点 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的 [RenderObject.parentData] 槽位，以配置父 widget 布局的 widget。
- [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 和 [State](https://www.yuque.com/thyname/flutter.widgets/state)，用于在其生命周期内可以多次以不同方式构建的 widget。
- [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget)，用于在给定特定配置和环境状态时始终以相同方式构建的 widget。
- [Widget](https://www.yuque.com/thyname/flutter.widgets/widget)，widget 概览。

### ProxyWidget()

```dart
ProxyWidget({dynamic key, required Widget child})
```

创建一个恰好拥有一个子 widget 的 widget。

### child

```dart
Widget child
```

树中位于此 widget 下方的 widget。

{@template flutter.widgets.ProxyWidget.child} 此 widget 只能拥有一个子节点。要布局多个子节点，可让此 widget 的子节点是诸如 [Row](https://www.yuque.com/thyname/flutter.widgets/row)、[Column](https://www.yuque.com/thyname/flutter.widgets/column) 或 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 之类拥有 `children` 属性的 widget，然后将各个子节点提供给该 widget。{@endtemplate}

# ParentDataWidget

```dart
abstract class ParentDataWidget<T extends ParentData> extends ProxyWidget {}
```

用于将 [ParentData](https://www.yuque.com/thyname/flutter.rendering/parentdata) 信息挂载到 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 子节点上的 widget 的基类。

可用于为拥有多个子节点的 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 提供逐子节点的配置。例如，[Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 使用 [Positioned](https://www.yuque.com/thyname/flutter.widgets/positioned) 这一父数据 widget 来定位每个子节点。

[ParentDataWidget](https://www.yuque.com/thyname/flutter.widgets/parentdatawidget) 专用于特定类型的 [ParentData](https://www.yuque.com/thyname/flutter.rendering/parentdata)。该类即为类型参数 `T`，即 [ParentData](https://www.yuque.com/thyname/flutter.rendering/parentdata) 的类型参数。

{@tool snippet}

此示例展示了如何构建一个 [ParentDataWidget](https://www.yuque.com/thyname/flutter.widgets/parentdatawidget)，通过为每个子节点指定一个 [Size](https://www.yuque.com/thyname/dart.ui/size) 来配置 `FrogJar` widget 的子节点。

```dart
class FrogSize extends ParentDataWidget<FrogJarParentData> {
  const FrogSize({
    super.key,
    required this.size,
    required super.child,
  });

  final Size size;

  @override
  void applyParentData(RenderObject renderObject) {
    final FrogJarParentData parentData = renderObject.parentData! as FrogJarParentData;
    if (parentData.size != size) {
      parentData.size = size;
      final RenderFrogJar targetParent = renderObject.parent! as RenderFrogJar;
      targetParent.markNeedsLayout();
    }
  }

  @override
  Type get debugTypicalAncestorWidgetClass => FrogJar;
}
```

{@end-tool}

另请参阅：

- [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)，布局算法的父类。
- [RenderObject.parentData]，此类所配置的槽位。
- [ParentData](https://www.yuque.com/thyname/flutter.rendering/parentdata)，将被放置在 [RenderObject.parentData] 槽位中的数据的父类。[ParentDataWidget](https://www.yuque.com/thyname/flutter.widgets/parentdatawidget) 的类型参数 `T` 就是一个 [ParentData](https://www.yuque.com/thyname/flutter.rendering/parentdata)。
- [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget)，包装 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的 widget 所属的类。
- [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 和 [State](https://www.yuque.com/thyname/flutter.widgets/state)，用于在其生命周期内可以多次以不同方式构建的 widget。

### ParentDataWidget()

```dart
ParentDataWidget({dynamic key, required Widget child})
```

抽象的 const 构造函数。此构造函数使子类能够提供 const 构造函数，以便可以在 const 表达式中使用它们。

### createElement()

```dart
ParentDataElement<T> createElement()
```

### debugIsValidRenderObject()

```dart
bool debugIsValidRenderObject(RenderObject renderObject)
```

检查此 widget 是否可以将其父数据应用到提供的 `renderObject` 上。

提供的 `renderObject` 的 [RenderObject.parentData] 通常由 [debugTypicalAncestorWidgetClass] 所返回类型的祖先 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 设置。

此方法会在以相同的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 调用 [applyParentData] 之前被调用。

### debugTypicalAncestorWidgetClass

```dart
Type get debugTypicalAncestorWidgetClass
```

描述通常用于设置 [applyParentData] 将要写入的 [ParentData](https://www.yuque.com/thyname/flutter.rendering/parentdata) 的 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget)。

这只用于错误信息中，通过 [debugTypicalAncestorWidgetDescription] 告知用户通常包裹此 [ParentDataWidget](https://www.yuque.com/thyname/flutter.widgets/parentdatawidget) 的 widget 是什么。

## 实现方式

所返回的 Type 应描述 `RenderObjectWidget` 的某个子类。如果支持多种 Type，请使用 [debugTypicalAncestorWidgetDescription]，它通常会插入此值，但也可以被重写以描述多种 Type。

```dart
  @override
  Type get debugTypicalAncestorWidgetClass => FrogJar;
```

如果"典型"父节点是泛型的（`Foo<T>`），可以考虑指定一个典型的类型参数（例如，如果 `int` 是该类型通常被特化的方式，则指定 `Foo<int>`），或者指定其上界（例如 `Foo<Object?>`）。

### debugTypicalAncestorWidgetDescription

```dart
String get debugTypicalAncestorWidgetDescription
```

描述通常用于设置 [applyParentData] 将要写入的 [ParentData](https://www.yuque.com/thyname/flutter.rendering/parentdata) 的 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget)。

这只用于错误信息中，告知用户通常包裹此 [ParentDataWidget](https://www.yuque.com/thyname/flutter.widgets/parentdatawidget) 的 widget 是什么。

默认以字符串形式返回 [debugTypicalAncestorWidgetClass]。可以重写此方法以描述多种有效的父节点 Type。

### applyParentData()

```dart
void applyParentData(RenderObject renderObject)
```

将此 widget 中的数据写入给定渲染对象的父数据中。

每当框架检测到与 [child] 相关联的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的 [RenderObject.parentData] 已过时时，就会调用此函数。例如，如果该渲染对象最近被插入渲染树中，该渲染对象的父数据可能与此 widget 中的数据不匹配。

子类应重写此函数，将其字段中的数据复制到给定渲染对象的 [RenderObject.parentData] 字段中。可以保证该渲染对象的父节点是由类型为 `T` 的 widget 创建的，这通常意味着此函数可以假定该渲染对象的父数据对象继承自某个特定的类。

如果此函数修改的数据会改变父节点的布局或绘制，那么此函数有责任在父节点上调用 [RenderObject.markNeedsLayout] 或 [RenderObject.markNeedsPaint]（视情况而定）。

### debugCanApplyOutOfTurn()

```dart
bool debugCanApplyOutOfTurn()
```

对于此 widget，是否允许使用 [ParentDataElement.applyWidgetOutOfTurn] 方法。

只有当此 widget 所代表的 [ParentData](https://www.yuque.com/thyname/flutter.rendering/parentdata) 配置不会对布局或绘制阶段产生影响时，才应返回 true。

另请参阅：

- [ParentDataElement.applyWidgetOutOfTurn]，在调试模式下会验证这一点。

# InheritedWidget

```dart
abstract class InheritedWidget extends ProxyWidget {}
```

用于高效地向树的下方传播信息的 widget 的基类。

{@youtube 560 315 https://www.youtube.com/watch?v=og-vJqLzg2c}

要从某个构建上下文获取最近的某种类型的继承 widget 实例，请使用 [BuildContext.dependOnInheritedWidgetOfExactType]。

以这种方式被引用的继承 widget，当其自身状态发生变化时，会导致使用方重建。

{@youtube 560 315 https://www.youtube.com/watch?v=Zbm3hjPjQMk}

{@tool snippet}

以下是名为 `FrogColor` 的继承 widget 的骨架：

```dart
class FrogColor extends InheritedWidget {
  const FrogColor({
    super.key,
    required this.color,
    required super.child,
  });

  final Color color;

  static FrogColor? maybeOf(BuildContext context) {
    return context.dependOnInheritedWidgetOfExactType<FrogColor>();
  }

  static FrogColor of(BuildContext context) {
    final FrogColor? result = maybeOf(context);
    assert(result != null, 'No FrogColor found in context');
    return result!;
  }

  @override
  bool updateShouldNotify(FrogColor oldWidget) => color != oldWidget.color;
}
```

{@end-tool}

## 实现 `of` 和 `maybeOf` 方法

按照惯例，会在 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 上提供两个静态方法 `of` 和 `maybeOf`，它们调用 [BuildContext.dependOnInheritedWidgetOfExactType]。这使得该类可以在作用域内不存在相应 widget 时定义自己的回退逻辑。

`of` 方法通常返回一个不可为空的实例，并在找不到该 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 时触发断言；而 `maybeOf` 方法返回一个可为空的实例，如果找不到该 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 则返回 null。`of` 方法通常是通过在内部调用 `maybeOf` 来实现的。

有时，`of` 和 `maybeOf` 方法返回的是某些数据，而不是继承 widget 本身；例如在此例中，它本可以返回一个 [Color](https://www.yuque.com/thyname/dart.ui/color)，而不是 `FrogColor` widget。

有时，继承 widget 是另一个类的实现细节，因此是私有的。在这种情况下，`of` 和 `maybeOf` 方法通常改为在公共类上实现。例如，[Theme](https://www.yuque.com/thyname/flutter.material/theme) 被实现为一个 [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget)，它构建了一个私有的继承 widget；[Theme.of] 使用 [BuildContext.dependOnInheritedWidgetOfExactType] 查找该私有继承 widget，然后返回其中的 [ThemeData](https://www.yuque.com/thyname/flutter.material/themedata)。

## 调用 `of` 或 `maybeOf` 方法

在使用 `of` 或 `maybeOf` 方法时，`context` 必须是该 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 的子孙，即它必须在树中位于该 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)"下方"。

{@tool snippet}

在此示例中，所使用的 `context` 来自 [Builder](https://www.yuque.com/thyname/flutter.widgets/builder)，它是 `FrogColor` widget 的子节点，因此这样可以正常工作。

```dart
// 接续前面的示例……
class MyPage extends StatelessWidget {
  const MyPage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: FrogColor(
        color: Colors.green,
        child: Builder(
          builder: (BuildContext innerContext) {
            return Text(
              'Hello Frog',
              style: TextStyle(color: FrogColor.of(innerContext).color),
            );
          },
        ),
      ),
    );
  }
}
```

{@end-tool}

{@tool snippet}

在此示例中，所使用的 `context` 来自 `MyOtherPage` widget，它是 `FrogColor` widget 的父节点，因此这样无法正常工作，在调用 `FrogColor.of` 时会触发断言。

```dart
// 接续前面的示例……

class MyOtherPage extends StatelessWidget {
  const MyOtherPage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: FrogColor(
        color: Colors.green,
        child: Text(
          'Hello Frog',
          style: TextStyle(color: FrogColor.of(context).color),
        ),
      ),
    );
  }
}
```

{@end-tool} {@youtube 560 315 https://www.youtube.com/watch?v=1t-8rBCGBYw}

另请参阅：

- [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 和 [State](https://www.yuque.com/thyname/flutter.widgets/state)，用于在其生命周期内可以多次以不同方式构建的 widget。
- [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget)，用于在给定特定配置和环境状态时始终以相同方式构建的 widget。
- [Widget](https://www.yuque.com/thyname/flutter.widgets/widget)，widget 概览。
- [InheritedNotifier](https://www.yuque.com/thyname/flutter.widgets/inheritednotifier)，一种继承 widget，其值可以是 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable)，并且每当该值发出通知时都会通知使用方。
- [InheritedModel](https://www.yuque.com/thyname/flutter.widgets/inheritedmodel)，一种继承 widget，允许客户端订阅其值的某些子部分的变化。

### InheritedWidget()

```dart
InheritedWidget({dynamic key, required Widget child})
```

抽象的 const 构造函数。此构造函数使子类能够提供 const 构造函数，以便可以在 const 表达式中使用它们。

### createElement()

```dart
InheritedElement createElement()
```

### updateShouldNotify()

```dart
bool updateShouldNotify(InheritedWidget oldWidget)
```

框架是否应通知继承自此 widget 的 widget。

当此 widget 重建时，有时我们需要重建继承自此 widget 的 widget，但有时则不需要。例如，如果此 widget 所持有的数据与 `oldWidget` 所持有的数据相同，那么就不需要重建继承了 `oldWidget` 所持有数据的那些 widget。

框架通过以树中此前占据此位置的 widget 作为参数调用此函数，来区分这些情况。所给定的 widget 保证与此对象具有相同的 [runtimeType]。

# RenderObjectWidget

```dart
abstract class RenderObjectWidget extends Widget {}
```

[RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 为 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 提供配置，后者包装 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)，而 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 负责应用程序的实际渲染工作。

通常，渲染对象 widget 不会直接子类化 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget)，而是子类化以下几种之一：

- [LeafRenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/leafrenderobjectwidget)，如果该 widget 没有子节点。
- [SingleChildRenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/singlechildrenderobjectwidget)，如果该 widget 恰好有一个子节点。
- [MultiChildRenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/multichildrenderobjectwidget)，如果该 widget 接受一个子节点列表。
- [SlottedMultiChildRenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/slottedmultichildrenderobjectwidget)，如果该 widget 将其子节点组织在不同的命名槽位中。

子类必须实现 [createRenderObject] 和 [updateRenderObject]。

### RenderObjectWidget()

```dart
RenderObjectWidget({dynamic key})
```

抽象的 const 构造函数。此构造函数使子类能够提供 const 构造函数，以便可以在 const 表达式中使用它们。

### createElement()

```dart
RenderObjectElement createElement()
```

RenderObjectWidget 总是膨胀为一个 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 的子类。

### createRenderObject()

```dart
RenderObject createRenderObject(BuildContext context)
```

使用此 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 所描述的配置，创建此 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 所代表的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 类的一个实例。

此方法不应对渲染对象的子节点做任何处理。这应该由在此对象的 [createElement] 方法所渲染对象中重写 [RenderObjectElement.mount] 的方法来处理。例如参见 [SingleChildRenderObjectElement.mount]。

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderObject renderObject)
```

将此 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 所描述的配置复制到给定的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)，该渲染对象的类型与此对象的 [createRenderObject] 所返回的类型相同。

此方法不应对更新渲染对象的子节点做任何处理。这应该由在此对象的 [createElement] 方法所渲染对象中重写 [RenderObjectElement.update] 的方法来处理。例如参见 [SingleChildRenderObjectElement.update]。

### didUnmountRenderObject()

```dart
void didUnmountRenderObject(RenderObject renderObject)
```

当先前与此 widget 关联的 RenderObject 从渲染树中移除时，会调用此方法。所提供的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的类型将与此 widget 的 [createRenderObject] 方法所创建的类型相同。

# LeafRenderObjectWidget

```dart
abstract class LeafRenderObjectWidget extends RenderObjectWidget {}
```

用于配置没有子节点的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 子类的 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 的父类。

子类必须实现 [createRenderObject] 和 [updateRenderObject]。

### LeafRenderObjectWidget()

```dart
LeafRenderObjectWidget({dynamic key})
```

抽象的 const 构造函数。此构造函数使子类能够提供 const 构造函数，以便可以在 const 表达式中使用它们。

### createElement()

```dart
LeafRenderObjectElement createElement()
```

# SingleChildRenderObjectWidget

```dart
abstract class SingleChildRenderObjectWidget extends RenderObjectWidget {}
```

用于配置拥有单个子节点槽位的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 子类的 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 的父类。

分配给此 widget 的渲染对象应利用 [RenderObjectWithChildMixin](https://www.yuque.com/thyname/flutter.rendering/renderobjectwithchildmixin) 来实现单子节点模型。该 mixin 暴露了一个 [RenderObjectWithChildMixin.child] 属性，允许获取属于 [child] widget 的渲染对象。

子类必须实现 [createRenderObject] 和 [updateRenderObject]。

### SingleChildRenderObjectWidget()

```dart
SingleChildRenderObjectWidget({dynamic key, Widget? child})
```

抽象的 const 构造函数。此构造函数使子类能够提供 const 构造函数，以便可以在 const 表达式中使用它们。

### child

```dart
Widget? child
```

树中位于此 widget 下方的 widget。

{@macro flutter.widgets.ProxyWidget.child}

### createElement()

```dart
SingleChildRenderObjectElement createElement()
```

# MultiChildRenderObjectWidget

```dart
abstract class MultiChildRenderObjectWidget extends RenderObjectWidget {}
```

用于配置拥有单个子节点列表的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 子类的 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 的父类。（此父类仅提供该子节点列表的存储，并不实际提供更新逻辑。）

子类必须使用混入了 [ContainerRenderObjectMixin](https://www.yuque.com/thyname/flutter.rendering/containerrenderobjectmixin) 的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)，该 mixin 提供了访问容器渲染对象（属于 [children] widget 的渲染对象）的子节点所需的功能。通常，子类会使用同时混入了 [ContainerRenderObjectMixin](https://www.yuque.com/thyname/flutter.rendering/containerrenderobjectmixin) 和 [RenderBoxContainerDefaultsMixin](https://www.yuque.com/thyname/flutter.rendering/renderboxcontainerdefaultsmixin) 的 [RenderBox](https://www.yuque.com/thyname/flutter.rendering/renderbox)。

子类必须实现 [createRenderObject] 和 [updateRenderObject]。

另请参阅：

- [Stack](https://www.yuque.com/thyname/flutter.widgets/stack)，它使用了 [MultiChildRenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/multichildrenderobjectwidget)。
- [RenderStack](https://www.yuque.com/thyname/flutter.rendering/renderstack)，相关渲染对象的一个实现示例。
- [SlottedMultiChildRenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/slottedmultichildrenderobjectwidget)，它配置的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 并非拥有单个子节点列表，而是将其子节点组织在命名槽位中。

### MultiChildRenderObjectWidget()

```dart
MultiChildRenderObjectWidget({dynamic key, List<Widget> children = const <Widget>[]})
```

为子类初始化字段。

### children

```dart
List<Widget> children
```

树中位于此 widget 下方的 widget。

如果这个列表将会被修改，通常明智的做法是为每个子 widget 设置一个 [Key](https://www.yuque.com/thyname/flutter.foundation/key)，以便框架能够将旧的配置与新的配置匹配起来，并保持底层渲染对象不变。

另外，Flutter 中的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 是不可变的，因此直接修改 [children]，例如 `someMultiChildRenderObjectWidget.children.add(...)` 或如下方示例代码，都会导致错误的行为。每当 children 列表被修改时，都应该提供一个新的列表对象。

```dart
// 这段代码是错误的。
class SomeWidgetState extends State<SomeWidget> {
  final List<Widget> _children = <Widget>[];

  void someHandler() {
    setState(() {
      _children.add(const ChildWidget());
    });
  }

  @override
  Widget build(BuildContext context) {
    // 在这里复用 `List<Widget> _children` 是有问题的。
    return Row(children: _children);
  }
}
```

以下代码修正了上面提到的问题。

```dart
class SomeWidgetState extends State<SomeWidget> {
  final List<Widget> _children = <Widget>[];

  void someHandler() {
    setState(() {
      // 这里的 key 使得 Flutter 即使在 children 列表被重新创建时
      // 也能够复用底层渲染对象。
      _children.add(ChildWidget(key: UniqueKey()));
    });
  }

  @override
  Widget build(BuildContext context) {
    // 由于 Widget 是不可变的，始终创建一个新的 children 列表。
    return Row(children: _children.toList());
  }
}
```

### createElement()

```dart
MultiChildRenderObjectElement createElement()
```

# ElementVisitor

```dart
typedef ElementVisitor = void Function(Element element)
```

[BuildContext.visitChildElements] 的回调签名。

参数是正在被访问的子节点。

在此回调中重入地调用 `element.visitChildElements` 是安全的。

# ConditionalElementVisitor

```dart
typedef ConditionalElementVisitor = bool Function(Element element)
```

[BuildContext.visitAncestorElements] 的回调签名。

参数是正在被访问的祖先节点。

返回 false 以停止遍历。

# BuildContext

```dart
abstract class BuildContext {}
```

指向某个 widget 在 widget 树中位置的句柄。

此类提供了一组方法，可在 [StatelessWidget.build] 方法以及 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象上的方法中使用。

[BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 对象会被传递给 [WidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/widgetbuilder) 函数（例如 [StatelessWidget.build]），并且可以通过 [State.context] 成员获取。一些静态函数（例如 [showDialog](https://www.yuque.com/thyname/flutter.material/showdialog)、[Theme.of] 等）也会接受构建上下文，以便它们能够代表调用方 widget 执行操作，或者为给定的上下文获取特定的数据。

每个 widget 都有自己的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)，它会成为由 [StatelessWidget.build] 或 [State.build] 函数所返回 widget 的父节点。（类似地，对于 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget)，它也是任何子节点的父节点。）

具体来说，这意味着在一个 build 方法内部，拥有该 build 方法的 widget 的构建上下文，与该 build 方法所返回的 widget 的构建上下文并不相同。这可能导致一些棘手的情形。例如，[Theme.of(context)] 会查找给定构建上下文最近的祖先 [Theme](https://www.yuque.com/thyname/flutter.material/theme)。如果某个 widget Q 的 build 方法在其返回的 widget 树中包含了一个 [Theme](https://www.yuque.com/thyname/flutter.material/theme)，并且尝试用自己的 context 调用 [Theme.of]，那么 Q 的 build 方法将无法找到那个 [Theme](https://www.yuque.com/thyname/flutter.material/theme) 对象。它找到的将是 widget Q 的祖先中存在的那个 [Theme](https://www.yuque.com/thyname/flutter.material/theme)。如果需要所返回树某个子部分的构建上下文，可以使用 [Builder](https://www.yuque.com/thyname/flutter.widgets/builder) widget：传递给 [Builder.builder] 回调的构建上下文将是 [Builder](https://www.yuque.com/thyname/flutter.widgets/builder) 自身的上下文。

例如，在以下代码片段中，[ScaffoldState.showBottomSheet] 方法是在 build 方法自身所创建的 [Scaffold](https://www.yuque.com/thyname/flutter.material/scaffold) widget 上调用的。如果没有使用 [Builder](https://www.yuque.com/thyname/flutter.widgets/builder)，而是直接使用了 build 方法自身的 `context` 参数，那么将找不到任何 [Scaffold](https://www.yuque.com/thyname/flutter.material/scaffold)，[Scaffold.of] 函数也会返回 null。

```dart
@override
Widget build(BuildContext context) {
  // 在这里，Scaffold.of(context) 返回 null
  return Scaffold(
    appBar: AppBar(title: const Text('Demo')),
    body: Builder(
      builder: (BuildContext context) {
        return TextButton(
          child: const Text('BUTTON'),
          onPressed: () {
            Scaffold.of(context).showBottomSheet(
              (BuildContext context) {
                return Container(
                  alignment: Alignment.center,
                  height: 200,
                  color: Colors.amber,
                  child: Center(
                    child: Column(
                      mainAxisSize: MainAxisSize.min,
                      children: <Widget>[
                        const Text('BottomSheet'),
                        ElevatedButton(
                          child: const Text('Close BottomSheet'),
                          onPressed: () {
                            Navigator.pop(context);
                          },
                        )
                      ],
                    ),
                  ),
                );
              },
            );
          },
        );
      },
    )
  );
}
```

特定 widget 的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 可能会随着该 widget 在树中移动而随时间改变位置。正因如此，此类方法返回的值不应在单次同步函数执行范围之外被缓存。

{@youtube 560 315 https://www.youtube.com/watch?v=rIaaH87z1-g}

避免存储 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的实例，因为一旦与之关联的 widget 从 widget 树中卸载，这些实例可能会变得无效。{@template flutter.widgets.BuildContext.asynchronous_gap} 如果某个 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 在异步间隙之后（即执行了某个异步操作之后）被使用，请考虑检查 [mounted]，以在与该上下文交互之前确定它是否仍然有效：

```dart
  @override
  Widget build(BuildContext context) {
    return OutlinedButton(
      onPressed: () async {
        await Future<void>.delayed(const Duration(seconds: 1));
        if (context.mounted) {
          Navigator.of(context).pop();
        }
      },
      child: const Text('Delayed pop'),
    );
  }
```

{@endtemplate}

[BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 对象实际上就是 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 对象。[BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 接口的存在是为了不鼓励直接操作 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 对象。

### widget

```dart
Widget get widget
```

作为此 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 当前的配置。

### owner

```dart
BuildOwner? get owner
```

此上下文所属的 [BuildOwner](https://www.yuque.com/thyname/flutter.widgets/buildowner)。[BuildOwner](https://www.yuque.com/thyname/flutter.widgets/buildowner) 负责管理此上下文的渲染管线。

### mounted

```dart
bool get mounted
```

与此上下文关联的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 当前是否已挂载在 widget 树中。

只有在 mounted 为 true 时，访问 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的属性或调用其上的任何方法才是有效的。如果 mounted 为 false，将触发断言。

一旦卸载，给定的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 将永远不会再次变为已挂载状态。

{@macro flutter.widgets.BuildContext.asynchronous_gap}

### debugDoingBuild

```dart
bool get debugDoingBuild
```

[widget] 当前是否正在更新 widget 树或渲染树。

对于 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 和 [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget)，此标志在其各自的 build 方法执行期间为 true。[RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 会在创建或配置其关联的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 期间将其设为 true。其他类型的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 也可能在概念上类似的阶段将其设为 true。

当此值为 true 时，[widget] 可以安全地通过调用 [dependOnInheritedElement] 或 [dependOnInheritedWidgetOfExactType] 来建立对某个 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 的依赖。

在发布（release）模式下访问此标志是无效的。

### findRenderObject()

```dart
RenderObject? findRenderObject()
```

该 widget 当前的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)。如果该 widget 是 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget)，这就是该 widget 为自身创建的渲染对象。否则，它就是第一个子孙 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 的渲染对象。

此方法只有在 build 阶段完成之后才会返回有效结果。因此在 build 方法中调用此方法是无效的。此方法只应在交互事件处理程序（例如手势回调）或布局、绘制回调中调用。如果 [State.mounted] 返回 false，调用此方法也是无效的。

如果该渲染对象是 [RenderBox](https://www.yuque.com/thyname/flutter.rendering/renderbox)（这是常见情形），那么可以通过 [size] 获取器获取该渲染对象的大小。这只有在布局阶段完成之后才有效，因此应仅在绘制回调或交互事件处理程序（例如手势回调）中查看。

关于一帧的不同阶段的详情，请参见 [WidgetsBinding.drawFrame] 处的讨论。

从理论上讲，调用此方法开销相对较大（相对于树的深度为 O(N)），但实际中通常开销很小，因为树中通常有很多渲染对象，因此到最近渲染对象的距离通常很短。

### size

```dart
Size? get size
```

[findRenderObject] 所返回 [RenderBox](https://www.yuque.com/thyname/flutter.rendering/renderbox) 的大小。

此获取器只有在布局阶段完成之后才会返回有效结果。因此在 build 方法中调用它是无效的。它只应在绘制回调或交互事件处理程序（例如手势回调）中调用。

关于一帧的不同阶段的详情，请参见 [WidgetsBinding.drawFrame] 处的讨论。

此获取器只有在 [findRenderObject] 实际返回一个 [RenderBox](https://www.yuque.com/thyname/flutter.rendering/renderbox) 时才会返回有效结果。如果 [findRenderObject] 返回的渲染对象不是 [RenderBox](https://www.yuque.com/thyname/flutter.rendering/renderbox) 的子类型（例如 [RenderView](https://www.yuque.com/thyname/flutter.rendering/renderview)），此获取器在调试模式下将抛出异常，在发布模式下将返回 null。

从理论上讲，调用此获取器开销相对较大（相对于树的深度为 O(N)），但实际中通常开销很小，因为树中通常有很多渲染对象，因此到最近渲染对象的距离通常很短。

### dependOnInheritedElement()

```dart
InheritedWidget dependOnInheritedElement(InheritedElement ancestor, {Object? aspect})
```

将此构建上下文注册到 [ancestor]，以便当 [ancestor] 的 widget 发生变化时，此构建上下文会被重建。

返回 `ancestor.widget`。

很少直接调用此方法。大多数应用应使用 [dependOnInheritedWidgetOfExactType]，它会在找到合适的 [InheritedElement](https://www.yuque.com/thyname/flutter.widgets/inheritedelement) 祖先之后调用此方法。

关于何时可以调用 [dependOnInheritedWidgetOfExactType] 的所有限定条件也同样适用于此方法。

### dependOnInheritedWidgetOfExactType()

```dart
T? dependOnInheritedWidgetOfExactType<T extends InheritedWidget>({Object? aspect})
```

返回给定类型 `T` 的最近 widget，并对其建立依赖；如果找不到合适的 widget，则返回 null。

所找到的 widget 将是一个具体的 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 子类，调用 [dependOnInheritedWidgetOfExactType] 会将此构建上下文注册到所返回的 widget 上。当该 widget 发生变化时（或者引入了该类型的新 widget，或者该 widget 消失时），此构建上下文会被重建，以便可以从该 widget 获取新的值。

{@template flutter.widgets.BuildContext.dependOnInheritedWidgetOfExactType} 通常这是通过 `of()` 静态方法隐式调用的，例如 [Theme.of]。

不应在 widget 构造函数或 [State.initState] 方法中调用此方法。虽然调用此方法实际上会将 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 注册为未来重建的依赖方，但构造函数和 [State.initState] 在生命周期上是锁定的，只会在初始创建该 element 时执行一次。

如果某个继承值随后发生变化，框架会正确地触发 [State.build] 方法重新运行，但无法重新运行构造函数或 [State.initState]。因此，如果任何内部变量、控制器或副作用是在这些一次性方法中使用继承值的"快照"进行初始化的，它们将保留其原始的、此时已过时的值。这会导致状态不同步：widget 的 [State.build] 方法可能正在使用更新后的数据，而其内部逻辑仍然绑定在 [State.initState] 期间捕获的过时数据上。

为确保 widget 保持同步，应（直接或间接地）在 build 方法、布局与绘制回调，或 [State.didChangeDependencies] 中调用此方法（或与之等价的方法）。

[State.didChangeDependencies] 会在 [State.initState] 之后立即被调用，并且每当此上下文所依赖的继承 widget 发生变化时都会被重新调用，直到该 widget 或其某个祖先下一次被移动为止（例如，因为添加或移除了一个祖先）。这使得 [State](https://www.yuque.com/thyname/flutter.widgets/state) 可以在调用 [State.build] 之前，更新依赖于该继承值的内部变量或执行相应的初始化逻辑。

不应在 [State.dispose] 中调用此方法，因为此时 element 树已不再稳定。要在该方法中引用某个祖先，应在 [State.didChangeDependencies] 中保存对该祖先的引用。在 [State.deactivate] 中使用此方法是安全的，该方法会在 widget 从树中移除时被调用。

也可以从交互事件处理程序（例如手势回调）或定时器中调用此方法，以获取一次性的值，只要该值不会被缓存和/或之后被复用。

调用此方法的开销是 O(1)（常数因子较小），但会导致该 widget 更频繁地被重建。

[aspect] 参数仅在 `T` 是支持局部更新的 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 子类（例如 [InheritedModel](https://www.yuque.com/thyname/flutter.widgets/inheritedmodel)）时使用。它指定此上下文依赖于该继承 widget 的哪个"方面"。{@endtemplate}

### getInheritedWidgetOfExactType()

```dart
T? getInheritedWidgetOfExactType<T extends InheritedWidget>()
```

返回给定 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 子类 `T` 的最近 widget；如果找不到合适的祖先，则返回 null。

{@template flutter.widgets.BuildContext.getInheritedWidgetOfExactType} 此方法不会像更常用的 [dependOnInheritedWidgetOfExactType] 那样引入依赖，因此当该 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 发生变化时，此上下文不会被重建。此函数适用于那些不希望产生依赖的少见用例。

不应在 [State.dispose] 中调用此方法，因为此时 element 树已不再稳定。要在该方法中引用某个祖先，应在 [State.didChangeDependencies] 中保存对该祖先的引用。在 [State.deactivate] 中使用此方法是安全的，该方法会在 widget 从树中移除时被调用。

也可以从交互事件处理程序（例如手势回调）或定时器中调用此方法，以获取一次性的值，只要该值不会被缓存和/或之后被复用。

调用此方法的开销是 O(1)（常数因子较小）。{@endtemplate}

### getElementForInheritedWidgetOfExactType()

```dart
InheritedElement? getElementForInheritedWidgetOfExactType<T extends InheritedWidget>()
```

获取与给定类型 `T` 的最近 widget 相对应的 element，`T` 必须是某个具体 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 子类的类型。

如果找不到这样的 element，则返回 null。

{@template flutter.widgets.BuildContext.getElementForInheritedWidgetOfExactType} 调用此方法的开销是 O(1)（常数因子较小）。

此方法不会像 [dependOnInheritedWidgetOfExactType] 那样与目标建立关联。

不应在 [State.dispose] 中调用此方法，因为此时 element 树已不再稳定。要在该方法中引用某个祖先，应在 [State.didChangeDependencies] 中通过调用 [dependOnInheritedWidgetOfExactType] 来保存对该祖先的引用。在 [State.deactivate] 中使用此方法是安全的，该方法会在 widget 从树中移除时被调用。{@endtemplate}

### findAncestorWidgetOfExactType()

```dart
T? findAncestorWidgetOfExactType<T extends Widget>()
```

返回给定类型 `T` 的最近祖先 widget，`T` 必须是某个具体 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 子类的类型。

{@template flutter.widgets.BuildContext.findAncestorWidgetOfExactType} 通常来说，[dependOnInheritedWidgetOfExactType] 更为有用，因为继承 widget 在发生变化时会触发使用方重建。此方法适用于在交互事件处理程序（例如手势回调）中使用，或用于执行一次性的任务，例如断言某个特定类型的 widget 是否存在于（或不存在于）祖先之中。widget 的 build 方法的返回值不应依赖于此方法的返回值，因为如果此方法的返回值发生变化，构建上下文并不会因此重建。这可能导致这样一种情形：build 方法中使用的数据发生了变化，但 widget 并未被重建。

调用此方法开销相对较大（相对于树的深度为 O(N)）。只有在已知此 widget 到目标祖先的距离较小且有界时，才应调用此方法。

不应在 [State.deactivate] 或 [State.dispose] 中调用此方法，因为此时 widget 树已不再稳定。要在这些方法中引用某个祖先，应在 [State.didChangeDependencies] 中通过调用 [findAncestorWidgetOfExactType] 来保存对该祖先的引用。

如果所请求类型的 widget 没有出现在此上下文的祖先中，则返回 null。{@endtemplate}

### findAncestorStateOfType()

```dart
T? findAncestorStateOfType<T extends State>()
```

返回是给定类型 `T` 实例的最近祖先 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) widget 的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象。

{@template flutter.widgets.BuildContext.findAncestorStateOfType} 不应在 build 方法中使用此方法，因为如果此方法可能返回的值发生变化，构建上下文并不会因此被重建。一般来说，对于这类情形，[dependOnInheritedWidgetOfExactType] 更为合适。此方法适用于以一次性方式改变某个祖先 widget 的状态，例如，使某个祖先滚动列表将此构建上下文的 widget 滚动到可见范围内，或者响应用户交互而改变焦点。

不过，总体而言，请考虑使用一个能够触发祖先中有状态变化的回调，而不是使用此方法所暗示的命令式风格。这样通常能带来更易维护、更可复用的代码，因为它将各个 widget 相互解耦。

调用此方法开销相对较大（相对于树的深度为 O(N)）。只有在已知此 widget 到目标祖先的距离较小且有界时，才应调用此方法。

不应在 [State.deactivate] 或 [State.dispose] 中调用此方法，因为此时 widget 树已不再稳定。要在这些方法中引用某个祖先，应在 [State.didChangeDependencies] 中通过调用 [findAncestorStateOfType] 来保存对该祖先的引用。{@endtemplate}

{@tool snippet}

```dart
ScrollableState? scrollable = context.findAncestorStateOfType<ScrollableState>();
```

{@end-tool}

### findRootAncestorStateOfType()

```dart
T? findRootAncestorStateOfType<T extends State>()
```

返回是给定类型 `T` 实例的最远祖先 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) widget 的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象。

{@template flutter.widgets.BuildContext.findRootAncestorStateOfType} 其作用方式与 [findAncestorStateOfType] 相同，但会持续访问后续的祖先，直到不再存在类型为 `T` 实例的祖先为止。然后返回最后找到的那一个。

此操作同样是 O(N)，不过这里的 N 是指整棵 widget 树，而不是某个子树。{@endtemplate}

### findAncestorRenderObjectOfType()

```dart
T? findAncestorRenderObjectOfType<T extends RenderObject>()
```

返回是给定类型 `T` 实例的最近祖先 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) widget 的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 对象。

{@template flutter.widgets.BuildContext.findAncestorRenderObjectOfType} 不应在 build 方法中使用此方法，因为如果此方法可能返回的值发生变化，构建上下文并不会因此被重建。一般来说，对于这类情形，[dependOnInheritedWidgetOfExactType] 更为合适。此方法仅适用于一些较为特殊的情形，即某个 widget 需要促使某个祖先改变其布局或绘制行为。例如，[Material](https://www.yuque.com/thyname/flutter.material/material) 使用此方法，以便 [InkWell](https://www.yuque.com/thyname/flutter.material/inkwell) widget 可以在 [Material](https://www.yuque.com/thyname/flutter.material/material) 实际的渲染对象上触发墨水飞溅（ink splash）效果。

调用此方法开销相对较大（相对于树的深度为 O(N)）。只有在已知此 widget 到目标祖先的距离较小且有界时，才应调用此方法。

不应在 [State.deactivate] 或 [State.dispose] 中调用此方法，因为此时 widget 树已不再稳定。要在这些方法中引用某个祖先，应在 [State.didChangeDependencies] 中通过调用 [findAncestorRenderObjectOfType] 来保存对该祖先的引用。{@endtemplate}

### visitAncestorElements()

```dart
void visitAncestorElements(ConditionalElementVisitor visitor)
```

从此构建上下文所属 widget 的父节点开始，沿祖先链向上遍历，对每个祖先调用参数所指定的函数。

{@template flutter.widgets.BuildContext.visitAncestorElements} 该回调会获得对祖先 widget 所对应 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 对象的引用。遍历会在到达根 widget 时，或当回调返回 false 时停止。该回调不得返回 null。

这对于检查 widget 树很有用。

调用此方法开销相对较大（相对于树的深度为 O(N)）。

不应在 [State.deactivate] 或 [State.dispose] 中调用此方法，因为此时 element 树已不再稳定。要在这些方法中引用某个祖先，应在 [State.didChangeDependencies] 中通过调用 [visitAncestorElements] 来保存对该祖先的引用。{@endtemplate}

### visitChildElements()

```dart
void visitChildElements(ElementVisitor visitor)
```

遍历此 widget 的子节点。

{@template flutter.widgets.BuildContext.visitChildElements} 这对于在子节点构建完成后、不等待下一帧就对它们应用更改非常有用，特别是在子节点已知的情况下，尤其是当只有恰好一个子节点时（对于 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 或 [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget) 来说，情况总是如此）。

对于对应 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 或 [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget) 的构建上下文而言，调用此方法开销非常小（O(1)，因为只有一个子节点）。

对于对应 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 的构建上下文而言，调用此方法可能开销较大（相对于子节点数量为 O(N)）。

递归调用此方法开销极大（相对于子孙节点数量为 O(N)），应尽可能避免。通常，使用 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 让子孙节点主动向上获取数据，要比递归使用 [visitChildElements] 将数据向下推送给它们廉价得多。{@endtemplate}

### dispatchNotification()

```dart
void dispatchNotification(Notification notification)
```

从给定的构建上下文开始，让此通知（notification）开始冒泡。

该通知将被传递给作为给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 祖先的、具有适当类型参数的任何 [NotificationListener](https://www.yuque.com/thyname/flutter.widgets/notificationlistener) widget。

### describeElement()

```dart
DiagnosticsNode describeElement(String name, {DiagnosticsTreeStyle style = DiagnosticsTreeStyle.errorProperty})
```

返回与当前构建上下文关联的 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 的描述。

`name` 通常类似于"The element being rebuilt was"这样的内容。

另请参阅：

- [Element.describeElements]，可用于描述一组 element。

### describeWidget()

```dart
DiagnosticsNode describeWidget(String name, {DiagnosticsTreeStyle style = DiagnosticsTreeStyle.errorProperty})
```

返回与当前构建上下文关联的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 的描述。

`name` 通常类似于"The widget being rebuilt was"这样的内容。

### describeMissingAncestor()

```dart
List<DiagnosticsNode> describeMissingAncestor({required Type expectedAncestorType})
```

为当前构建上下文的祖先树中缺失的某种特定类型的 widget 添加一条描述。

关于使用此方法的示例，可参见 [debugCheckHasMaterial](https://www.yuque.com/thyname/flutter.material/debugcheckhasmaterial)。

### describeOwnershipChain()

```dart
DiagnosticsNode describeOwnershipChain(String name)
```

为从某个特定 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 出发的所属链（ownership chain）添加一条描述，并加入错误报告中。

所属链有助于调试 element 的来源。

# BuildScope

```dart
final class BuildScope {}
```

用于确定 [BuildOwner.buildScope] 操作范围的类。

[BuildOwner.buildScope] 方法会重建所有与其 `context` 参数拥有相同 [Element.buildScope] 的脏（dirty）[Element](https://www.yuque.com/thyname/flutter.widgets/element)，并跳过那些 [Element.buildScope] 不同的 element。

默认情况下，[Element](https://www.yuque.com/thyname/flutter.widgets/element) 与其父节点拥有相同的 `buildScope`。特殊的 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 可以重写 [Element.buildScope]，为其子孙节点创建一个独立的构建作用域。例如，[LayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/layoutbuilder) widget 建立了自己的 [BuildScope](https://www.yuque.com/thyname/flutter.widgets/buildscope)，使得在传入的约束已知之前，任何子孙 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 都不会过早地重建。

### BuildScope()

```dart
BuildScope({VoidCallback? scheduleRebuild})
```

创建一个带有可选 [scheduleRebuild] 回调的 [BuildScope](https://www.yuque.com/thyname/flutter.widgets/buildscope)。

### scheduleRebuild

```dart
VoidCallback? scheduleRebuild
```

一个可选的 [VoidCallback](https://www.yuque.com/thyname/dart.ui/voidcallback)，当此 [BuildScope](https://www.yuque.com/thyname/flutter.widgets/buildscope) 中的 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 首次被标记为脏（dirty）时会被调用。

此回调通常意味着必须在本帧稍后的某个时刻调用 [BuildOwner.buildScope] 方法，以重建此 [BuildScope](https://www.yuque.com/thyname/flutter.widgets/buildscope) 中的脏 element。如果此作用域正在被 [BuildOwner.buildScope] 主动构建，则不会调用此回调，因为当 [BuildOwner.buildScope] 返回时，该 [BuildScope](https://www.yuque.com/thyname/flutter.widgets/buildscope) 将处于干净状态。

# BuildOwner

```dart
class BuildOwner {}
```

widget 框架的管理类。

此类追踪哪些 widget 需要重建，并处理适用于整个 widget 树的其他任务，例如管理树的未激活 element 列表，以及在调试时热重载期间在必要时触发"reassemble"命令。

主 build owner 通常由 [WidgetsBinding](https://www.yuque.com/thyname/flutter.widgets/widgetsbinding) 持有，并由操作系统驱动，与构建/布局/绘制管线的其余部分一起运作。

可以构建额外的 build owner，用于管理屏幕外的 widget 树。

要为某棵树指定一个 build owner，可在该树的根 element 上使用 [RootElementMixin.assignOwner] 方法。

{@tool dartpad} 此示例展示了如何构建一棵屏幕外的 widget 树，用于测量所渲染树的布局大小。对于某些使用场景，更简单的 [Offstage](https://www.yuque.com/thyname/flutter.widgets/offstage) widget 可能是此方法的更好替代方案。

** 参见 examples/api/lib/widgets/framework/build_owner.0.dart 中的代码 ** {@end-tool}

### BuildOwner()

```dart
BuildOwner({VoidCallback? onBuildScheduled, FocusManager? focusManager})
```

创建一个用于管理 widget 的对象。

如果未指定 `focusManager` 参数或其为 null，此构造函数将构造一个新的 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager)，并通过 [FocusManager.registerGlobalHandlers] 注册其全局输入处理程序，这会修改静态状态。希望避免更改此状态的调用方可以在此显式传入一个 focus manager。

### onBuildScheduled

```dart
VoidCallback? onBuildScheduled
```

在每一次构建过程中，当第一个可构建的 element 被标记为脏时调用。

### focusManager

```dart
FocusManager focusManager
```

负责管理焦点树的对象。

很少直接使用。通常，可考虑使用 [FocusScope.of] 来获取给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)。

更多详情请参见 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager)。

此字段默认使用已通过 [FocusManager.registerGlobalHandlers] 注册其全局输入处理程序的 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager)。希望避免注册这些处理程序（以及更改相关静态状态）的调用方，可以显式向 [BuildOwner.new] 构造函数传入一个 focus manager。

### scheduleBuildFor()

```dart
void scheduleBuildFor(Element element)
```

将某个 element 添加到脏 element 列表中，以便在 [WidgetsBinding.drawFrame] 调用 [buildScope] 时对其进行重建。

### debugBuilding

```dart
bool get debugBuilding
```

此 widget 树当前是否处于构建阶段。

仅在启用断言时有效。

### lockState()

```dart
void lockState(VoidCallback callback)
```

建立一个禁止调用 [State.setState] 的作用域，并调用给定的 `callback`。

此机制用于确保，例如，[State.dispose] 不会调用 [State.setState]。

### buildScope()

```dart
void buildScope(Element context, [VoidCallback? callback])
```

为更新 widget 树建立一个作用域，并调用给定的 `callback`（如果有的话）。然后，按深度顺序构建所有通过 [scheduleBuildFor] 被标记为脏的 element。

此机制可防止 build 方法传递性地要求运行其他 build 方法，从而可能导致无限循环。

脏列表会在 `callback` 返回之后被处理，按深度顺序构建所有通过 [scheduleBuildFor] 被标记为脏的 element。如果在此方法运行期间有 element 被标记为脏，那么它们的深度必须比 `context` 节点更深，并且比本次处理过程中此前已构建的任何节点都更深。

如果要在不执行任何其他工作的情况下清空当前的脏列表，可以不带回调地调用此函数。这正是框架在每一帧中、在 [WidgetsBinding.drawFrame] 里所做的事情。

同一时间只能有一个 [buildScope] 处于活动状态。

[buildScope] 隐含地也是一个 [lockState] 作用域。

要在每次调用此方法时打印一条控制台消息，可将 [debugPrintBuildScope](https://www.yuque.com/thyname/flutter.widgets/debugprintbuildscope) 设为 true。在调试涉及 widget 未被标记为脏、或被过于频繁地标记为脏的问题时，这很有用。

### globalKeyCount

```dart
int get globalKeyCount
```

当前与此 build owner 所构建的 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 相关联的 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 实例数量。

### finalizeTree()

```dart
void finalizeTree()
```

通过卸载所有不再处于活动状态的 element，完成此次 element 构建过程。

由 [WidgetsBinding.drawFrame] 调用。

在调试模式下，这还会运行一些健全性检查，例如检查重复的全局键。

### reassemble()

```dart
void reassemble(Element root)
```

使以给定 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 为根的整个子树被完全重建。开发工具在应用代码发生变化并进行热重载时会使用此方法，以使 widget 树能够获取任何已更改的实现。

此操作开销较大，除开发期间外不应调用。

# NotifiableElementMixin

```dart
mixin NotifiableElementMixin on Element {}
```

混入此类以允许接收子 Element 派发的 [Notification](https://www.yuque.com/thyname/flutter.widgets/notification) 对象。

另请参阅：

- [NotificationListener](https://www.yuque.com/thyname/flutter.widgets/notificationlistener)，一个允许消费通知的 Widget。

### onNotification()

```dart
bool onNotification(Notification notification)
```

当适当类型的通知到达树中的此位置时调用。

返回 true 以取消通知的冒泡。返回 false 以允许通知继续派发给更上层的祖先节点。

### attachNotificationTree()

```dart
void attachNotificationTree()
```

# Element

```dart
abstract class Element extends DiagnosticableTree implements BuildContext {}
```

[Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 在树中特定位置的实例化。

Widget 描述了如何配置一个子树，但同一个 Widget 可以同时用于配置多个子树，因为 Widget 是不可变的。[Element](https://www.yuque.com/thyname/flutter.widgets/element) 表示在树中特定位置使用某个 Widget 进行配置。随着时间推移，与给定元素关联的 Widget 可能会发生变化，例如，当父 Widget 重建并为此位置创建一个新 Widget 时。

Element 构成一棵树。大多数 Element 只有一个唯一的子节点，但某些 Widget（例如 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 的子类）可以拥有多个子节点。

Element 具有以下生命周期：

- 框架通过在将用作 Element 初始配置的 Widget 上调用 [Widget.createElement] 来创建一个 Element。
- 框架调用 [mount] 将新创建的 Element 添加到树中给定父节点的给定插槽（slot）处。[mount] 方法负责扩展（inflate）任何子 Widget，并在必要时调用 [attachRenderObject] 以将关联的渲染对象附加到渲染树上。
- 此时，该 Element 被视为"活动的"（active），并可能出现在屏幕上。
- 在某个时刻，父节点可能决定更改用于配置此 Element 的 Widget，例如因为父节点使用新状态重建。发生这种情况时，框架将使用新 Widget 调用 [update]。新 Widget 的 [runtimeType] 和 key 始终与旧 Widget 相同。如果父节点希望更改此树位置处 Widget 的 [runtimeType] 或 key，可以通过卸载此 Element 并在此位置扩展新 Widget 来实现。
- 在某个时刻，祖先节点可能决定从树中移除此 Element（或某个中间祖先节点），祖先节点通过在自身上调用 [deactivateChild] 来实现。停用中间祖先节点将从渲染树中移除该 Element 的渲染对象，并将此 Element 添加到 [owner] 的非活动元素列表中，从而促使框架在此 Element 上调用 [deactivate]。
- 此时，该 Element 被视为"非活动的"（inactive），不会出现在屏幕上。Element 只能在当前动画帧结束前保持非活动状态。在动画帧结束时，任何仍处于非活动状态的 Element 都将被卸载。
- 如果该 Element 被重新纳入树中（例如，因为它或其某个祖先节点具有一个被重复使用的全局键），框架会将该 Element 从 [owner] 的非活动元素列表中移除，在该 Element 上调用 [activate]，并将该 Element 的渲染对象重新附加到渲染树上。（此时，该 Element 再次被视为"活动的"，并可能出现在屏幕上。）
- 如果该 Element 在当前动画帧结束前未被重新纳入树中，框架将在该 Element 上调用 [unmount]。
- 此时，该 Element 被视为"失效的"（defunct），今后将不再被纳入树中。

### Element()

```dart
Element(Widget widget)
```

创建一个使用给定 Widget 作为其配置的 Element。

通常由 [Widget.createElement] 的重写方法调用。

### operator ==()

```dart
bool operator ==(Object other)
```

比较两个 Widget 是否相等。

当一个 Widget 被另一个根据 `operator ==` 比较相等的 Widget 重建时，框架会假定此次更新是多余的，并跳过更新该分支子树的工作。

通常不建议在任何具有子节点的 Widget 上重写 `operator ==`，因为正确的实现必须委托给子节点的相等运算符，而这是一个 O(N²) 的操作：每个子节点都需要自行遍历其所有子节点，在树的每一层都是如此。

对于叶子 Widget（没有子节点的 Widget），如果重建该 Widget 的开销明显大于检查 Widget 参数是否相等，并且预期该 Widget 会经常使用相同的参数被重建，那么实现此方法是合理的。

然而，通常更高效的做法是，在已知构建方法中使用的 Widget 不会改变的情况下，缓存这些 Widget。

### slot

```dart
Object? get slot
```

由父节点设置的信息，用于定义此子节点在父节点子节点列表中的位置。

子 Widget 的 slot 在父节点调用其 [updateChild] 方法以扩展该子 Widget 时确定。有关 slot 的更多详细信息，请参阅 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement)。

### depth

```dart
int get depth
```

一个整数，保证大于其父节点的深度（如果有父节点的话）。树根处的 Element 深度必须大于 0。

### widget

```dart
Widget get widget
```

此 Element 的配置。

应避免在 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 子类型上重写此字段以提供更具体的 Widget 类型（即 [StatelessElement](https://www.yuque.com/thyname/flutter.widgets/statelesselement) 和 [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget)）。相反，应在需要更具体类型的调用点进行类型转换。这样可以避免该获取器（getter）产生显著的转换开销——该获取器在构建阶段会在框架内部被频繁访问，而更具体的类型信息在此处并不会被用到。

### mounted

```dart
bool get mounted
```

### debugIsDefunct

```dart
bool get debugIsDefunct
```

如果该 Element 已失效，则返回 true。

此获取器在 profile 和 release 构建中始终返回 false。有关更多信息，请参阅 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 的生命周期文档。

### debugIsActive

```dart
bool get debugIsActive
```

如果该 Element 处于活动状态，则返回 true。

此获取器在 profile 和 release 构建中始终返回 false。有关更多信息，请参阅 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 的生命周期文档。

### owner

```dart
BuildOwner? get owner
```

管理此 Element 生命周期的对象。

### buildScope

```dart
BuildScope get buildScope
```

一个 [BuildScope](https://www.yuque.com/thyname/flutter.widgets/buildscope)，其脏（dirty）[Element](https://www.yuque.com/thyname/flutter.widgets/element) 只能通过 `context` 参数是此 [BuildScope](https://www.yuque.com/thyname/flutter.widgets/buildscope) 内某个 Element 的 [BuildOwner.buildScope] 调用来重建。

该获取器通常只有在此 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 已经 [mounted] 时访问才是安全的。

默认实现返回父 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 的 [buildScope]，因为在大多数情况下，一旦其祖先节点不再是脏的，[Element](https://www.yuque.com/thyname/flutter.widgets/element) 就可以准备好重建。一个值得注意的例外是 [LayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/layoutbuilder) 的后代节点，它们在传入约束可用之前不能重建。[LayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/layoutbuilder) 的 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 重写了 [buildScope]，以确保其所有后代节点在传入约束确定之前都不能重建。

如果你选择重写此获取器以建立自己的 [BuildScope](https://www.yuque.com/thyname/flutter.widgets/buildscope)，为了刷新该 [BuildScope](https://www.yuque.com/thyname/flutter.widgets/buildscope) 中的脏 [Element](https://www.yuque.com/thyname/flutter.widgets/element)，你需要在适当的时候手动调用 [BuildOwner.buildScope]，并传入你的 [BuildScope](https://www.yuque.com/thyname/flutter.widgets/buildscope) 的根 [Element](https://www.yuque.com/thyname/flutter.widgets/element)，因为 Flutter 框架不会尝试注册或管理自定义的 [BuildScope](https://www.yuque.com/thyname/flutter.widgets/buildscope)。

如果重写此获取器，请始终返回相同的 [BuildScope](https://www.yuque.com/thyname/flutter.widgets/buildscope) 实例。不支持在运行时更改此获取器返回的值。

[updateChild] 方法会忽略 [buildScope]：如果父 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 对某个具有不同 [BuildScope](https://www.yuque.com/thyname/flutter.widgets/buildscope) 的子节点调用 [updateChild]，该子节点仍然可能重建。

另请参阅：

- [LayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/layoutbuilder)，一个建立自定义 [BuildScope](https://www.yuque.com/thyname/flutter.widgets/buildscope) 的 Widget。

### reassemble()

```dart
void reassemble()
```

{@template flutter.widgets.Element.reassemble} 在调试期间每次应用重新组装（reassemble）时调用，例如在热重载（hot reload）期间。

此方法应重新运行任何依赖于全局状态的初始化逻辑，例如从资源包（asset bundle）加载图片（因为资源包可能已发生变化）。

此函数仅在开发期间被调用。在 release 构建中，`ext.flutter.reassemble` 钩子不可用，因此这段代码永远不会执行。

实现者不应依赖热重载源代码更新、reassemble 和 build 方法在热重载启动后的任何特定调用顺序。有可能一个 [Timer](https://www.yuque.com/thyname/dart.async/timer)（例如一个 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)）或附加到该 isolate 的调试会话会在 reassemble 被调用之前触发一次构建。依赖于 reassemble 在热重载后设置的前置条件的代码，必须能够容忍被乱序调用，例如通过静默失效而不是抛出异常来实现。也就是说，一旦 reassemble 被调用，build 之后至少会被调用一次。{@endtemplate}

另请参阅：

- [State.reassemble]
- [BindingBase.reassembleApplication]
- [Image](https://www.yuque.com/thyname/dart.ui/image)，它使用此方法来重新加载图片。

### renderObject

```dart
RenderObject? get renderObject
```

树中此位置（或其下方）的渲染对象。

如果此对象是一个 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement)，则渲染对象就是树中此位置的对象。否则，此获取器将沿树向下遍历，直到找到一个 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement)。

树中的某些位置没有对应的渲染对象。在这些情况下，此获取器返回 null。如果该 Element 位于 [View](https://www.yuque.com/thyname/flutter.widgets/view) 之外，就可能发生这种情况，因为只有根植于某个 view 的 Element 子树才具有与之关联的渲染树。

### renderObjectAttachingChild

```dart
Element? get renderObjectAttachingChild
```

返回此 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 的子节点，该子节点会将一个 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 插入到此 Element 的祖先节点中，以构建渲染树。

如果此 Element 没有任何需要将 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 附加到此 Element 祖先节点的子节点，则返回 null。因此，[RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 将返回 null，因为其子节点会将它们的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 插入到该 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 本身，而不是插入到该 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 的祖先节点中。

此外，对于那些自行承载独立渲染树、并不扩展祖先渲染树的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)，此方法也可能返回 null。

### describeMissingAncestor()

```dart
List<DiagnosticsNode> describeMissingAncestor({required Type expectedAncestorType})
```

### describeElements()

```dart
DiagnosticsNode describeElements(String name, Iterable<Element> elements)
```

将一组 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 添加到错误报告中，返回一个列表。

### describeElement()

```dart
DiagnosticsNode describeElement(String name, {DiagnosticsTreeStyle style = DiagnosticsTreeStyle.errorProperty})
```

### describeWidget()

```dart
DiagnosticsNode describeWidget(String name, {DiagnosticsTreeStyle style = DiagnosticsTreeStyle.errorProperty})
```

### describeOwnershipChain()

```dart
DiagnosticsNode describeOwnershipChain(String name)
```

### visitChildren()

```dart
void visitChildren(ElementVisitor visitor)
```

对每个子节点调用该参数（函数）。支持拥有子节点的子类必须重写此方法。

访问子节点的顺序不作保证，但应随时间保持一致。

在构建期间调用此方法是危险的：此时子节点列表可能仍在更新中，因此子节点可能尚未构建完成，或者可能是即将被替换的旧子节点。只有在能够证明子节点可用的情况下，才应调用此方法。

### debugVisitOnstageChildren()

```dart
void debugVisitOnstageChildren(ElementVisitor visitor)
```

对每个被视为在场（onstage）的子节点调用该参数。

[Offstage](https://www.yuque.com/thyname/flutter.widgets/offstage) 和 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 等类会重写此方法以隐藏其子节点。

是否在场会影响该 Element 在测试期间使用 Flutter 的 [Finder] 对象时的可发现性。例如，当你指示测试框架点击某个 Widget 时，默认情况下查找器（finder）只会查找在场的 Element，而忽略不在场的 Element。

默认实现委托给 [visitChildren]，因此将该 Element 视为在场。

另请参阅：

- [Offstage](https://www.yuque.com/thyname/flutter.widgets/offstage) Widget，用于隐藏其子节点。
- [Finder]，默认跳过不在场的 Widget。
- [RenderObject.visitChildrenForSemantics]，与此方法相对，专门用于将部分 UI 从语义树中排除。

### visitChildElements()

```dart
void visitChildElements(ElementVisitor visitor)
```

围绕 [visitChildren] 的封装，供 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 使用。

### updateChild()

```dart
Element? updateChild(Element? child, Widget? newWidget, Object? newSlot)
```

使用给定的新配置更新给定的子节点。

此方法是 Widget 系统的核心。每当我们要根据更新后的配置添加、更新或移除一个子节点时，都会调用此方法。

`newSlot` 参数指定此 Element 的 [slot] 的新值。

如果 `child` 为 null，且 `newWidget` 不为 null，那么我们需要为其创建一个新的子节点，即使用 `newWidget` 配置的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。

如果 `newWidget` 为 null，且 `child` 不为 null，那么我们需要移除该子节点，因为它不再具有配置。

如果两者都不为 null，那么我们需要将 `child` 的配置更新为 `newWidget` 给定的新配置。如果 `newWidget` 可以赋予现有子节点（由 [Widget.canUpdate] 决定），则如此赋予。否则，需要释放旧子节点，并为新配置创建一个新的子节点。

如果两者都为 null，那么我们既没有子节点，也不会有子节点，因此不做任何操作。

[updateChild] 方法的返回值：如果它必须创建一个新 Element，则返回该新 Element；如果它只需更新子节点，则返回传入的子节点；如果它移除了子节点且未进行替换，则返回 null。

下表总结了上述内容：

|                   | **newWidget == null**       | **newWidget != null**                                |
| :---------------: | :-------------------------- | :--------------------------------------------------- |
| **child == null** | 返回 null。                 | 返回新的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。                                 |
| **child != null** | 移除旧的子节点，返回 null。 | 尽可能更新旧的子节点，返回该子节点或新的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。 |

`newSlot` 参数仅在 `newWidget` 不为 null 时使用。如果 `child` 为 null（或旧的子节点无法更新），则 `newSlot` 会通过 [inflateWidget] 赋给为该子节点创建的新 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。如果 `child` 不为 null（且旧的子节点*可以*更新），则 `newSlot` 会传递给 [updateSlotForChild]，以更新其 slot，以防自上次构建以来它的位置发生了变化。

有关 slot 的更多信息，请参阅 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 文档。

### updateChildren()

```dart
List<Element> updateChildren(List<Element> oldChildren, List<Widget> newWidgets, {Set<Element>? forgottenChildren, List<Object?>? slots})
```

使用新的 Widget 更新此 Element 的子节点。

尝试使用给定的新 Widget 更新给定的旧子节点列表，移除失效的 Element 并按需引入新的 Element，然后返回新的子节点列表。

在此函数执行期间，`oldChildren` 列表不得被修改。如果调用者希望在此函数处于调用栈中时，以重入方式（reentrantly）从 `oldChildren` 中移除元素，调用者可以提供一个 `forgottenChildren` 参数，该参数可以在此函数处于调用栈中时被修改。每当此函数从 `oldChildren` 中读取时，它会首先检查该子节点是否在 `forgottenChildren` 中。如果是，则该函数的行为就如同该子节点不在 `oldChildren` 中一样。

此函数是围绕 [updateChild] 的一个便捷封装，[updateChild] 用于更新每个单独的子节点。如果 `slots` 不为 null，[updateChild] 的 `newSlot` 参数的值将使用当前处理的 `child` 在 `newWidgets` 列表中对应的索引，从该列表中获取（`newWidgets` 和 `slots` 的长度必须相同）。如果 `slots` 为 null，则使用 [IndexedSlot<Element>] 作为 `newSlot` 参数的值。在这种情况下，[IndexedSlot.index] 被设置为当前处理的 `child` 在 `newWidgets` 列表中对应的索引，[IndexedSlot.value] 被设置为该列表中前一个 Widget 的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)（如果是列表中的第一个子节点，则为 null）。

当某个 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 的 [slot] 值发生变化时，与之关联的 [renderObject] 需要移动到其父节点子节点列表中的新位置。如果该 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 以链表形式组织其子节点（如 [ContainerRenderObjectMixin](https://www.yuque.com/thyname/flutter.rendering/containerrenderobjectmixin) 所做的那样），可以通过将子节点 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 重新插入到列表中，紧跟在作为 [slot] 对象中 [IndexedSlot.value] 提供的 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 所关联的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 之后来实现。

然而，仅使用前一个兄弟节点作为 [slot] 是不够的，因为子节点 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 只有在其关联的 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 的 [slot] 被更新时才会移动。当子节点 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 的顺序发生变化时，列表中的某些元素可能会移动到新的索引位置，但仍然拥有相同的前一个兄弟节点。例如，当 `[e1, e2, e3, e4]` 变为 `[e1, e3, e4, e2]` 时，元素 e4 仍然以 e3 作为前一个兄弟节点，即使它在列表中的索引已经改变，并且它的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 需要移动到 e2 的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 之前。为了触发这次移动，每当某个 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 在其父节点子节点列表中的索引发生变化时，都需要为其分配一个新的 [slot] 值。使用 [IndexedSlot<Element>] 恰好实现了这一点，同时也确保了底层的父 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 通过 [slot] 对象中提供的新前一个兄弟节点，知道某个子节点需要移动到链表中的什么位置。

### mount()

```dart
void mount(Element? parent, Object? newSlot)
```

将此 Element 添加到给定父节点的给定 slot 中的树中。

当一个新创建的 Element 首次被添加到树中时，框架会调用此函数。使用此方法来初始化依赖于拥有父节点的状态。独立于父节点的状态则可以更方便地在构造函数中初始化。

此方法将该 Element 从"初始"（initial）生命周期状态转变为"活动"（active）生命周期状态。

重写此方法的子类很可能也需要重写 [update]、[visitChildren]、[RenderObjectElement.insertRenderObjectChild]、[RenderObjectElement.moveRenderObjectChild] 和 [RenderObjectElement.removeRenderObjectChild]。

此方法的实现应以调用继承方法开始，如 `super.mount(parent, newSlot)`。

### update()

```dart
void update(Widget newWidget)
```

更改用于配置此 Element 的 Widget。

当父节点希望使用不同的 Widget 配置此 Element 时，框架会调用此函数。新 Widget 保证与旧 Widget 具有相同的 [runtimeType]。

此函数仅在"活动"生命周期状态下被调用。

### updateSlotForChild()

```dart
void updateSlotForChild(Element child, Object? newSlot)
```

更改给定子节点在其父节点子节点列表中所占据的 slot。

当子节点在此 Element 的子节点列表中从一个位置移动到另一个位置时，由 [MultiChildRenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/multichildrenderobjectelement) 及其他具有多个子节点的 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 子类调用。

### updateSlot()

```dart
void updateSlot(Object? newSlot)
```

当框架需要更改此 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 在其祖先节点中所占据的 slot 时，由 [updateSlotForChild] 调用。

### detachRenderObject()

```dart
void detachRenderObject()
```

从渲染树中移除 [renderObject]。

此函数的默认实现会对每个子节点递归调用 [detachRenderObject]。[RenderObjectElement.detachRenderObject] 的重写方法执行将 [renderObject] 从渲染树中移除的实际工作。

此方法由 [deactivateChild] 调用。

### attachRenderObject()

```dart
void attachRenderObject(Object? newSlot)
```

将 [renderObject] 添加到渲染树中 `newSlot` 指定的位置。

此函数的默认实现会对每个子节点递归调用 [attachRenderObject]。[RenderObjectElement.attachRenderObject] 的重写方法执行将 [renderObject] 添加到渲染树中的实际工作。

`newSlot` 参数指定此 Element 的 [slot] 的新值。

### inflateWidget()

```dart
Element inflateWidget(Widget newWidget, Object? newSlot)
```

为给定 Widget 创建一个 Element，并将其作为此 Element 在给定 slot 中的子节点添加。

此方法通常由 [updateChild] 调用，但也可以由需要对创建 Element 进行更精细控制的子类直接调用。

如果给定的 Widget 具有全局键（global key），且已存在一个使用该全局键的 Widget 的 Element，此函数将复用该 Element（可能将其从树中的其他位置移植过来，或将其从非活动元素列表中重新激活），而不是创建一个新的 Element。

`newSlot` 参数指定此 Element 的 [slot] 的新值。

此函数返回的 Element 已经完成挂载，并处于"活动"生命周期状态。

### deactivateChild()

```dart
void deactivateChild(Element child)
```

将给定的 Element 移动到非活动元素列表中，并将其渲染对象从渲染树中分离。

此方法通过将给定 Element 的渲染对象从渲染树中分离，并将该 Element 移动到非活动元素列表中，从而使其不再作为此 Element 的子节点。

此方法（间接地）在该子节点上调用 [deactivate]。

调用者负责将该子节点从其子节点模型中移除。通常 [deactivateChild] 是由 Element 在更新其子节点模型时自行调用；但是，在 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 重新设置父节点期间，新父节点会主动调用旧父节点的 [deactivateChild]，此前会先使用 [forgetChild] 使旧父节点更新其子节点模型。

### forgetChild()

```dart
void forgetChild(Element child)
```

从该 Element 的子节点列表中移除给定的子节点，为该子节点在 Element 树中的其他位置被复用做准备。

这会更新子节点模型，从而使 [visitChildren] 等方法不再遍历该子节点。

调用此方法时，该 Element 仍将拥有一个有效的父节点，并且该子节点的 [Element.slot] 值在该父节点的上下文中仍然有效。此方法调用之后，将调用 [deactivateChild] 以切断与此对象的联系。

[update] 负责更新或创建将替换此 `child` 的新子节点。

### activate()

```dart
void activate()
```

从"非活动"生命周期状态转变为"活动"生命周期状态。

当一个先前被停用的 Element 被重新纳入树中时，框架会调用此方法。框架不会在 Element 首次变为活动状态时（即从"初始"生命周期状态开始时）调用此方法，而是在这种情况下调用 [mount]。

有关更多信息，请参阅 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 的生命周期文档。

此方法的实现应以调用继承方法开始，如 `super.activate()`。

### deactivate()

```dart
void deactivate()
```

从"活动"生命周期状态转变为"非活动"生命周期状态。

当一个先前处于活动状态的 Element 被移动到非活动元素列表中时，框架会调用此方法。在非活动状态下，该 Element 不会出现在屏幕上。该 Element 只能在当前动画帧结束前保持非活动状态。在动画帧结束时，如果该 Element 尚未被重新激活，框架将卸载该 Element。

如果在重建某个 Widget 子树时出现未捕获的异常，框架也会在失败的子树上调用此方法，以确保 Widget 树处于相对一致的状态。此类子树的停用仅在尽力而为（best-effort）的基础上执行，停用过程中抛出的错误不会被重新抛出。

此方法由 [deactivateChild] 间接调用。

有关更多信息，请参阅 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 的生命周期文档。

此方法的实现应以调用继承方法结束，如 `super.deactivate()`。

### debugDeactivated()

```dart
void debugDeactivated()
```

在子节点被停用后调用（参见 [deactivate]），仅限调试模式。

此方法不会在 release 构建中被调用。

### unmount()

```dart
void unmount()
```

从"非活动"生命周期状态转变为"失效"生命周期状态。

当框架确定一个非活动的 Element 永远不会被重新激活时调用。在每个动画帧结束时，框架会对任何剩余的非活动 Element 调用 [unmount]，以防止非活动 Element 保持非活动状态的时间超过一个动画帧。

此函数被调用后，该 Element 将不会再次被纳入树中。

此 Element 持有的任何资源都应在此时释放。例如，[RenderObjectElement.unmount] 会调用 [RenderObject.dispose] 并将其对渲染对象的引用置空。

有关更多信息，请参阅 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 的生命周期文档。

此方法的实现应以调用继承方法结束，如 `super.unmount()`。

### debugExpectsRenderObjectForSlot()

```dart
bool debugExpectsRenderObjectForSlot(Object? slot)
```

给定 `slot` 中的子节点（或其某个后代节点）是否必须通过在其祖先 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 上调用 [RenderObjectElement.insertRenderObjectChild] 来将一个 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 插入到该祖先节点中。

此方法用于在 Element 树中定义非渲染区域（有关渲染区域和非渲染区域的说明，请参阅 [WidgetsBinding](https://www.yuque.com/thyname/flutter.widgets/widgetsbinding)）：

Element 树的大多数分支最终都会将一个 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 插入到其 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 祖先节点中，以构建渲染树。然而，有一个值得注意的例外：某个 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 可能期望特定子节点 slot 的占用者创建一个新的独立渲染树，因此不允许将渲染对象插入现有渲染树中。对于这种情况，这些 Element 必须针对相应的 slot 从此方法返回 false，以向该 slot 中的子节点表明它不得在其祖先节点上调用 [RenderObjectElement.insertRenderObjectChild]。

例如，支撑 [ViewAnchor](https://www.yuque.com/thyname/flutter.widgets/viewanchor) 的 Element 会针对 [ViewAnchor.view] slot 从此方法返回 false，以强制要求该 slot 由例如 [View](https://www.yuque.com/thyname/flutter.widgets/view) Widget 占用，后者最终会为该 view 引导出一个独立的渲染树。另一个例子是 [ViewCollection](https://www.yuque.com/thyname/flutter.widgets/viewcollection) Widget，出于同样的原因，它会针对其所有 slot 返回 false。

重写此方法并不常见，因为表现出上述行为的 Element 很少见。

### findRenderObject()

```dart
RenderObject? findRenderObject()
```

### size

```dart
Size? get size
```

### doesDependOnInheritedElement()

```dart
bool doesDependOnInheritedElement(InheritedElement ancestor)
```

如果之前曾使用 [ancestor] 调用过 [dependOnInheritedElement]，则返回 `true`。

### dependOnInheritedElement()

```dart
InheritedWidget dependOnInheritedElement(InheritedElement ancestor, {Object? aspect})
```

### dependOnInheritedWidgetOfExactType()

```dart
T? dependOnInheritedWidgetOfExactType<T extends InheritedWidget>({Object? aspect})
```

### getInheritedWidgetOfExactType()

```dart
T? getInheritedWidgetOfExactType<T extends InheritedWidget>()
```

### getElementForInheritedWidgetOfExactType()

```dart
InheritedElement? getElementForInheritedWidgetOfExactType<T extends InheritedWidget>()
```

### attachNotificationTree()

```dart
void attachNotificationTree()
```

在 [Element.mount] 和 [Element.activate] 中调用，以将此 Element 注册到通知树中。

暴露此方法仅是为了使 [NotifiableElementMixin](https://www.yuque.com/thyname/flutter.widgets/notifiableelementmixin) 可以被实现。希望响应通知的 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 子类应改为混入该 mixin。

另请参阅：

- [NotificationListener](https://www.yuque.com/thyname/flutter.widgets/notificationlistener)，一个允许监听通知的 Widget。

### findAncestorWidgetOfExactType()

```dart
T? findAncestorWidgetOfExactType<T extends Widget>()
```

### findAncestorStateOfType()

```dart
T? findAncestorStateOfType<T extends State<StatefulWidget>>()
```

### findRootAncestorStateOfType()

```dart
T? findRootAncestorStateOfType<T extends State<StatefulWidget>>()
```

### findAncestorRenderObjectOfType()

```dart
T? findAncestorRenderObjectOfType<T extends RenderObject>()
```

### visitAncestorElements()

```dart
void visitAncestorElements(ConditionalElementVisitor visitor)
```

### didChangeDependencies()

```dart
void didChangeDependencies()
```

当此 Element 的某个依赖发生变化时调用。

[dependOnInheritedWidgetOfExactType] 会将此 Element 注册为依赖于给定类型的继承信息。当树中此位置该类型的信息发生变化时（例如，因为 [InheritedElement](https://www.yuque.com/thyname/flutter.widgets/inheritedelement) 更新为一个新的 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)，且 [InheritedWidget.updateShouldNotify] 返回 true），框架会调用此函数以通知此 Element 该变化。

### debugGetCreatorChain()

```dart
String debugGetCreatorChain(int limit)
```

返回一段描述导致此 Element 被创建的原因的文本。

用于调试某个 Element 的来源。

### debugGetDiagnosticChain()

```dart
List<Element> debugGetDiagnosticChain()
```

返回从此 Element 回溯到树根的父节点链。

用于以调试方式显示 Element 树，仅展开从根节点到此 Element 路径上的节点。

### dispatchNotification()

```dart
void dispatchNotification(Notification notification)
```

### toStringShort()

```dart
String toStringShort()
```

此 Element 的简短文本描述。

### toDiagnosticsNode()

```dart
DiagnosticsNode toDiagnosticsNode({String? name, DiagnosticsTreeStyle? style})
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

### dirty

```dart
bool get dirty
```

如果该 Element 已被标记为需要重建，则返回 true。

该标志在 Element 首次创建时以及每次调用 [markNeedsBuild] 后为 true。该标志通常在 [performRebuild] 的实现中被重置为 false，但某些 Element（例如 [LayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/layoutbuilder) Widget 的 Element）可能会选择重写 [markNeedsBuild]，使其在被调用时不将 [dirty] 标志设置为 `true`。

### markNeedsBuild()

```dart
void markNeedsBuild()
```

将该 Element 标记为脏，并将其添加到下一帧需要重建的 Widget 全局列表中。

由于在同一帧内构建同一个 Element 两次是低效的，应用程序和 Widget 的结构应确保只在帧开始之前的事件处理程序中将 Widget 标记为脏，而不是在构建过程本身中标记。

### rebuild()

```dart
void rebuild({bool force = false})
```

促使 Widget 自我更新。在调试构建中，还会验证各种不变量（invariant）。

由 [BuildOwner](https://www.yuque.com/thyname/flutter.widgets/buildowner) 在调用 [BuildOwner.scheduleBuildFor] 将此 Element 标记为脏时调用；也由 [mount] 在 Element 首次构建时调用；还由 [update] 在 Widget 发生变化时调用。

该方法只有在 [dirty] 为 true 时才会重建。要不论 [dirty] 标志如何都强制重建，可将 `force` 设置为 true。在 [update] 期间强制重建很方便，因为此时 [dirty] 为 false。

## 何时发生重建

### 术语

[Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 表示 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 的配置。每个 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 都有一个 Widget，由 [Element.widget] 指定。"widget" 这个术语常被用来代指，尽管严格来说使用 "element" 会更准确。

尽管一个 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 拥有一个当前的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget)，但随着时间推移，该 Widget 可能会被其他 Widget 替换。例如，支撑某个 [ColoredBox](https://www.yuque.com/thyname/flutter.widgets/coloredbox) 的 Element，其 Widget 最初可能是一个 [ColoredBox.color] 为蓝色的 [ColoredBox](https://www.yuque.com/thyname/flutter.widgets/coloredbox)，随后被赋予一个颜色为绿色的新 [ColoredBox](https://www.yuque.com/thyname/flutter.widgets/coloredbox)。

在任意特定时刻，同一棵树中的多个 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 可能拥有相同的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget)。例如，同一个颜色为绿色的 [ColoredBox](https://www.yuque.com/thyname/flutter.widgets/coloredbox) 可能同时在 Widget 树中的多个位置被使用，每个位置都由不同的 Element 支撑。

### 将 Element 标记为脏

一个 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 可以在帧与帧之间被标记为脏。这可能出于多种原因发生，包括以下几种：

- [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 可以通过调用 [State.setState] 方法使其 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 被标记为脏。
- 当一个 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 发生变化时，之前订阅过它的后代节点将被标记为脏。
- 在热重载期间，每个 Element 都会被标记为脏（使用 [Element.reassemble]）。

### 重建

脏的 Element 会在下一帧被重建。具体的重建方式取决于 Element 的种类。[StatelessElement](https://www.yuque.com/thyname/flutter.widgets/statelesselement) 通过其 Widget 的 [StatelessWidget.build] 方法进行重建。[StatefulElement](https://www.yuque.com/thyname/flutter.widgets/statefulelement) 通过其 Widget 的 state 的 [State.build] 方法进行重建。[RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 通过更新其 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 进行重建。

在许多情况下，重建的最终结果是单个子 Widget，或者（对于 [MultiChildRenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/multichildrenderobjectelement)）是一个子 Widget 列表。

这些子 Widget 用于更新该 Element 的子节点（或多个子节点）Element 的 [widget] 属性。如果新 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 具有与之相同的 [Type](https://www.yuque.com/thyname/dart.core/type) 和 [Key](https://www.yuque.com/thyname/flutter.foundation/key)，则认为该新 Widget 与现有 Element 相对应。（对于 [MultiChildRenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/multichildrenderobjectelement)，即使 Widget 的顺序发生变化，也会花费一些精力来追踪这些 Widget；请参阅 [RenderObjectElement.updateChildren]。）

如果没有对应的先前子节点，则会创建一个新的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)（使用 [Widget.createElement]）；然后该 Element 本身会被构建，如此递归下去。

如果之前存在一个子节点，但本次构建没有提供对应的子节点来更新它，那么旧的子节点将被丢弃（或者，在涉及 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 重新设置父节点的情况下，在 Element 树的其他位置被复用）。

然而，最常见的情况是，存在一个对应的先前子节点。这种情况通过要求子 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 使用新的子 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 自我更新来处理。对于 [StatefulElement](https://www.yuque.com/thyname/flutter.widgets/statefulelement)，这正是触发 [State.didUpdateWidget] 的原因。

### 不重建

在某个 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 被告知使用新的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 更新自身之前，会先使用 `operator ==` 比较新旧对象。

一般而言，这等价于使用 [identical](https://www.yuque.com/thyname/dart.core/identical) 来判断这两个对象是否确实是同一个实例。如果是，并且该 Element 尚未因其他原因被标记为脏，那么该 Element 会跳过自我更新，因为它可以确定更新自身或其后代节点没有任何价值。

强烈建议避免在 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 对象上重写 `operator ==`。虽然这样做看起来可以提升性能，但实际上，对于非叶子 Widget，这会导致 O(N²) 的行为。这是因为这种比较必然需要包含对子 Widget 的比较，而如果这些子 Widget 也实现了 `operator ==`，最终会导致对整个 Widget 树的完整遍历……而这一过程会在树的每一层重复进行。实际上，直接重建反而开销更小。（此外，如果应用程序中使用的*任何* [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 子类实现了 `operator ==`，那么编译器就无法在任何地方内联该比较，因为它必须将该调用视为虚调用，以防该实例恰好是一个重写了该运算符的实例。）

相反，避免不必要重建的最佳方式是缓存从 [State.build] 返回的 Widget，这样每一帧都会使用相同的 Widget，直到它们发生变化为止。存在多种机制来鼓励这样做：例如，`const` Widget 就是一种自动缓存的形式（如果一个 Widget 是使用 `const` 关键字构造的，那么每次使用相同参数构造时都会返回同一个实例）。

另一个例子是 [AnimatedBuilder.child] 属性，它允许子树中非动画部分保持静态，即使 [AnimatedBuilder.builder] 回调重新创建了其他组件。

### performRebuild()

```dart
void performRebuild()
```

促使 Widget 自我更新。

在完成适当的检查后由 [rebuild] 调用。

基础实现仅清除 [dirty] 标志。

# ErrorWidgetBuilder

```dart
typedef ErrorWidgetBuilder = Widget Function(FlutterErrorDetails details)
```

在构建 Widget 时发生错误时调用的构造函数的签名。

参数提供了有关错误原因的信息。

另请参阅：

- [ErrorWidget.builder]，可以设置它来重写默认的 [ErrorWidget](https://www.yuque.com/thyname/flutter.widgets/errorwidget) 构建器。
- [FlutterError.reportError]，通常在调用 [ErrorWidget.builder] 之前，使用相同的 [FlutterErrorDetails](https://www.yuque.com/thyname/flutter.foundation/fluttererrordetails) 对象调用。

# ErrorWidget

```dart
class ErrorWidget extends LeafRenderObjectWidget {}
```

渲染异常消息的 Widget。

当构建方法失败时使用此 Widget，以帮助确定问题所在。异常也会记录到控制台，你可以使用 `flutter logs` 查看。控制台还将包含其他信息，例如异常的堆栈跟踪。

可以重写此 Widget。

{@tool dartpad} 此示例展示了如何在 release 模式下重写标准的错误 Widget 构建器，同时在 debug 模式下使用标准构建器。

点击"Error Prone"按钮时会发生该错误。

** 参见 examples/api/lib/widgets/framework/error_widget.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [FlutterError.onError]，可以将其设置为一个方法，如果相比显示错误消息更倾向于退出应用程序，则可以调用该方法。
- <https://docs.flutter.dev/testing/errors>，关于错误处理的更多信息。

### ErrorWidget()

```dart
ErrorWidget(Object exception)
```

创建一个显示给定异常的 Widget。

消息将是给定异常的字符串化结果，除非计算该值本身会抛出异常，在这种情况下，消息将是字符串 "Error"。

如果从 IDE 或 devtools 检查此对象，且原始异常是一个 [FlutterError](https://www.yuque.com/thyname/flutter.foundation/fluttererror) 对象，检查输出中将显示原始异常本身。

### ErrorWidget.withDetails()

```dart
ErrorWidget.withDetails({String message = '', FlutterError? error})
```

创建一个显示给定错误消息的 Widget。

可以提供一个显式的 [FlutterError](https://www.yuque.com/thyname/flutter.foundation/fluttererror) 以报告给检查工具。它不需要与消息内容匹配。

### builder

```dart
ErrorWidgetBuilder builder
```

[ErrorWidget](https://www.yuque.com/thyname/flutter.widgets/errorwidget) 的可配置工厂。

当构建 Widget 时发生错误，出错的 Widget 将被此函数返回的 Widget 替换。默认情况下，会返回一个 [ErrorWidget](https://www.yuque.com/thyname/flutter.widgets/errorwidget)。

调用此函数时，系统通常处于不稳定状态。构建过程中（可能还有布局过程中）刚刚抛出了一个异常，因此周围的 Widget 和渲染对象可能处于相当脆弱的状态。框架本身（尤其是 [BuildOwner](https://www.yuque.com/thyname/flutter.widgets/buildowner)）也可能处于混乱状态，很可能会抛出更多异常。

正因如此，强烈建议此函数返回的 Widget 执行尽可能少的工作。[LeafRenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/leafrenderobjectwidget) 是最佳选择，尤其是对应于能够处理最荒谬的传入约束的 [RenderBox](https://www.yuque.com/thyname/flutter.rendering/renderbox) 的那种。默认构造函数映射到 [RenderErrorBox](https://www.yuque.com/thyname/flutter.rendering/rendererrorbox)。

默认行为是在 debug 模式下显示异常消息，在 release 构建中则只显示灰色背景，不显示任何内容。

另请参阅：

- [FlutterError.onError]，通常在调用此回调之前，使用相同的 [FlutterErrorDetails](https://www.yuque.com/thyname/flutter.foundation/fluttererrordetails) 对象调用，也可以配置它来控制错误的报告方式。
- <https://docs.flutter.dev/testing/errors>，关于错误处理的更多信息。

### message

```dart
String message
```

要显示的消息。

### createRenderObject()

```dart
RenderBox createRenderObject(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# WidgetBuilder

```dart
typedef WidgetBuilder = Widget Function(BuildContext context)
```

创建 Widget 的函数的签名，例如 [StatelessWidget.build] 或 [State.build]。

由 [Builder.builder]、[OverlayEntry.builder] 等使用。

另请参阅：

- [IndexedWidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/indexedwidgetbuilder)，与此类似，但还接受一个 index。
- [TransitionBuilder](https://www.yuque.com/thyname/flutter.widgets/transitionbuilder)，与此类似，但还接受一个 child。
- [ValueWidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/valuewidgetbuilder)，与此类似，但接受一个 value 和一个 child。

# IndexedWidgetBuilder

```dart
typedef IndexedWidgetBuilder = Widget Function(BuildContext context, int index)
```

为给定索引（例如列表中的索引）创建 Widget 的函数的签名。

由 [ListView.builder] 及其他使用惰性生成 Widget 的 API 使用。

另请参阅：

- [WidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/widgetbuilder)，与此类似，但只接受一个 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)。
- [TransitionBuilder](https://www.yuque.com/thyname/flutter.widgets/transitionbuilder)，与此类似，但还接受一个 child。
- [NullableIndexedWidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/nullableindexedwidgetbuilder)，与此类似，但可能返回 null。

# NullableIndexedWidgetBuilder

```dart
typedef NullableIndexedWidgetBuilder = Widget? Function(BuildContext context, int index)
```

为给定索引（例如列表中的索引）创建 Widget 的函数的签名，但可能返回 null。

由 [SliverChildBuilderDelegate.builder] 及其他使用惰性生成 Widget、且子节点数量事先未知的 API 使用。

与大多数构建器不同，此回调可以返回 null，表示该索引超出范围。这是否有效以及何时有效取决于该构建器的语义。例如，[SliverChildBuilderDelegate.builder] 在索引超出范围时返回 null，该范围由 [SliverChildBuilderDelegate.childCount] 定义；因此在这种情况下，`index` 参数的值可能决定返回 null 是否有效。

另请参阅：

- [WidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/widgetbuilder)，与此类似，但只接受一个 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)。
- [TransitionBuilder](https://www.yuque.com/thyname/flutter.widgets/transitionbuilder)，与此类似，但还接受一个 child。
- [IndexedWidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/indexedwidgetbuilder)，与此类似，但不可为 null。

# TransitionBuilder

```dart
typedef TransitionBuilder = Widget Function(BuildContext context, Widget? child)
```

一个根据给定的 child 构建 Widget 的构建器。

该 child 通常应作为返回的 Widget 树的一部分。

由 [AnimatedBuilder.builder]、[ListenableBuilder.builder]、[WidgetsApp.builder] 和 [MaterialApp.builder] 使用。

另请参阅：

- [WidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/widgetbuilder)，与此类似，但只接受一个 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)。
- [IndexedWidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/indexedwidgetbuilder)，与此类似，但还接受一个 index。
- [ValueWidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/valuewidgetbuilder)，与此类似，但接受一个 value 和一个 child。

# ComponentElement

```dart
abstract class ComponentElement extends Element {}
```

一种由其他 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 组合而成的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。

[ComponentElement](https://www.yuque.com/thyname/flutter.widgets/componentelement) 不直接创建 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)，而是通过创建其他 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 间接创建 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)。

与 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 相对。

### ComponentElement()

```dart
ComponentElement(Widget widget)
```

创建一个使用给定 Widget 作为其配置的 Element。

### debugDoingBuild

```dart
bool get debugDoingBuild
```

### renderObjectAttachingChild

```dart
Element? get renderObjectAttachingChild
```

### mount()

```dart
void mount(Element? parent, Object? newSlot)
```

### performRebuild()

```dart
void performRebuild()
```

调用（对于无状态 Widget）[StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget) 对象的 [StatelessWidget.build] 方法，或（对于有状态 Widget）[State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的 [State.build] 方法，然后更新 Widget 树。

在 [mount] 期间自动调用以生成首次构建，并在 Element 需要更新时由 [rebuild] 调用。

### build()

```dart
Widget build()
```

子类应重写此函数，以实际调用其 Widget 相应的 `build` 函数（例如 [StatelessWidget.build] 或 [State.build]）。

### visitChildren()

```dart
void visitChildren(ElementVisitor visitor)
```

### forgetChild()

```dart
void forgetChild(Element child)
```

# StatelessElement

```dart
class StatelessElement extends ComponentElement {}
```

一种使用 [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget) 作为其配置的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。

### StatelessElement()

```dart
StatelessElement(StatelessWidget widget)
```

创建一个使用给定 Widget 作为其配置的 Element。

### build()

```dart
Widget build()
```

### update()

```dart
void update(StatelessWidget newWidget)
```

# StatefulElement

```dart
class StatefulElement extends ComponentElement {}
```

一种使用 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 作为其配置的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。

### StatefulElement()

```dart
StatefulElement(StatefulWidget widget)
```

创建一个使用给定 Widget 作为其配置的 Element。

### build()

```dart
Widget build()
```

### state

```dart
State<StatefulWidget> get state
```

与树中此位置关联的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 实例。

[State](https://www.yuque.com/thyname/flutter.widgets/state) 对象与持有它们的 [StatefulElement](https://www.yuque.com/thyname/flutter.widgets/statefulelement) 对象之间是一对一的关系。[State](https://www.yuque.com/thyname/flutter.widgets/state) 对象由 [StatefulElement](https://www.yuque.com/thyname/flutter.widgets/statefulelement) 在 [mount] 中创建。

### reassemble()

```dart
void reassemble()
```

### performRebuild()

```dart
void performRebuild()
```

### update()

```dart
void update(StatefulWidget newWidget)
```

### activate()

```dart
void activate()
```

### deactivate()

```dart
void deactivate()
```

### unmount()

```dart
void unmount()
```

### dependOnInheritedElement()

```dart
InheritedWidget dependOnInheritedElement(Element ancestor, {Object? aspect})
```

### didChangeDependencies()

```dart
void didChangeDependencies()
```

### toDiagnosticsNode()

```dart
DiagnosticsNode toDiagnosticsNode({String? name, DiagnosticsTreeStyle? style})
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ProxyElement

```dart
abstract class ProxyElement extends ComponentElement {}
```

一种使用 [ProxyWidget](https://www.yuque.com/thyname/flutter.widgets/proxywidget) 作为其配置的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。

### ProxyElement()

```dart
ProxyElement(ProxyWidget widget)
```

为子类初始化字段。

### build()

```dart
Widget build()
```

### update()

```dart
void update(ProxyWidget newWidget)
```

### updated()

```dart
void updated(ProxyWidget oldWidget)
```

当 [widget] 发生变化时，在构建期间调用。

默认情况下调用 [notifyClients]。子类可以重写此方法，以避免在不必要时调用 [notifyClients]（例如，如果新旧 Widget 是等价的）。

### notifyClients()

```dart
void notifyClients(ProxyWidget oldWidget)
```

通知其他对象与此 Element 关联的 Widget 已发生变化。

在更改与此 Element 关联的 Widget 之后、但在重建此 Element 之前，于 [update]（通过 [updated]）期间调用。

# ParentDataElement

```dart
class ParentDataElement<T extends ParentData> extends ProxyElement {}
```

一种使用 [ParentDataWidget](https://www.yuque.com/thyname/flutter.widgets/parentdatawidget) 作为其配置的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。

### ParentDataElement()

```dart
ParentDataElement(ParentDataWidget<T> widget)
```

创建一个使用给定 Widget 作为其配置的 Element。

### debugParentDataType

```dart
Type get debugParentDataType
```

返回此 Element 已配置的 [ParentData](https://www.yuque.com/thyname/flutter.rendering/parentdata) 的 [Type](https://www.yuque.com/thyname/dart.core/type)。

这仅在调试模式下可用。在 profile 和 release 模式下会抛出异常。

### applyWidgetOutOfTurn()

```dart
void applyWidgetOutOfTurn(ParentDataWidget<T> newWidget)
```

在给定 Widget 上调用 [ParentDataWidget.applyParentData]，并向其传递此 Element 最终负责的 parent data 所属的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)。

这允许在不触发构建的情况下修改渲染对象的 [RenderObject.parentData]。这通常不建议这样做，但在以下情况下是合理的：

- 构建和布局当前正在进行中，但所讨论的 [ParentData](https://www.yuque.com/thyname/flutter.rendering/parentdata) 不影响布局，且要应用的值在构建和布局之前无法确定（例如，它依赖于某个后代节点的布局）。
- 绘制当前正在进行中，但所讨论的 [ParentData](https://www.yuque.com/thyname/flutter.rendering/parentdata) 不影响布局或绘制，且要应用的值在绘制之前无法确定（例如，它依赖于合成阶段）。

无论哪种情况，预计下一次构建都会导致此 Element 使用给定的新 Widget（或具有等价数据的 Widget）进行配置。

只有 [ParentDataWidget.debugCanApplyOutOfTurn] 返回 true 的 [ParentDataWidget](https://www.yuque.com/thyname/flutter.widgets/parentdatawidget) 才能以这种方式应用。

新 Widget 必须与当前 Widget 具有相同的 child。

使用此方法的一个例子是 [AutomaticKeepAlive](https://www.yuque.com/thyname/flutter.widgets/automatickeepalive) Widget。如果它在构建某个后代节点期间收到通知，说明其 child 必须保持存活，它将不按常规顺序应用一个 [KeepAlive](https://www.yuque.com/thyname/flutter.widgets/keepalive) Widget。这是安全的，因为根据定义，该 child 已经存活，因此这不会改变父节点在本帧的行为。这比仅仅为了更新 [KeepAlive](https://www.yuque.com/thyname/flutter.widgets/keepalive) Widget 而请求额外一帧更高效。

### notifyClients()

```dart
void notifyClients(ParentDataWidget<T> oldWidget)
```

# InheritedElement

```dart
class InheritedElement extends ProxyElement {}
```

一种使用 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 作为其配置的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。

### InheritedElement()

```dart
InheritedElement(InheritedWidget widget)
```

创建一个使用给定 Widget 作为其配置的 Element。

### debugDeactivated()

```dart
void debugDeactivated()
```

### getDependencies()

```dart
Object? getDependencies(Element dependent)
```

返回使用 [setDependencies] 为 [dependent] 记录的依赖值。

每个依赖的 Element 都会映射到一个单一的对象值，该值表示该 Element 如何依赖于此 [InheritedElement](https://www.yuque.com/thyname/flutter.widgets/inheritedelement)。此值默认为 null，默认情况下依赖的 Element 会无条件地重建。

子类可以使用 [updateDependencies] 管理这些值，以便在 [notifyDependent] 中有选择地重建依赖节点。

此方法通常仅在 [updateDependencies] 的重写方法中调用。

另请参阅：

- [updateDependencies]，每次通过 [dependOnInheritedWidgetOfExactType] 创建依赖时调用。
- [setDependencies]，为某个依赖的 Element 设置依赖值。
- [notifyDependent]，可以重写它，使用依赖节点的依赖值来决定该依赖节点是否需要重建。
- [InheritedModel](https://www.yuque.com/thyname/flutter.widgets/inheritedmodel)，一个使用此方法管理依赖值的类的示例。

### setDependencies()

```dart
void setDependencies(Element dependent, Object? value)
```

为 [dependent] 设置 [getDependencies] 返回的值。

每个依赖的 Element 都会映射到一个单一的对象值，该值表示该 Element 如何依赖于此 [InheritedElement](https://www.yuque.com/thyname/flutter.widgets/inheritedelement)。[updateDependencies] 方法默认将此值设置为 null，以使依赖的 Element 无条件地重建。

子类可以使用 [updateDependencies] 管理这些值，以便在 [notifyDependent] 中有选择地重建依赖节点。

此方法通常仅在 [updateDependencies] 的重写方法中调用。

另请参阅：

- [updateDependencies]，每次通过 [dependOnInheritedWidgetOfExactType] 创建依赖时调用。
- [getDependencies]，返回某个依赖的 Element 的当前值。
- [notifyDependent]，可以重写它，使用依赖节点的 [getDependencies] 值来决定该依赖节点是否需要重建。
- [InheritedModel](https://www.yuque.com/thyname/flutter.widgets/inheritedmodel)，一个使用此方法管理依赖值的类的示例。

### updateDependencies()

```dart
void updateDependencies(Element dependent, Object? aspect)
```

当添加一个新的 [dependent] 时，由 [dependOnInheritedWidgetOfExactType] 调用。

每个依赖的 Element 都可以通过 [setDependencies] 映射到一个单一的对象值。此方法可以使用 [getDependencies] 查找现有的依赖值。

默认情况下，此方法将 [dependent] 的继承依赖值设置为 null。这仅用于记录对 [dependent] 的无条件依赖。

子类可以管理自己的依赖值，以便在 [notifyDependent] 中有选择地重建依赖节点。

另请参阅：

- [getDependencies]，返回某个依赖的 Element 的当前值。
- [setDependencies]，为某个依赖的 Element 设置值。
- [notifyDependent]，可以重写它，使用依赖节点的依赖值来决定该依赖节点是否需要重建。
- [InheritedModel](https://www.yuque.com/thyname/flutter.widgets/inheritedmodel)，一个使用此方法管理依赖值的类的示例。

### notifyDependent()

```dart
void notifyDependent(InheritedWidget oldWidget, Element dependent)
```

由 [notifyClients] 针对每个依赖节点调用。

默认情况下调用 `dependent.didChangeDependencies()`。

子类可以重写此方法，根据 [getDependencies] 的值有选择地调用 [didChangeDependencies]。

另请参阅：

- [updateDependencies]，每次通过 [dependOnInheritedWidgetOfExactType] 创建依赖时调用。
- [getDependencies]，返回某个依赖的 Element 的当前值。
- [setDependencies]，为某个依赖的 Element 设置值。
- [InheritedModel](https://www.yuque.com/thyname/flutter.widgets/inheritedmodel)，一个使用此方法管理依赖值的类的示例。

### removeDependent()

```dart
void removeDependent(Element dependent)
```

由 [Element.deactivate] 调用，以从此 [InheritedElement](https://www.yuque.com/thyname/flutter.widgets/inheritedelement) 中移除给定的 `dependent` [Element](https://www.yuque.com/thyname/flutter.widgets/element)。

移除该依赖节点后，当此 [InheritedElement](https://www.yuque.com/thyname/flutter.widgets/inheritedelement) 通知其依赖节点时，将不再对其调用 [Element.didChangeDependencies]。

子类可以重写此方法，以释放为给定 [dependent] 保留的任何资源。

### updated()

```dart
void updated(InheritedWidget oldWidget)
```

如果 [InheritedWidget.updateShouldNotify] 返回 true，则调用所有依赖 Element 的 [Element.didChangeDependencies]。

由 [update] 在 [build] 之前立即调用。

调用 [notifyClients] 以实际触发通知。

### notifyClients()

```dart
void notifyClients(InheritedWidget oldWidget)
```

通过调用 [Element.didChangeDependencies]，通知所有依赖的 Element 此继承 Widget 已发生变化。

此方法只能在构建阶段调用。通常此方法会在继承 Widget 重建时自动调用，例如作为在该继承 Widget 之上调用 [State.setState] 的结果。

另请参阅：

- [InheritedNotifier](https://www.yuque.com/thyname/flutter.widgets/inheritednotifier)，[InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 的一个子类，当其 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable) 发送通知时也会调用此方法。

# RenderObjectElement

```dart
abstract class RenderObjectElement extends Element {}
```

一种使用 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 作为其配置的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。

[RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 对象在渲染树中拥有一个关联的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)，负责处理布局、绘制和命中测试等具体操作。

与 [ComponentElement](https://www.yuque.com/thyname/flutter.widgets/componentelement) 相对。

有关 Element 生命周期的详细信息，请参阅 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 处的讨论。

## 编写 RenderObjectElement 子类

大多数 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 使用三种常见的子节点模型：

- 叶子渲染对象，没有子节点：[LeafRenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/leafrenderobjectelement) 类处理这种情况。
- 单个子节点：[SingleChildRenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/singlechildrenderobjectelement) 类处理这种情况。
- 子节点链表：[MultiChildRenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/multichildrenderobjectelement) 类处理这种情况。

然而，有时渲染对象的子节点模型更为复杂。也许它拥有一个二维的子节点数组。也许它按需构造子节点。也许它包含多个列表。在这种情况下，配置该 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 所对应的 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 将是 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 的一个新子类。

这样的子类负责管理子节点，具体来说，是此对象的子 [Element](https://www.yuque.com/thyname/flutter.widgets/element)，以及其对应 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的子 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)。

### 特化获取器

[RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 对象大部分时间都充当其 [widget] 和 [renderObject] 之间的中介。通常建议不要特化 [widget] 获取器，而是在各个调用点进行类型转换，以避免在此特定实现之外增加开销。

```dart
class FooElement extends RenderObjectElement {
  FooElement(super.widget);

  // 特化 renderObject 获取器是可以的，
  // 因为它对性能不敏感。
  @override
  RenderFoo get renderObject => super.renderObject as RenderFoo;

  void _foo() {
    // 但对于 widget 获取器，我们更倾向于
    // 在本地进行类型转换，因为这样可以在
    // 不需要类型转换的地方获得更好的整体性能：
    final Foo foo = widget as Foo;
    // ...
  }

  // ...
}
```

### Slot

每个子 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 都对应一个 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)，该 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 应作为子节点附加到此 Element 的渲染对象上。

然而，Element 的直接子节点可能并不是最终产生它们所对应的实际 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的节点。例如，一个 [StatelessElement](https://www.yuque.com/thyname/flutter.widgets/statelesselement)（[StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget) 的 Element）对应的是其 child（即其 [StatelessWidget.build] 方法返回的 Element）所对应的任何 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)。

因此，每个子节点都会被分配一个 _[slot]_ 令牌。这是一个标识符，其含义仅对此 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 节点私有。当最终产生 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的后代节点准备好将其附加到此节点的渲染对象时，它会将该 slot 令牌传回此节点，从而使此节点能够廉价地识别出应将子渲染对象放在其父渲染对象中相对于其他子节点的什么位置。

子节点的 [slot] 是在父节点调用 [updateChild] 以扩展该子节点时确定的（参见下一节）。可以通过调用 [updateSlotForChild] 来更新它。

### 更新子节点

在 Element 生命周期的早期，框架会调用 [mount] 方法。此方法应针对每个子节点调用 [updateChild]，传入该子节点的 Widget 和 slot，从而获得一个子 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 列表。

随后，框架会调用 [update] 方法。在此方法中，[RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 应针对每个子节点调用 [updateChild]，传入在 [mount] 期间或上次运行 [update] 时（以最近发生的为准）获得的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)、新的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 和 slot。这会为该对象提供一个新的子 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 对象列表。

在可能的情况下，[update] 方法应尝试将上一轮的 Element 与新一轮的 Widget 进行映射。例如，如果上一轮的某个 Element 配置了特定的 [Key](https://www.yuque.com/thyname/flutter.foundation/key)，而新一轮的某个 Widget 具有相同的 key，那么它们应当配对，旧的 Element 应使用该 Widget（以及与新 Widget 新位置相对应的 slot）进行更新。[updateChildren] 方法在这方面可能会有帮助。

应按逻辑顺序对子节点调用 [updateChild]。顺序可能很重要；例如，如果两个子节点在其构建方法中都使用了 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage) 的 `writeState` 功能（且都没有 [Widget.key]），那么第一个子节点写入的状态将被第二个子节点覆盖。

#### 在构建阶段动态确定子节点

子 Widget 不一定非要原封不动地来自此 Element 的 Widget。它们可以通过回调动态生成，或以其他更具创造性的方式生成。

#### 在布局阶段动态确定子节点

如果要在布局阶段生成 Widget，那么在 [mount] 和 [update] 方法中生成它们是行不通的：此时此 Element 的渲染对象的布局尚未开始。相反，[update] 方法可以将渲染对象标记为需要布局（参见 [RenderObject.markNeedsLayout]），然后渲染对象的 [RenderObject.performLayout] 方法可以回调此 Element，让它生成 Widget 并相应地调用 [updateChild]。

要让渲染对象在布局期间调用某个 Element，它必须使用 [RenderObject.invokeLayoutCallback]。要让某个 Element 在其 [update] 方法之外调用 [updateChild]，它必须使用 [BuildOwner.buildScope]。

框架在正常操作中提供的检查，比在布局期间进行构建时提供的检查要多得多。因此，创建具有布局期构建语义的 Widget 时应格外小心。

#### 处理构建时的错误

如果某个 Element 调用一个构建器函数来获取其子节点的 Widget，它可能会发现该构建过程抛出了异常。此类异常应被捕获，并使用 [FlutterError.reportError] 报告。如果需要一个子节点，但构建器以这种方式失败了，可以改用 [ErrorWidget](https://www.yuque.com/thyname/flutter.widgets/errorwidget) 的实例。

### 分离子节点

在使用 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 时，某个子节点有可能在此 Element 更新之前，就被另一个 Element 主动移除。（具体来说，当具有特定 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 的 Widget 所根植的子树，正从此 Element 移动到构建阶段中较早处理的另一个 Element 时，就会发生这种情况。）发生这种情况时，此 Element 的 [forgetChild] 方法将被调用，并传入受影响的子 Element 的引用。

[RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 子类的 [forgetChild] 方法必须从其子节点列表中移除该子 Element，这样当它下一次 [update] 其子节点时，被移除的子节点就不会被考虑在内。

出于性能考虑，如果有很多 Element，通过将被遗忘的 Element 存储在一个 [Set](https://www.yuque.com/thyname/dart.core/set) 中来追踪它们，可能比主动改变子节点列表和所有 slot 身份的本地记录更快。例如，参见 [MultiChildRenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/multichildrenderobjectelement) 的实现。

### 维护渲染对象树

一旦某个后代节点生成了一个渲染对象，它就会调用 [insertRenderObjectChild]。如果该后代节点的 slot 身份发生变化，它会调用 [moveRenderObjectChild]。如果某个后代节点消失了，它会调用 [removeRenderObjectChild]。

这三个方法应相应地更新渲染树，分别将给定的子渲染对象附加到、移动到、或从此 Element 自身的渲染对象中分离。

### 遍历子节点

如果一个 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 对象拥有任何子 [Element](https://www.yuque.com/thyname/flutter.widgets/element)，它必须在其 [visitChildren] 方法的实现中公开它们。此方法被框架的许多内部机制使用，因此应当保持高效。测试框架和 [debugDumpApp](https://www.yuque.com/thyname/flutter.widgets/debugdumpapp) 也会使用它。

### RenderObjectElement()

```dart
RenderObjectElement(RenderObjectWidget widget)
```

创建一个使用给定 Widget 作为其配置的 Element。

### renderObject

```dart
RenderObject get renderObject
```

此 Element 底层的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)。

如果此 Element 已被 [unmount]，此获取器将抛出异常。

### renderObjectAttachingChild

```dart
Element? get renderObjectAttachingChild
```

### debugDoingBuild

```dart
bool get debugDoingBuild
```

### mount()

```dart
void mount(Element? parent, Object? newSlot)
```

### update()

```dart
void update(RenderObjectWidget newWidget)
```

### performRebuild()

```dart
void performRebuild()
```

### deactivate()

```dart
void deactivate()
```

### unmount()

```dart
void unmount()
```

### updateSlot()

```dart
void updateSlot(Object? newSlot)
```

### attachRenderObject()

```dart
void attachRenderObject(Object? newSlot)
```

### detachRenderObject()

```dart
void detachRenderObject()
```

### insertRenderObjectChild()

```dart
void insertRenderObjectChild(RenderObject child, Object? slot)
```

将给定的子节点插入到给定 slot 处的 [renderObject] 中。

{@template flutter.widgets.RenderObjectElement.insertRenderObjectChild} `slot` 的语义由此 Element 决定。例如，如果此 Element 只有一个子节点，则 slot 应始终为 null。如果此 Element 拥有一个子节点列表，那么包装在 [IndexedSlot](https://www.yuque.com/thyname/flutter.widgets/indexedslot) 中的前一个兄弟 Element 是一个方便的 slot 值。{@endtemplate}

### moveRenderObjectChild()

```dart
void moveRenderObjectChild(RenderObject child, Object? oldSlot, Object? newSlot)
```

将给定的子节点从给定的旧 slot 移动到给定的新 slot。

保证给定的子节点以 [renderObject] 作为其父节点。

{@macro flutter.widgets.RenderObjectElement.insertRenderObjectChild}

只有在 [updateChild] 最终可能使用一个现有的 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 子节点和一个与该 Element 先前被赋予的 slot 不同的 `slot` 被调用时，才会调用此方法。例如，[MultiChildRenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/multichildrenderobjectelement) 就是这样做的。[SingleChildRenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/singlechildrenderobjectelement) 不会这样做（因为 `slot` 始终为 null）。一个拥有一组特定 slot、且每个子节点始终拥有相同 slot（并且不同 slot 中的子节点永远不会为了更新某个 slot 而与另一个 slot 中的 Element 进行比较）的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)，永远不会调用此方法。

### removeRenderObjectChild()

```dart
void removeRenderObjectChild(RenderObject child, Object? slot)
```

从 [renderObject] 中移除给定的子节点。

保证给定的子节点已插入到给定的 `slot` 处，且以 [renderObject] 作为其父节点。

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RootRenderObjectElement

```dart
abstract class RootRenderObjectElement extends RenderObjectElement with RootElementMixin {}
```

已弃用。框架中未使用，将在未来版本的 Flutter 中移除。

继承此类的类可以改为继承 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 并混入 [RootElementMixin](https://www.yuque.com/thyname/flutter.widgets/rootelementmixin)。

### RootRenderObjectElement()

```dart
RootRenderObjectElement(RenderObjectWidget widget)
```

为子类初始化字段。

# RootElementMixin

```dart
mixin RootElementMixin on Element {}
```

用于树根处 Element 的 mixin。

只有根 Element 才可以显式设置其 owner。所有其他 Element 都从其父节点继承其 owner。

### assignOwner()

```dart
void assignOwner(BuildOwner owner)
```

设置该 Element 的 owner。该 owner 将被传播给此 Element 的所有后代节点。

owner 管理脏 Element 列表。

[WidgetsBinding](https://www.yuque.com/thyname/flutter.widgets/widgetsbinding) 引入了主要的 owner，即 [WidgetsBinding.buildOwner]，并在调用 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 时将其赋给 Widget 树。该 binding 负责通过调用 build owner 的 [BuildOwner.buildScope] 方法来驱动构建管线。参见 [WidgetsBinding.drawFrame]。

### mount()

```dart
void mount(Element? parent, Object? newSlot)
```

# LeafRenderObjectElement

```dart
class LeafRenderObjectElement extends RenderObjectElement {}
```

一种使用 [LeafRenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/leafrenderobjectwidget) 作为其配置的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。

### LeafRenderObjectElement()

```dart
LeafRenderObjectElement(LeafRenderObjectWidget widget)
```

创建一个使用给定 Widget 作为其配置的 Element。

### forgetChild()

```dart
void forgetChild(Element child)
```

### insertRenderObjectChild()

```dart
void insertRenderObjectChild(RenderObject child, Object? slot)
```

### moveRenderObjectChild()

```dart
void moveRenderObjectChild(RenderObject child, Object? oldSlot, Object? newSlot)
```

### removeRenderObjectChild()

```dart
void removeRenderObjectChild(RenderObject child, Object? slot)
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

# SingleChildRenderObjectElement

```dart
class SingleChildRenderObjectElement extends RenderObjectElement {}
```

一种使用 [SingleChildRenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/singlechildrenderobjectwidget) 作为其配置的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。

其 child 是可选的。

此 Element 子类可用于其 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 使用 [RenderObjectWithChildMixin](https://www.yuque.com/thyname/flutter.rendering/renderobjectwithchildmixin) mixin 的 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget)。这类 Widget 应继承自 [SingleChildRenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/singlechildrenderobjectwidget)。

### SingleChildRenderObjectElement()

```dart
SingleChildRenderObjectElement(SingleChildRenderObjectWidget widget)
```

创建一个使用给定 Widget 作为其配置的 Element。

### visitChildren()

```dart
void visitChildren(ElementVisitor visitor)
```

### forgetChild()

```dart
void forgetChild(Element child)
```

### mount()

```dart
void mount(Element? parent, Object? newSlot)
```

### update()

```dart
void update(SingleChildRenderObjectWidget newWidget)
```

### insertRenderObjectChild()

```dart
void insertRenderObjectChild(RenderObject child, Object? slot)
```

### moveRenderObjectChild()

```dart
void moveRenderObjectChild(RenderObject child, Object? oldSlot, Object? newSlot)
```

### removeRenderObjectChild()

```dart
void removeRenderObjectChild(RenderObject child, Object? slot)
```

# MultiChildRenderObjectElement

```dart
class MultiChildRenderObjectElement extends RenderObjectElement {}
```

一种使用 [MultiChildRenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/multichildrenderobjectwidget) 作为其配置的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。

此 Element 子类可用于其 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 使用 [ContainerRenderObjectMixin](https://www.yuque.com/thyname/flutter.rendering/containerrenderobjectmixin) mixin、且 parent data 类型实现了 [ContainerParentDataMixin<RenderObject>] 的 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget)。这类 Widget 应继承自 [MultiChildRenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/multichildrenderobjectwidget)。

另请参阅：

- [IndexedSlot](https://www.yuque.com/thyname/flutter.widgets/indexedslot)，用作 [MultiChildRenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/multichildrenderobjectelement) 子节点的 [Element.slot]。
- [RenderObjectElement.updateChildren]，其中讨论了为何将 [IndexedSlot](https://www.yuque.com/thyname/flutter.widgets/indexedslot) 用作 [MultiChildRenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/multichildrenderobjectelement) 子节点的 slot。

### MultiChildRenderObjectElement()

```dart
MultiChildRenderObjectElement(MultiChildRenderObjectWidget widget)
```

创建一个使用给定 Widget 作为其配置的 Element。

### renderObject

```dart
ContainerRenderObjectMixin<RenderObject, ContainerParentDataMixin<RenderObject>> get renderObject
```

### children

```dart
Iterable<Element> get children
```

此 Element 当前的子节点列表。

此列表经过过滤，隐藏了已被遗忘的 Element（使用 [forgetChild]）。

### insertRenderObjectChild()

```dart
void insertRenderObjectChild(RenderObject child, IndexedSlot<Element?> slot)
```

### moveRenderObjectChild()

```dart
void moveRenderObjectChild(RenderObject child, IndexedSlot<Element?> oldSlot, IndexedSlot<Element?> newSlot)
```

### removeRenderObjectChild()

```dart
void removeRenderObjectChild(RenderObject child, Object? slot)
```

### visitChildren()

```dart
void visitChildren(ElementVisitor visitor)
```

### forgetChild()

```dart
void forgetChild(Element child)
```

### inflateWidget()

```dart
Element inflateWidget(Widget newWidget, Object? newSlot)
```

### mount()

```dart
void mount(Element? parent, Object? newSlot)
```

### update()

```dart
void update(MultiChildRenderObjectWidget newWidget)
```

# RenderTreeRootElement

```dart
abstract class RenderTreeRootElement extends RenderObjectElement {}
```

用于管理渲染树根节点的 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement)。

与其他任何渲染对象 Element 不同，此 Element 不会尝试将其 [renderObject] 附加到最近的祖先 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement)。相反，子类必须重写 [attachRenderObject] 和 [detachRenderObject]，以将 [renderObject] 附加到/分离自管理该渲染树的任何实例（例如，通过将其赋值给 [PipelineOwner.rootNode]）。

### RenderTreeRootElement()

```dart
RenderTreeRootElement(RenderObjectWidget widget)
```

创建一个使用给定 Widget 作为其配置的 Element。

### attachRenderObject()

```dart
void attachRenderObject(Object? newSlot)
```

### detachRenderObject()

```dart
void detachRenderObject()
```

### updateSlot()

```dart
void updateSlot(Object? newSlot)
```

# DebugCreator

```dart
class DebugCreator {}
```

作为某个 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的创建者的 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 的封装类。

将一个 [DebugCreator](https://www.yuque.com/thyname/flutter.widgets/debugcreator) 设置为 [RenderObject.debugCreator] 将带来更好的错误消息。

### DebugCreator()

```dart
DebugCreator(Element element)
```

使用输入的 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 创建一个 [DebugCreator](https://www.yuque.com/thyname/flutter.widgets/debugcreator) 实例。

### element

```dart
Element element
```

该 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的创建者。

### toString()

```dart
String toString()
```

# IndexedSlot

```dart
class IndexedSlot<T extends Element?> {}
```

用于 [MultiChildRenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/multichildrenderobjectelement) 子节点的 [Element.slot] 的一个值。

[MultiChildRenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/multichildrenderobjectelement) 的一个 slot 由一个 [index] 和一个任意的 [value] 组成，[index] 标识占用此 slot 的子节点在 [MultiChildRenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/multichildrenderobjectelement) 子节点列表中的位置，[value] 可以进一步定义占用此 slot 的子节点在其父节点子节点列表中的位置。

另请参阅：

- [RenderObjectElement.updateChildren]，其中讨论了为何将此类用作 [MultiChildRenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/multichildrenderobjectelement) 子节点的 slot 值。

### IndexedSlot()

```dart
IndexedSlot(int index, T value)
```

使用提供的 [index] 和 slot [value] 创建一个 [IndexedSlot](https://www.yuque.com/thyname/flutter.widgets/indexedslot)。

### value

```dart
T value
```

用于定义占用此 slot 的子节点在其父节点子节点列表中位置的信息。

### index

```dart
int index
```

此 slot 在父节点子节点列表中的索引。
