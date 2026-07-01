@docImport 'app_bar.dart'; @docImport 'scaffold.dart';

# CollapseMode

```dart
enum CollapseMode {}
```

The collapsing effect while the space bar collapses from its full size.

The background widget will scroll in a parallax fashion.

The background widget pin in place until it reaches the min extent.

The background widget will act as normal with no collapsing effect.

# StretchMode

```dart
enum StretchMode {}
```

The stretching effect while the space bar stretches beyond its full size.

The background widget will expand to fill the extra space.

The background will blur using a [ui.ImageFilter.blur] effect.

The title will fade away as the user over-scrolls.

# FlexibleSpaceBar

```dart
class FlexibleSpaceBar extends StatefulWidget {}
```

The part of a Material Design [AppBar] that expands, collapses, and stretches.

{@youtube 560 315 https://www.youtube.com/watch?v=mSc7qFzxHDw}

Most commonly used in the [SliverAppBar.flexibleSpace] field, a flexible space bar expands and contracts as the app scrolls so that the [AppBar] reaches from the top of the app to the top of the scrolling contents of the app. When using [SliverAppBar.flexibleSpace], the [SliverAppBar.expandedHeight] must be large enough to accommodate the [SliverAppBar.flexibleSpace] widget.

Furthermore is included functionality for stretch behavior. When [SliverAppBar.stretch] is true, and your [ScrollPhysics] allow for overscroll, this space will stretch with the overscroll.

The widget that sizes the [AppBar] must wrap it in the widget returned by [FlexibleSpaceBar.createSettings], to convey sizing information down to the [FlexibleSpaceBar].

{@tool dartpad} This sample application demonstrates the different features of the [FlexibleSpaceBar] when used in a [SliverAppBar]. This app bar is configured to stretch into the overscroll space, and uses the [FlexibleSpaceBar.stretchModes] to apply `fadeTitle`, `blurBackground` and `zoomBackground`. The app bar also makes use of [CollapseMode.parallax] by default.

** See code in examples/api/lib/material/flexible_space_bar/flexible_space_bar.0.dart ** {@end-tool}

See also:

- [SliverAppBar], which implements the expanding and contracting.
- [AppBar], which is used by [SliverAppBar].
- <https://material.io/design/components/app-bars-top.html#behavior>

### FlexibleSpaceBar()

```dart
FlexibleSpaceBar({dynamic key, Widget? title, Widget? background, bool? centerTitle, EdgeInsetsGeometry? titlePadding, CollapseMode collapseMode = CollapseMode.parallax, List<StretchMode> stretchModes = const <StretchMode>[StretchMode.zoomBackground], double expandedTitleScale = 1.5})
```

Creates a flexible space bar.

Most commonly used in the [AppBar.flexibleSpace] field.

### title

```dart
Widget? title
```

The primary contents of the flexible space bar when expanded.

Typically a [Text] widget.

### background

```dart
Widget? background
```

Shown behind the [title] when expanded.

Typically an [Image] widget with [Image.fit] set to [BoxFit.cover].

### centerTitle

```dart
bool? centerTitle
```

Whether the title should be centered.

If the length of the title is greater than the available space, set this property to false. This aligns the title to the start of the flexible space bar and applies [titlePadding] to the title.

By default this property is true if the current target platform is [TargetPlatform.iOS] or [TargetPlatform.macOS], false otherwise.

### collapseMode

```dart
CollapseMode collapseMode
```

Collapse effect while scrolling.

Defaults to [CollapseMode.parallax].

### stretchModes

```dart
List<StretchMode> stretchModes
```

Stretch effect while over-scrolling.

Defaults to include [StretchMode.zoomBackground].

### titlePadding

```dart
EdgeInsetsGeometry? titlePadding
```

Defines how far the [title] is inset from either the widget's bottom-left or its center.

Typically this property is used to adjust how far the title is inset from the bottom-left and it is specified along with [centerTitle] false.

If [centerTitle] is true, then the title is centered within the flexible space bar with a bottom padding of 16.0 pixels.

If [centerTitle] is false and [FlexibleSpaceBarSettings.hasLeading] is true, then the title is aligned to the start of the flexible space bar with the [titlePadding] applied. If [titlePadding] is null, then defaults to start padding of 72.0 pixels and bottom padding of 16.0 pixels.

### expandedTitleScale

```dart
double expandedTitleScale
```

Defines how much the title is scaled when the FlexibleSpaceBar is expanded due to the user scrolling downwards. The title is scaled uniformly on the x and y axes while maintaining its bottom-left position (bottom-center if [centerTitle] is true).

Defaults to 1.5 and must be greater than 1.

### createSettings()

```dart
Widget createSettings({double? toolbarOpacity, double? minExtent, double? maxExtent, bool? isScrolledUnder, bool? hasLeading, required double currentExtent, required Widget child})
```

Wraps a widget that contains an [AppBar] to convey sizing information down to the [FlexibleSpaceBar].

Used by [Scaffold] and [SliverAppBar].

`toolbarOpacity` affects how transparent the text within the toolbar appears. `minExtent` sets the minimum height of the resulting [FlexibleSpaceBar] when fully collapsed. `maxExtent` sets the maximum height of the resulting [FlexibleSpaceBar] when fully expanded. `currentExtent` sets the scale of the [FlexibleSpaceBar.background] and [FlexibleSpaceBar.title] widgets of [FlexibleSpaceBar] upon initialization. `scrolledUnder` is true if the [FlexibleSpaceBar] overlaps the app's primary scrollable, false if it does not, and null if the caller has not determined as much. See also:

- [FlexibleSpaceBarSettings] which creates a settings object that can be used to specify these settings to a [FlexibleSpaceBar].

### createState()

```dart
State<FlexibleSpaceBar> createState()
```

# FlexibleSpaceBarSettings

```dart
class FlexibleSpaceBarSettings extends InheritedWidget {}
```

Provides sizing and opacity information to a [FlexibleSpaceBar].

See also:

- [FlexibleSpaceBar] which creates a flexible space bar.

### FlexibleSpaceBarSettings()

```dart
FlexibleSpaceBarSettings({dynamic key, required double toolbarOpacity, required double minExtent, required double maxExtent, required double currentExtent, required dynamic child, bool? isScrolledUnder, bool? hasLeading})
```

Creates a Flexible Space Bar Settings widget.

Used by [Scaffold] and [SliverAppBar]. [child] must have a [FlexibleSpaceBar] widget in its tree for the settings to take affect.

### toolbarOpacity

```dart
double toolbarOpacity
```

Affects how transparent the text within the toolbar appears.

### minExtent

```dart
double minExtent
```

Minimum height of the resulting [FlexibleSpaceBar] when fully collapsed.

### maxExtent

```dart
double maxExtent
```

Maximum height of the resulting [FlexibleSpaceBar] when fully expanded.

### currentExtent

```dart
double currentExtent
```

If the [FlexibleSpaceBar.title] or the [FlexibleSpaceBar.background] is not null, then this value is used to calculate the relative scale of these elements upon initialization.

### isScrolledUnder

```dart
bool? isScrolledUnder
```

True if the FlexibleSpaceBar overlaps the primary scrollable's contents.

This value is used by the [AppBar] to resolve [AppBar.backgroundColor] against [WidgetState.scrolledUnder], i.e. to enable apps to specify different colors when content has been scrolled up and behind the app bar.

Null if the caller hasn't determined if the FlexibleSpaceBar overlaps the primary scrollable's contents.

### hasLeading

```dart
bool? hasLeading
```

True if the FlexibleSpaceBar has a leading widget.

This value is used by the [FlexibleSpaceBar] to determine if there should be a gap between the leading widget and the title.

Null if the caller hasn't determined if the FlexibleSpaceBar has a leading widget.

### updateShouldNotify()

```dart
bool updateShouldNotify(FlexibleSpaceBarSettings oldWidget)
```
