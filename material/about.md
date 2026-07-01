@docImport 'package:flutter/cupertino.dart';

@docImport 'drawer.dart'; @docImport 'list_tile_theme.dart';

# AboutListTile

```dart
class AboutListTile extends StatelessWidget {}
```

A [ListTile] that shows an about box.

This widget is often added to an app's [Drawer]. When tapped it shows an about box dialog with [showAboutDialog].

The about box will include a button that shows licenses for software used by the application. The licenses shown are those returned by the [LicenseRegistry] API, which can be used to add more licenses to the list.

If your application does not have a [Drawer], you should provide an affordance to call [showAboutDialog] or (at least) [showLicensePage].

{@tool dartpad} This sample shows two ways to open [AboutDialog]. The first one uses an [AboutListTile], and the second uses the [showAboutDialog] function.

** See code in examples/api/lib/material/about/about_list_tile.0.dart ** {@end-tool}

### AboutListTile()

```dart
AboutListTile({dynamic key, Widget? icon, Widget? child, String? applicationName, String? applicationVersion, Widget? applicationIcon, String? applicationLegalese, List<Widget>? aboutBoxChildren, bool? dense})
```

Creates a list tile for showing an about box.

The arguments are all optional. The application name, if omitted, will be derived from the nearest [Title] widget. The version, icon, and legalese values default to the empty string.

### icon

```dart
Widget? icon
```

The icon to show for this drawer item.

By default no icon is shown.

This is not necessarily the same as the image shown in the dialog box itself; which is controlled by the [applicationIcon] property.

### child

```dart
Widget? child
```

The label to show on this drawer item.

Defaults to a text widget that says "About Foo" where "Foo" is the application name specified by [applicationName].

### applicationName

```dart
String? applicationName
```

The name of the application.

This string is used in the default label for this drawer item (see [child]) and as the caption of the [AboutDialog] that is shown.

Defaults to the value of [Title.title], if a [Title] widget can be found. Otherwise, defaults to [Platform.resolvedExecutable].

### applicationVersion

```dart
String? applicationVersion
```

The version of this build of the application.

This string is shown under the application name in the [AboutDialog].

Defaults to the empty string.

### applicationIcon

```dart
Widget? applicationIcon
```

The icon to show next to the application name in the [AboutDialog].

By default no icon is shown.

Typically this will be an [ImageIcon] widget. It should honor the [IconTheme]'s [IconThemeData.size].

This is not necessarily the same as the icon shown on the drawer item itself, which is controlled by the [icon] property.

### applicationLegalese

```dart
String? applicationLegalese
```

A string to show in small print in the [AboutDialog].

Typically this is a copyright notice.

Defaults to the empty string.

### aboutBoxChildren

```dart
List<Widget>? aboutBoxChildren
```

Widgets to add to the [AboutDialog] after the name, version, and legalese.

This could include a link to a Web site, some descriptive text, credits, or other information to show in the about box.

Defaults to nothing.

### dense

```dart
bool? dense
```

Whether this list tile is part of a vertically dense list.

If this property is null, then its value is based on [ListTileThemeData.dense].

Dense list tiles default to a smaller height.

### build()

```dart
Widget build(BuildContext context)
```

# showAboutDialog()

```dart
void showAboutDialog({required BuildContext context, String? applicationName, String? applicationVersion, Widget? applicationIcon, String? applicationLegalese, List<Widget>? children, bool barrierDismissible = true, Color? barrierColor, String? barrierLabel, bool useRootNavigator = true, RouteSettings? routeSettings, Offset? anchorPoint})
```

Displays an [AboutDialog], which describes the application and provides a button to show licenses for software used by the application.

The arguments correspond to the properties on [AboutDialog].

If the application has a [Drawer], consider using [AboutListTile] instead of calling this directly.

If you do not need an about box in your application, you should at least provide an affordance to call [showLicensePage].

The licenses shown on the [LicensePage] are those returned by the [LicenseRegistry] API, which can be used to add more licenses to the list.

The [context], [barrierDismissible], [barrierColor], [barrierLabel], [useRootNavigator], [routeSettings] and [anchorPoint] arguments are passed to [showDialog], the documentation for which discusses how it is used.

# showAdaptiveAboutDialog()

```dart
void showAdaptiveAboutDialog({required BuildContext context, String? applicationName, String? applicationVersion, Widget? applicationIcon, String? applicationLegalese, List<Widget>? children, bool barrierDismissible = true, Color? barrierColor, String? barrierLabel, bool useRootNavigator = true, RouteSettings? routeSettings, Offset? anchorPoint})
```

Displays either a Material or Cupertino [AboutDialog] depending on platform, which describes the application and provides a button to show licenses for software used by the application.

The arguments correspond to the properties on [AboutDialog].

If the application has a [Drawer], consider using [AboutListTile] instead of calling this directly.

If you do not need an about box in your application, you should at least provide an affordance to call [showLicensePage].

The licenses shown on the [LicensePage] are those returned by the [LicenseRegistry] API, which can be used to add more licenses to the list.

On most platforms this function will act the same as [showDialog], except for iOS and macOS, in which case it will act the same as [showCupertinoDialog].

The [context], [barrierDismissible], [barrierColor], [barrierLabel], [useRootNavigator], [routeSettings] and [anchorPoint] arguments are passed to [showAdaptiveDialog], the documentation for which discusses how it is used.

