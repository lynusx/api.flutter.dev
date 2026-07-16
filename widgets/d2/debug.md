@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/rendering.dart'; @docImport 'package:flutter/scheduler.dart';

@docImport 'binding.dart'; @docImport 'widget_inspector.dart';

# debugPrintRebuildDirtyWidgets

```dart
bool debugPrintRebuildDirtyWidgets
```

记录每一帧中被构建的脏组件（dirty widgets）。

结合 [debugPrintBuildScope](https://www.yuque.com/thyname/flutter.widgets/debugprintbuildscope) 或 [debugPrintBeginFrameBanner](https://www.yuque.com/thyname/flutter.scheduler/debugprintbeginframebanner)，可以区分由部件树的初始挂载（例如在调用 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 时）触发的构建，与由管线（pipeline）触发的常规构建。

结合 [debugPrintScheduleBuildForStacks](https://www.yuque.com/thyname/flutter.widgets/debugprintschedulebuildforstacks)，可以观察某个部件的脏/干净（dirty/clean）生命周期。

若需获取类似信息，但希望在 Flutter DevTools 的时间线（timeline）中查看，而不是在控制台中查看（控制台中的信息可能过多），可以考虑使用 [debugProfileBuildsEnabled](https://www.yuque.com/thyname/flutter.widgets/debugprofilebuildsenabled)。

另请参阅：

- [WidgetsBinding.drawFrame]，用于驱动构建和渲染管线以生成一帧。

# RebuildDirtyWidgetCallback

```dart
typedef RebuildDirtyWidgetCallback = void Function(Element e, bool builtOnce)
```

[debugOnRebuildDirtyWidget](https://www.yuque.com/thyname/flutter.widgets/debugonrebuilddirtywidget) 实现的签名。

# debugOnRebuildDirtyWidget

```dart
RebuildDirtyWidgetCallback? debugOnRebuildDirtyWidget
```

每帧中每个被构建的脏组件都会调用此回调。

此回调仅在调试构建（debug build）中被调用。

另请参阅：

- [debugPrintRebuildDirtyWidgets](https://www.yuque.com/thyname/flutter.widgets/debugprintrebuilddirtywidgets)，功能类似，但是将信息记录到控制台而不是调用回调。
- [debugOnProfilePaint](https://www.yuque.com/thyname/flutter.rendering/debugonprofilepaint)，对 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的绘制执行类似的操作。
- [WidgetInspectorService](https://www.yuque.com/thyname/flutter.widgets/widgetinspectorservice)，当启用 `ext.flutter.inspector.trackRebuildDirtyWidgets` 服务扩展时，使用 [debugOnRebuildDirtyWidget](https://www.yuque.com/thyname/flutter.widgets/debugonrebuilddirtywidget) 回调生成聚合的性能统计信息，描述发生重建的时间及部件。

# debugPrintBuildScope

```dart
bool debugPrintBuildScope
```

记录对 [BuildOwner.buildScope] 的所有调用。

结合 [debugPrintScheduleBuildForStacks](https://www.yuque.com/thyname/flutter.widgets/debugprintschedulebuildforstacks)，可以追踪 [State.setState] 调用何时被处理。

结合 [debugPrintRebuildDirtyWidgets](https://www.yuque.com/thyname/flutter.widgets/debugprintrebuilddirtywidgets) 或 [debugPrintBeginFrameBanner](https://www.yuque.com/thyname/flutter.scheduler/debugprintbeginframebanner)，可以区分由部件树的初始挂载（例如在调用 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 时）触发的构建，与由管线触发的常规构建。

另请参阅：

- [WidgetsBinding.drawFrame]，用于驱动构建和渲染管线以生成一帧。

# debugPrintScheduleBuildForStacks

```dart
bool debugPrintScheduleBuildForStacks
```

记录将部件标记为需要重建的调用堆栈。

每当 [BuildOwner.scheduleBuildFor] 将一个元素（element）添加到脏列表（dirty list）中时，都会调用此方法。通常这是调用 [Element.markNeedsBuild] 的结果，而后者通常又是调用 [State.setState] 的结果。

若需查看部件何时被重建，请参阅 [debugPrintRebuildDirtyWidgets](https://www.yuque.com/thyname/flutter.widgets/debugprintrebuilddirtywidgets)。

若需查看脏列表何时被刷新，请参阅 [debugPrintBuildScope](https://www.yuque.com/thyname/flutter.widgets/debugprintbuildscope)。

若需查看帧何时被调度，请参阅 [debugPrintScheduleFrameStacks](https://www.yuque.com/thyname/flutter.scheduler/debugprintscheduleframestacks)。

# debugPrintGlobalKeyedWidgetLifecycle

```dart
bool debugPrintGlobalKeyedWidgetLifecycle
```

记录带有全局键（global key）的部件何时被停用（deactivated），以及何时被重新激活（重新获取，retaken）。

这有助于追查与 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 逻辑相关的框架 bug。

# debugProfileBuildsEnabled

```dart
bool debugProfileBuildsEnabled
```

为每个被构建的 Widget 添加 [Timeline](https://www.yuque.com/thyname/dart.developer/timeline) 事件。

此标志所公开的计时信息并不能代表构建的实际开销，因为相对于每个对象的构建时间而言，添加时间线事件的开销是很大的。不过，它可以在时间线中揭示意外的部件行为。

在调试构建中，跟踪中会包含额外的信息（例如正在构建的部件的属性）。收集这些数据的开销很大，这进一步导致这些跟踪无法代表实际性能。此数据在 profile 构建中会被省略。

有关 Flutter 性能调试的更多信息，请参阅 <https://docs.flutter.dev/perf/ui-performance>。

另请参阅：

- [debugPrintRebuildDirtyWidgets](https://www.yuque.com/thyname/flutter.widgets/debugprintrebuilddirtywidgets)，功能类似，但是将信息报告到控制台。
- [debugProfileLayoutsEnabled](https://www.yuque.com/thyname/flutter.rendering/debugprofilelayoutsenabled)，对布局（layout）执行类似的操作，其控制台版本为 [debugPrintLayouts](https://www.yuque.com/thyname/flutter.rendering/debugprintlayouts)。
- [debugProfilePaintsEnabled](https://www.yuque.com/thyname/flutter.rendering/debugprofilepaintsenabled)，对绘制（painting）执行类似的操作。
- [debugProfileBuildsEnabledUserWidgets](https://www.yuque.com/thyname/flutter.widgets/debugprofilebuildsenableduserwidgets)，为用户创建的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 构建时间添加事件，开销更低。
- [debugEnhanceBuildTimelineArguments](https://www.yuque.com/thyname/flutter.widgets/debugenhancebuildtimelinearguments)，使用与 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 构建相关的调试信息增强跟踪。

# debugProfileBuildsEnabledUserWidgets

```dart
bool debugProfileBuildsEnabledUserWidgets
```

为每个用户创建的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 构建添加 [Timeline](https://www.yuque.com/thyname/dart.developer/timeline) 事件。

用户创建的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 是指在根库（root library）中构造的任意 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget)。[Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 通常包含在库中构造的子 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget)（例如，[TextButton](https://www.yuque.com/thyname/flutter.material/textbutton) 拥有一个 [RichText](https://www.yuque.com/thyname/flutter.widgets/richtext) 子部件）。启用此标志后，这些子部件的时间线事件将被省略。这不仅适用于根库中声明的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget)，也适用于任何 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget)。

另请参阅：

- [debugProfileBuildsEnabled](https://www.yuque.com/thyname/flutter.widgets/debugprofilebuildsenabled)，功能类似，但为每个部件都显示事件，开销更高。
- [debugEnhanceBuildTimelineArguments](https://www.yuque.com/thyname/flutter.widgets/debugenhancebuildtimelinearguments)，使用与 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 构建相关的调试信息增强跟踪。

# debugEnhanceBuildTimelineArguments

```dart
bool debugEnhanceBuildTimelineArguments
```

为与 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 构建相关的 [Timeline](https://www.yuque.com/thyname/dart.developer/timeline) 事件添加调试信息。

此标志仅会为调试构建添加 [Timeline](https://www.yuque.com/thyname/dart.developer/timeline) 事件参数。额外的参数将被添加到 "BUILD" [Timeline](https://www.yuque.com/thyname/dart.developer/timeline) 事件，以及所有 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 构建 [Timeline](https://www.yuque.com/thyname/dart.developer/timeline) 事件中，即在 [debugProfileBuildsEnabled](https://www.yuque.com/thyname/flutter.widgets/debugprofilebuildsenabled) 和 [debugProfileBuildsEnabledUserWidgets](https://www.yuque.com/thyname/flutter.widgets/debugprofilebuildsenableduserwidgets) 任一为 true 时添加的那些 [Timeline](https://www.yuque.com/thyname/dart.developer/timeline) 事件。所添加的调试信息包括与 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 脏状态相关的统计数据，以及 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 的诊断信息（即 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 的属性）。

另请参阅：

- [debugProfileBuildsEnabled](https://www.yuque.com/thyname/flutter.widgets/debugprofilebuildsenabled)，为每个被构建的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 添加 [Timeline](https://www.yuque.com/thyname/dart.developer/timeline) 事件。
- [debugProfileBuildsEnabledUserWidgets](https://www.yuque.com/thyname/flutter.widgets/debugprofilebuildsenableduserwidgets)，为每个用户创建的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 添加 [Timeline](https://www.yuque.com/thyname/dart.developer/timeline) 事件。
- [debugEnhanceLayoutTimelineArguments](https://www.yuque.com/thyname/flutter.rendering/debugenhancelayouttimelinearguments)，对与 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 布局相关的事件执行类似的操作。
- [debugEnhancePaintTimelineArguments](https://www.yuque.com/thyname/flutter.rendering/debugenhancepainttimelinearguments)，对与 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 绘制相关的事件执行类似的操作。

# debugHighlightDeprecatedWidgets

```dart
bool debugHighlightDeprecatedWidgets
```

为已弃用的部件显示提示横幅（banner）。

# debugChildrenHaveDuplicateKeys()

```dart
bool debugChildrenHaveDuplicateKeys(Widget parent, Iterable<Widget> children, {String? message})
```

如果给定的子部件列表包含任何重复的非空键，则触发断言。

要调用此函数，请使用以下模式：

```dart
class MyWidget extends StatelessWidget {
  MyWidget({ super.key, required this.children }) {
    assert(!debugChildrenHaveDuplicateKeys(this, children));
  }

  final List<Widget> children;

  // ...
}
```

如果指定了 `message`，它将覆盖默认消息。

对于列表项没有特定父级的场景，可使用此函数的另一版本，请参阅 [debugItemsHaveDuplicateKeys](https://www.yuque.com/thyname/flutter.widgets/debugitemshaveduplicatekeys)。

如果断言被禁用，则不执行任何操作，始终返回 false。

# debugItemsHaveDuplicateKeys()

```dart
bool debugItemsHaveDuplicateKeys(Iterable<Widget> items)
```

如果给定的项目列表包含任何重复的非空键，则触发断言。

要调用此函数，请使用以下模式：

```dart
assert(!debugItemsHaveDuplicateKeys(items));
```

对于专门供父级检查其子部件列表使用的版本，请参阅 [debugChildrenHaveDuplicateKeys](https://www.yuque.com/thyname/flutter.widgets/debugchildrenhaveduplicatekeys)。

如果断言被禁用，则不执行任何操作，始终返回 false。

# debugCheckHasTable()

```dart
bool debugCheckHasTable(BuildContext context)
```

断言给定的上下文（context）拥有 [Table](https://www.yuque.com/thyname/flutter.widgets/table) 祖先。

由 [TableRowInkWell](https://www.yuque.com/thyname/flutter.material/tablerowinkwell) 使用，以确保其仅在合适的上下文中使用。

要调用此函数，请使用以下模式，通常在相应 Widget 的 build 方法中：

```dart
assert(debugCheckHasTable(context));
```

始终将此断言放在任何提前返回（early return）之前，以确保在所有情况下都能检查该不变量。这可以防止 bug 在某个特定代码路径被触发之前一直被隐藏。

此方法可能开销较大（它会遍历元素树）。

如果断言被禁用，则不执行任何操作，始终返回 true。

# debugCheckHasMediaQuery()

```dart
bool debugCheckHasMediaQuery(BuildContext context)
```

断言给定的上下文拥有 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先。

由多种部件使用，以确保它们仅在合适的上下文中使用。

要调用此函数，请使用以下模式，通常在相应 Widget 的 build 方法中：

```dart
assert(debugCheckHasMediaQuery(context));
```

始终将此断言放在任何提前返回之前，以确保在所有情况下都能检查该不变量。这可以防止 bug 在某个特定代码路径被触发之前一直被隐藏。

如果断言被禁用，则不执行任何操作，始终返回 true。

# debugCheckHasDirectionality()

```dart
bool debugCheckHasDirectionality(BuildContext context, {String? why, String? hint, String? alternative})
```

断言给定的上下文拥有 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 祖先。

由多种部件使用，以确保它们仅在合适的上下文中使用。

要调用此函数，请使用以下模式，通常在相应 Widget 的 build 方法中：

```dart
assert(debugCheckHasDirectionality(context));
```

为改善错误信息，你可以通过以下命名参数添加一些额外说明。

- why：说明为何需要该方向，例如 "to resolve the 'alignment' argument"。应为一个说明原因的副词短语。
- hint：说明可能发生此情况的原因，例如 "The default value of the 'alignment' argument of the $runtimeType widget is an AlignmentDirectional value."。应为一个标点完整的句子。
- alternative：针对具体情况提供额外建议，尤其是提供 Directionality 祖先之外的替代方案，例如 "Alternatively, consider specifying the 'textDirection' argument."。应为一个标点完整的句子。

每个参数都可以为 null，此时会被跳过（这是默认行为）。如果它们非空，则会按照上述顺序被包含在内，并穿插在关于 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 的更通用建议之间。

始终将此断言放在任何提前返回之前，以确保在所有情况下都能检查该不变量。这可以防止 bug 在某个特定代码路径被触发之前一直被隐藏。

如果断言被禁用，则不执行任何操作，始终返回 true。

另请参阅：

- [debugCheckHasDirectionality](https://www.yuque.com/thyname/flutter.widgets/debugcheckhasdirectionality)，一个类似但更通用的绘制库（painting-library）级别的函数。

# debugWidgetBuilderValue()

```dart
void debugWidgetBuilderValue(Widget widget, Widget? built)
```

断言 `built` 部件不为空。

当给定的 `widget` 调用某个构建器（builder）函数时使用，用于检查该函数是否按通常要求返回了非空值。

如果断言被禁用，则不执行任何操作。

# debugCheckHasWidgetsLocalizations()

```dart
bool debugCheckHasWidgetsLocalizations(BuildContext context)
```

断言给定的上下文拥有一个包含 [WidgetsLocalizations](https://www.yuque.com/thyname/flutter.widgets/widgetslocalizations) 委托（delegate）的 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) 祖先。

要调用此函数，请使用以下模式，通常在相应 Widget 的 build 方法中：

```dart
assert(debugCheckHasWidgetsLocalizations(context));
```

始终将此断言放在任何提前返回之前，以确保在所有情况下都能检查该不变量。这可以防止 bug 在某个特定代码路径被触发之前一直被隐藏。

如果断言被禁用，则不执行任何操作，始终返回 true。

# debugCheckHasOverlay()

```dart
bool debugCheckHasOverlay(BuildContext context)
```

断言给定的上下文拥有 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 祖先。

要调用此函数，请使用以下模式，通常在相应 Widget 的 build 方法中：

```dart
assert(debugCheckHasOverlay(context));
```

始终将此断言放在任何提前返回之前，以确保在所有情况下都能检查该不变量。这可以防止 bug 在某个特定代码路径被触发之前一直被隐藏。

此方法可能开销较大（它会遍历元素树）。

如果断言被禁用，则不执行任何操作，始终返回 true。

# debugAssertAllWidgetVarsUnset()

```dart
bool debugAssertAllWidgetVarsUnset(String reason)
```

如果没有任何一个 widgets 库的调试变量被更改过，则返回 true。

测试框架使用此函数，以确保调试变量没有被意外更改。

有关完整列表，请参阅 [widgets 库](widgets/widgets-library.html)。
