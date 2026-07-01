@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/rendering.dart'; @docImport 'package:flutter/scheduler.dart';

@docImport 'binding.dart'; @docImport 'widget_inspector.dart';

# debugPrintRebuildDirtyWidgets

```dart
bool debugPrintRebuildDirtyWidgets
```

Log the dirty widgets that are built each frame.

Combined with [debugPrintBuildScope] or [debugPrintBeginFrameBanner], this allows you to distinguish builds triggered by the initial mounting of a widget tree (e.g. in a call to [runApp]) from the regular builds triggered by the pipeline.

Combined with [debugPrintScheduleBuildForStacks], this lets you watch a widget's dirty/clean lifecycle.

To get similar information but showing it on the timeline available from Flutter DevTools rather than getting it in the console (where it can be overwhelming), consider [debugProfileBuildsEnabled].

See also:

- [WidgetsBinding.drawFrame], which pumps the build and rendering pipeline to generate a frame.

# RebuildDirtyWidgetCallback

```dart
typedef RebuildDirtyWidgetCallback = void Function(Element e, bool builtOnce)
```

Signature for [debugOnRebuildDirtyWidget] implementations.

# debugOnRebuildDirtyWidget

```dart
RebuildDirtyWidgetCallback? debugOnRebuildDirtyWidget
```

Callback invoked for every dirty widget built each frame.

This callback is only invoked in debug builds.

See also:

- [debugPrintRebuildDirtyWidgets], which does something similar but logs to the console instead of invoking a callback.
- [debugOnProfilePaint], which does something similar for [RenderObject] painting.
- [WidgetInspectorService], which uses the [debugOnRebuildDirtyWidget] callback to generate aggregate profile statistics describing which widget rebuilds occurred when the `ext.flutter.inspector.trackRebuildDirtyWidgets` service extension is enabled.

# debugPrintBuildScope

```dart
bool debugPrintBuildScope
```

Log all calls to [BuildOwner.buildScope].

Combined with [debugPrintScheduleBuildForStacks], this allows you to track when a [State.setState] call gets serviced.

Combined with [debugPrintRebuildDirtyWidgets] or [debugPrintBeginFrameBanner], this allows you to distinguish builds triggered by the initial mounting of a widget tree (e.g. in a call to [runApp]) from the regular builds triggered by the pipeline.

See also:

- [WidgetsBinding.drawFrame], which pumps the build and rendering pipeline to generate a frame.

# debugPrintScheduleBuildForStacks

```dart
bool debugPrintScheduleBuildForStacks
```

Log the call stacks that mark widgets as needing to be rebuilt.

This is called whenever [BuildOwner.scheduleBuildFor] adds an element to the dirty list. Typically this is as a result of [Element.markNeedsBuild] being called, which itself is usually a result of [State.setState] being called.

To see when a widget is rebuilt, see [debugPrintRebuildDirtyWidgets].

To see when the dirty list is flushed, see [debugPrintBuildScope].

To see when a frame is scheduled, see [debugPrintScheduleFrameStacks].

# debugPrintGlobalKeyedWidgetLifecycle

```dart
bool debugPrintGlobalKeyedWidgetLifecycle
```

Log when widgets with global keys are deactivated and log when they are reactivated (retaken).

This can help track down framework bugs relating to the [GlobalKey] logic.

# debugProfileBuildsEnabled

```dart
bool debugProfileBuildsEnabled
```

Adds [Timeline] events for every Widget built.

The timing information this flag exposes is not representative of the actual cost of building, because the overhead of adding timeline events is significant relative to the time each object takes to build. However, it can expose unexpected widget behavior in the timeline.

In debug builds, additional information is included in the trace (such as the properties of widgets being built). Collecting this data is expensive and further makes these traces non-representative of actual performance. This data is omitted in profile builds.

For more information about performance debugging in Flutter, see <https://docs.flutter.dev/perf/ui-performance>.

See also:

- [debugPrintRebuildDirtyWidgets], which does something similar but reporting the builds to the console.
- [debugProfileLayoutsEnabled], which does something similar for layout, and [debugPrintLayouts], its console equivalent.
- [debugProfilePaintsEnabled], which does something similar for painting.
- [debugProfileBuildsEnabledUserWidgets], which adds events for user-created [Widget] build times and incurs less overhead.
- [debugEnhanceBuildTimelineArguments], which enhances the trace with debugging information related to [Widget] builds.

# debugProfileBuildsEnabledUserWidgets

```dart
bool debugProfileBuildsEnabledUserWidgets
```

Adds [Timeline] events for every user-created [Widget] built.

A user-created [Widget] is any [Widget] that is constructed in the root library. Often [Widget]s contain child [Widget]s that are constructed in libraries (for example, a [TextButton] having a [RichText] child). Timeline events for those children will be omitted with this flag. This works for any [Widget] not just ones declared in the root library.

See also:

- [debugProfileBuildsEnabled], which functions similarly but shows events for every widget and has a higher overhead cost.
- [debugEnhanceBuildTimelineArguments], which enhances the trace with debugging information related to [Widget] builds.

# debugEnhanceBuildTimelineArguments

```dart
bool debugEnhanceBuildTimelineArguments
```

Adds debugging information to [Timeline] events related to [Widget] builds.

This flag will only add [Timeline] event arguments for debug builds. Additional arguments will be added for the "BUILD" [Timeline] event and for all [Widget] build [Timeline] events, which are the [Timeline] events that are added when either of [debugProfileBuildsEnabled] and [debugProfileBuildsEnabledUserWidgets] are true. The debugging information that will be added in trace arguments includes stats around [Widget] dirty states and [Widget] diagnostic information (i.e. [Widget] properties).

See also:

