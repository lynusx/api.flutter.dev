@docImport 'app.dart'; @docImport 'color_scheme.dart'; @docImport 'page.dart'; @docImport 'predictive_back_page_transitions_builder.dart';

# FadeForwardsPageTransitionsBuilder

```dart
class FadeForwardsPageTransitionsBuilder extends PageTransitionsBuilder {}
```

Used by [PageTransitionsTheme] to define a horizontal [MaterialPageRoute] page transition animation that looks like the default page transition used on Android U.

{@tool dartpad} This example shows the default page transition on Android.

** See code in examples/api/lib/material/page_transitions_theme/page_transitions_theme.3.dart ** {@end-tool}

See also:

- [FadeUpwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android O.
- [OpenUpwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android P.
- [ZoomPageTransitionsBuilder], which defines the default page transition that's similar to the one provided in Android Q.
- [CupertinoPageTransitionsBuilder], which defines a horizontal page transition that matches native iOS page transitions.
- [PredictiveBackPageTransitionsBuilder], which defines a page transition that allows peeking behind the current route on Android.
- [FadeForwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android U.

### FadeForwardsPageTransitionsBuilder()

```dart
FadeForwardsPageTransitionsBuilder({Color? backgroundColor})
```

Constructs a page transition animation that matches the transition used on Android U.

### backgroundColor

```dart
Color? backgroundColor
```

The background color during transition between two routes.

When a new page fades in and the old page fades out, this background color helps avoid a black background between two page.

Defaults to [ColorScheme.surface]

### kTransitionMilliseconds

```dart
int kTransitionMilliseconds
```

The value of [transitionDuration] in milliseconds.

Eyeballed on a physical Pixel 9 running Android 16. This does not match the actual value used by native Android, which is 800ms, because native Android is using Material 3 Expressive springs that are not currently supported by Flutter. So for now at least, this is an approximation.

### transitionDuration

```dart
Duration get transitionDuration
```

### delegatedTransition

```dart
DelegatedTransitionBuilder? get delegatedTransition
```

### buildTransitions()

```dart
Widget buildTransitions<T>(PageRoute<T>? route, BuildContext? context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```

# ZoomPageTransitionsBuilder

```dart
class ZoomPageTransitionsBuilder extends PageTransitionsBuilder {}
```

Used by [PageTransitionsTheme] to define a zooming [MaterialPageRoute] page transition animation that looks like the default page transition used on Android Q.

See also:

- [FadeUpwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android O.
- [OpenUpwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android P.
- [CupertinoPageTransitionsBuilder], which defines a horizontal page transition that matches native iOS page transitions.
- [PredictiveBackPageTransitionsBuilder], which defines a page transition that allows peeking behind the current route on Android.
- [FadeForwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android U.

### ZoomPageTransitionsBuilder()

```dart
ZoomPageTransitionsBuilder({bool allowSnapshotting = true, bool allowEnterRouteSnapshotting = true, Color? backgroundColor})
```

Constructs a page transition animation that matches the transition used on Android Q.

### allowSnapshotting

```dart
bool allowSnapshotting
```

Whether zoom page transitions will prefer to animate a snapshot of the entering and exiting routes.

If not specified, defaults to true.

When this value is true, zoom page transitions will snapshot the entering and exiting routes. These snapshots are then animated in place of the underlying widgets to improve performance of the transition.

Generally this means that animations that occur on the entering/exiting route while the route animation plays may appear frozen - unless they are a hero animation or something that is drawn in a separate overlay.

{@tool dartpad} This example shows a [MaterialApp] that disables snapshotting for the zoom transitions on Android.

** See code in examples/api/lib/material/page_transitions_theme/page_transitions_theme.1.dart ** {@end-tool}

See also:

- [PageRoute.allowSnapshotting], which enables or disables snapshotting on a per route basis.

### allowEnterRouteSnapshotting

```dart
bool allowEnterRouteSnapshotting
```

Whether to enable snapshotting on the entering route during the transition animation.

If not specified, defaults to true. If false, the route snapshotting will not be applied to the route being animating into, e.g. when transitioning from route A to route B, B will not be snapshotted.

### backgroundColor

```dart
Color? backgroundColor
```

The color of the scrim (background) that fades in and out during the transition.

If not provided, defaults to current theme's [ColorScheme.surface] color.

### delegatedTransition

```dart
DelegatedTransitionBuilder? get delegatedTransition
```

### buildTransitions()

```dart
Widget buildTransitions<T>(PageRoute<T> route, BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```

# PageTransitionsTheme

```dart
class PageTransitionsTheme with Diagnosticable {}
```

Defines the page transition animations used by [MaterialPageRoute] for different [TargetPlatform]s.

The [MaterialPageRoute.buildTransitions] method looks up the current [PageTransitionsTheme] with `Theme.of(context).pageTransitionsTheme` and delegates to [buildTransitions].

If a builder with a matching platform is not found, then the [ZoomPageTransitionsBuilder] is used.

{@tool dartpad} This example shows a [MaterialApp] that defines a custom [PageTransitionsTheme].

** See code in examples/api/lib/material/page_transitions_theme/page_transitions_theme.0.dart ** {@end-tool}

See also:

- [ThemeData.pageTransitionsTheme], which defines the default page transitions for the overall theme.
- [FadeUpwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android O.
- [OpenUpwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android P.
- [ZoomPageTransitionsBuilder], which defines the default page transition that's similar to the one provided by Android Q.
- [FadeForwardsPageTransitionsBuilder], which defines the default page transition that's similar to the one provided by Android U.
- [CupertinoPageTransitionsBuilder], which defines a horizontal page transition that matches native iOS page transitions.

### PageTransitionsTheme()

```dart
PageTransitionsTheme({Map<TargetPlatform, PageTransitionsBuilder> builders = _defaultBuilders})
```

Constructs an object that selects a transition based on the platform.

By default the list of builders is: [ZoomPageTransitionsBuilder] for [TargetPlatform.android], [TargetPlatform.windows] and [TargetPlatform.linux] and [CupertinoPageTransitionsBuilder] for [TargetPlatform.iOS] and [TargetPlatform.macOS].

### builders

```dart
Map<TargetPlatform, PageTransitionsBuilder> get builders
```

The [PageTransitionsBuilder]s supported by this theme.

### buildTransitions()

```dart
Widget buildTransitions<T>(PageRoute<T> route, BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```

Delegates to the builder for the current [ThemeData.platform]. If a builder for the current platform is not found, then the [ZoomPageTransitionsBuilder] is used.

[MaterialPageRoute.buildTransitions] delegates to this method.

### delegatedTransition()

```dart
DelegatedTransitionBuilder? delegatedTransition(TargetPlatform platform)
```

Provides the delegate transition for the target platform.

{@macro flutter.widgets.delegatedTransition}

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
