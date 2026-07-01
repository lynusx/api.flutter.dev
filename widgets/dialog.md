# RawDialogRouteBuilder

```dart
typedef RawDialogRouteBuilder<T> = Route<T> Function(BuildContext context, WidgetBuilder builder)
```

A builder for a route that takes the build context and the widget intended to go inside the route as a parameter.

# showRawDialog()

```dart
Future<T?> showRawDialog<T>({required BuildContext context, required WidgetBuilder builder, RawDialogRouteBuilder<T>? routeBuilder, bool useRootNavigator = true, RouteSettings? routeSettings, bool fullscreenDialog = false})
```

Displays a dialog over the contents of the app.

{@template flutter.widgets.showRawDialog.windowing} If windowing is enabled via `flutter config --enable-windowing`, then the dialog is displayed in its own window using the windowing system, rather than as a modal overlay within the current window. This will only function on platforms that support the dialog window type. True dialog windows will lack barriers. {@endtemplate}

The parameter `builder` builds the content of the dialog.

{@template flutter.widgets.showRawDialog.context} The `context` argument is used to look up the [Navigator] and [Theme] for the dialog. It is only used when the method is called. Its corresponding widget can be safely removed from the tree before the dialog is closed. {@endtemplate}

The parameter `routeBuilder` builds the [Route] that will be pushed to the [Navigator]. Defaults to building a [RawDialogRoute]. When windowing is available, this parameter will be silently ignored.

{@template flutter.widgets.showRawDialog.navigator} The `useRootNavigator` argument is used to determine whether to push the dialog to the [Navigator] furthest from or nearest to the given `context`. By default, `useRootNavigator` is `true` and the dialog route created by this method is pushed to the root navigator. It can not be `null`. {@endtemplate}

{@template flutter.widgets.showRawDialog.routeSettings} The `routeSettings` argument is passed to [showGeneralDialog], see [RouteSettings] for details. {@endtemplate}

Returns a [Future] that resolves to the value (if any) that was passed to [Navigator.pop] when the dialog was closed.

See also:

- `WindowManager`, for more information on how to set up windowing.