- [debugProfileBuildsEnabled], which adds [Timeline] events for every [Widget] built.
- [debugProfileBuildsEnabledUserWidgets], which adds [Timeline] events for every user-created [Widget] built.
- [debugEnhanceLayoutTimelineArguments], which does something similar for events related to [RenderObject] layouts.
- [debugEnhancePaintTimelineArguments], which does something similar for events related to [RenderObject] paints.

# debugHighlightDeprecatedWidgets

```dart
bool debugHighlightDeprecatedWidgets
```

Show banners for deprecated widgets.

# debugChildrenHaveDuplicateKeys()

```dart
bool debugChildrenHaveDuplicateKeys(Widget parent, Iterable<Widget> children, {String? message})
```

Asserts if the given child list contains any duplicate non-null keys.

To invoke this function, use the following pattern:

```dart
class MyWidget extends StatelessWidget {
  MyWidget({ super.key, required this.children }) {
    assert(!debugChildrenHaveDuplicateKeys(this, children));
  }

  final List<Widget> children;

  // ...
}
```

If specified, the `message` overrides the default message.

For a version of this function that can be used in contexts where the list of items does not have a particular parent, see [debugItemsHaveDuplicateKeys].

Does nothing if asserts are disabled. Always returns false.

# debugItemsHaveDuplicateKeys()

```dart
bool debugItemsHaveDuplicateKeys(Iterable<Widget> items)
```

Asserts if the given list of items contains any duplicate non-null keys.

To invoke this function, use the following pattern:

```dart
assert(!debugItemsHaveDuplicateKeys(items));
```

For a version of this function specifically intended for parents checking their children lists, see [debugChildrenHaveDuplicateKeys].

Does nothing if asserts are disabled. Always returns false.

# debugCheckHasTable()

```dart
bool debugCheckHasTable(BuildContext context)
```

Asserts that the given context has a [Table] ancestor.

Used by [TableRowInkWell] to make sure that it is only used in an appropriate context.

To invoke this function, use the following pattern, typically in the relevant Widget's build method:

```dart
assert(debugCheckHasTable(context));
```

Always place this before any early returns, so that the invariant is checked in all cases. This prevents bugs from hiding until a particular codepath is hit.

This method can be expensive (it walks the element tree).

Does nothing if asserts are disabled. Always returns true.

# debugCheckHasMediaQuery()

```dart
bool debugCheckHasMediaQuery(BuildContext context)
```

Asserts that the given context has a [MediaQuery] ancestor.

Used by various widgets to make sure that they are only used in an appropriate context.

To invoke this function, use the following pattern, typically in the relevant Widget's build method:

```dart
assert(debugCheckHasMediaQuery(context));
```

Always place this before any early returns, so that the invariant is checked in all cases. This prevents bugs from hiding until a particular codepath is hit.

Does nothing if asserts are disabled. Always returns true.

# debugCheckHasDirectionality()

```dart
bool debugCheckHasDirectionality(BuildContext context, {String? why, String? hint, String? alternative})
```

Asserts that the given context has a [Directionality] ancestor.

Used by various widgets to make sure that they are only used in an appropriate context.

To invoke this function, use the following pattern, typically in the relevant Widget's build method:

```dart
assert(debugCheckHasDirectionality(context));
```

To improve the error messages you can add some extra color using the named arguments.

- why: explain why the direction is needed, for example "to resolve the 'alignment' argument". Should be an adverb phrase describing why.
- hint: explain why this might be happening, for example "The default value of the 'alignment' argument of the $runtimeType widget is an AlignmentDirectional value.". Should be a fully punctuated sentence.
- alternative: provide additional advice specific to the situation, especially an alternative to providing a Directionality ancestor. For example, "Alternatively, consider specifying the 'textDirection' argument.". Should be a fully punctuated sentence.

Each one can be null, in which case it is skipped (this is the default). If they are non-null, they are included in the order above, interspersed with the more generic advice regarding [Directionality].

Always place this before any early returns, so that the invariant is checked in all cases. This prevents bugs from hiding until a particular codepath is hit.

Does nothing if asserts are disabled. Always returns true.

See also:

- [debugCheckHasDirectionality], which is a similar, but more general painting-library level function.

# debugWidgetBuilderValue()

```dart
void debugWidgetBuilderValue(Widget widget, Widget? built)
```

Asserts that the `built` widget is not null.

Used when the given `widget` calls a builder function to check that the function returned a non-null value, as typically required.

Does nothing when asserts are disabled.

# debugCheckHasWidgetsLocalizations()

```dart
bool debugCheckHasWidgetsLocalizations(BuildContext context)
```

Asserts that the given context has a [Localizations] ancestor that contains a [WidgetsLocalizations] delegate.

To call this function, use the following pattern, typically in the relevant Widget's build method:

```dart
assert(debugCheckHasWidgetsLocalizations(context));
```

Always place this before any early returns, so that the invariant is checked in all cases. This prevents bugs from hiding until a particular codepath is hit.

Does nothing if asserts are disabled. Always returns true.

# debugCheckHasOverlay()

```dart
bool debugCheckHasOverlay(BuildContext context)
```

Asserts that the given context has an [Overlay] ancestor.

To call this function, use the following pattern, typically in the relevant Widget's build method:

```dart
assert(debugCheckHasOverlay(context));
```

Always place this before any early returns, so that the invariant is checked in all cases. This prevents bugs from hiding until a particular codepath is hit.

This method can be expensive (it walks the element tree).

Does nothing if asserts are disabled. Always returns true.

# debugAssertAllWidgetVarsUnset()

```dart
bool debugAssertAllWidgetVarsUnset(String reason)
```

Returns true if none of the widget library debug variables have been changed.

This function is used by the test framework to ensure that debug variables haven't been inadvertently changed.

See [the widgets library](widgets/widgets-library.html) for a complete list.