# showLicensePage()

```dart
void showLicensePage({required BuildContext context, String? applicationName, String? applicationVersion, Widget? applicationIcon, String? applicationLegalese, bool useRootNavigator = false})
```

Displays a [LicensePage], which shows licenses for software used by the application.

The application arguments correspond to the properties on [LicensePage].

The `context` argument is used to look up the [Navigator] for the page.

The `useRootNavigator` argument is used to determine whether to push the page to the [Navigator] furthest from or nearest to the given `context`. It is `false` by default.

If the application has a [Drawer], consider using [AboutListTile] instead of calling this directly.

The [AboutDialog] shown by [showAboutDialog] includes a button that calls [showLicensePage].

The licenses shown on the [LicensePage] are those returned by the [LicenseRegistry] API, which can be used to add more licenses to the list.

# AboutDialog

```dart
class AboutDialog extends StatelessWidget {}
```

An about box. This is a dialog box with the application's icon, name, version number, and copyright, plus a button to show licenses for software used by the application.

To show an [AboutDialog], use [showAboutDialog].

{@youtube 560 315 https://www.youtube.com/watch?v=YFCSODyFxbE}

If the application has a [Drawer], the [AboutListTile] widget can make the process of showing an about dialog simpler.

The [AboutDialog] shown by [showAboutDialog] includes a button that calls [showLicensePage].

The licenses shown on the [LicensePage] are those returned by the [LicenseRegistry] API, which can be used to add more licenses to the list.

### AboutDialog()

```dart
AboutDialog({dynamic key, String? applicationName, String? applicationVersion, Widget? applicationIcon, String? applicationLegalese, List<Widget>? children})
```

Creates an about box.

The arguments are all optional. The application name, if omitted, will be derived from the nearest [Title] widget. The version, icon, and legalese values default to the empty string.

### AboutDialog.adaptive()

```dart
AboutDialog.adaptive({Key? key, String? applicationName, String? applicationVersion, Widget? applicationIcon, String? applicationLegalese, List<Widget>? children})
```

Creates an adaptive [AboutDialog] based on whether the target platform is iOS or macOS, following Material design's [Cross-platform guidelines](https://material.io/design/platform-guidance/cross-platform-adaptation.html).

Typically passed as a child of [showAdaptiveAboutDialog], which will display the [AboutDialog] differently based on platform.

This constructor offers the same customization options as the default [AboutDialog] constructor, allowing you to specify the application's [applicationName], [applicationVersion], [applicationIcon], [applicationLegalese], and additional [children] that appear in the dialog.

The target platform is based on the current [Theme]: [ThemeData.platform].

### applicationName

```dart
String? applicationName
```

The name of the application.

Defaults to the value of [Title.title], if a [Title] widget can be found. Otherwise, defaults to [Platform.resolvedExecutable].

### applicationVersion

```dart
String? applicationVersion
```

The version of this build of the application.

This string is shown under the application name.

Defaults to the empty string.

### applicationIcon

```dart
Widget? applicationIcon
```

The icon to show next to the application name.

By default no icon is shown.

Typically this will be an [ImageIcon] widget. It should honor the [IconTheme]'s [IconThemeData.size].

### applicationLegalese

```dart
String? applicationLegalese
```

A string to show in small print.

Typically this is a copyright notice.

Defaults to the empty string.

### children

```dart
List<Widget>? children
```

Widgets to add to the dialog box after the name, version, and legalese.

This could include a link to a Web site, some descriptive text, credits, or other information to show in the about box.

Defaults to nothing.

### build()

```dart
Widget build(BuildContext context)
```

# LicensePage

```dart
class LicensePage extends StatefulWidget {}
```

A page that shows licenses for software used by the application.

To show a [LicensePage], use [showLicensePage].

The [AboutDialog] shown by [showAboutDialog] and [AboutListTile] includes a button that calls [showLicensePage].

The licenses shown on the [LicensePage] are those returned by the [LicenseRegistry] API, which can be used to add more licenses to the list.

### LicensePage()

```dart
LicensePage({dynamic key, String? applicationName, String? applicationVersion, Widget? applicationIcon, String? applicationLegalese})
```

Creates a page that shows licenses for software used by the application.

The arguments are all optional. The application name, if omitted, will be derived from the nearest [Title] widget. The version and legalese values default to the empty string.

The licenses shown on the [LicensePage] are those returned by the [LicenseRegistry] API, which can be used to add more licenses to the list.

### applicationName

```dart
String? applicationName
```

The name of the application.

Defaults to the value of [Title.title], if a [Title] widget can be found. Otherwise, defaults to [Platform.resolvedExecutable].

### applicationVersion

```dart
String? applicationVersion
```

The version of this build of the application.

This string is shown under the application name.

Defaults to the empty string.

### applicationIcon

```dart
Widget? applicationIcon
```

The icon to show below the application name.

By default no icon is shown.

Typically this will be an [ImageIcon] widget. It should honor the [IconTheme]'s [IconThemeData.size].

### applicationLegalese

```dart
String? applicationLegalese
```

A string to show in small print.

Typically this is a copyright notice.

Defaults to the empty string.

### createState()

```dart
State<LicensePage> createState()
```
