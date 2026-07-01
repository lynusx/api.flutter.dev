@docImport 'package:flutter/material.dart';

# Adaptation

```dart
class Adaptation<T> {}
```

Defines a customized theme for components with an `adaptive` factory constructor.

Currently, only [Switch.adaptive] supports this class.

### Adaptation()

```dart
Adaptation()
```

Creates an [Adaptation].

### type

```dart
Type get type
```

The adaptation's type.

### adapt()

```dart
T adapt(ThemeData theme, T defaultValue)
```

Typically, this is overridden to return an instance of a custom component ThemeData class, like [SwitchThemeData], instead of the defaultValue.

Factory constructors that support adaptations - currently only [Switch.adaptive] - look for a type-specific adaptation in [ThemeData.adaptationMap] when computing their effective default component theme. If a matching adaptation is not found, the component may choose to use a default adaptation. For example, the [Switch.adaptive] component uses an empty [SwitchThemeData] if a matching adaptation is not found, for the sake of backwards compatibility.

{@tool dartpad} This sample shows how to create and use subclasses of [Adaptation] that define adaptive [SwitchThemeData]s. The [adapt] method in this example is overridden to only customize cupertino-style switches, but it can also be used to customize any other platforms.

** See code in examples/api/lib/material/switch/switch.4.dart ** {@end-tool}

# ThemeExtension

```dart
abstract class ThemeExtension<T extends ThemeExtension<T>> {}
```

An interface that defines custom additions to a [ThemeData] object.

{@youtube 560 315 https://www.youtube.com/watch?v=8-szcYzFVao}

Typically used for custom colors. To use, subclass [ThemeExtension], define a number of fields (e.g. [Color]s), and implement the [copyWith] and [lerp] methods. The latter will ensure smooth transitions of properties when switching themes.

{@tool dartpad} This sample shows how to create and use a subclass of [ThemeExtension] that defines two colors.

** See code in examples/api/lib/material/theme/theme_extension.1.dart ** {@end-tool}

### ThemeExtension()

```dart
ThemeExtension()
```

Enable const constructor for subclasses.

### type

```dart
Object get type
```

The extension's type.

### copyWith()

```dart
ThemeExtension<T> copyWith()
```

Creates a copy of this theme extension with the given fields replaced by the non-null parameter values.

### lerp()

```dart
ThemeExtension<T> lerp(ThemeExtension<T>? other, double t)
```

Linearly interpolate with another [ThemeExtension] object.

{@macro dart.ui.shadow.lerp}

# MaterialTapTargetSize

```dart
enum MaterialTapTargetSize {}
```

Configures the tap target and layout size of certain Material widgets.

Changing the value in [ThemeData.materialTapTargetSize] will affect the accessibility experience.

Some of the impacted widgets include:

- [FloatingActionButton], only the mini tap target size is increased.
- [MaterialButton]
- [OutlinedButton]
- [TextButton]
- [ElevatedButton]
- [IconButton]
- The time picker widget ([showTimePicker])
- [SnackBar]
- [Chip]
- [RawChip]
- [InputChip]
- [ChoiceChip]
- [FilterChip]
- [ActionChip]
- [Radio]
- [Switch]
- [Checkbox]

Expands the minimum tap target size to 48px by 48px.

This is the default value of [ThemeData.materialTapTargetSize] and the recommended size to conform to Android accessibility scanner recommendations.

Shrinks the tap target size to the minimum provided by the Material specification.

# ThemeData

```dart
class ThemeData with Diagnosticable {}
```

Defines the configuration of the overall visual [Theme] for a [MaterialApp] or a widget subtree within the app.

The [MaterialApp] theme property can be used to configure the appearance of the entire app. Widget subtrees within an app can override the app's theme by including a [Theme] widget at the top of the subtree.

Widgets whose appearance should align with the overall theme can obtain the current theme's configuration with [Theme.of]. Material components typically depend exclusively on the [colorScheme] and [textTheme]. These properties are guaranteed to have non-null values.

The static [Theme.of] method finds the [ThemeData] value specified for the nearest [BuildContext] ancestor. This lookup is inexpensive, essentially just a single HashMap access. It can sometimes be a little confusing because [Theme.of] can not see a [Theme] widget that is defined in the current build method's context. To overcome that, create a new custom widget for the subtree that appears below the new [Theme], or insert a widget that creates a new BuildContext, like [Builder].

{@tool dartpad} This example demonstrates how a typical [MaterialApp] specifies and uses a custom [Theme]. The theme's [ColorScheme] is based on a single "seed" color and configures itself to match the platform's current light or dark color configuration. The theme overrides the default configuration of [FloatingActionButton] to show how to customize the appearance a class of components.

** See code in examples/api/lib/material/theme_data/theme_data.0.dart ** {@end-tool}

See <https://material.io/design/color/> for more discussion on how to pick the right colors.

### ThemeData()

```dart
ThemeData({Iterable<Adaptation<Object>>? adaptations, bool? applyElevationOverlayColor, NoDefaultCupertinoThemeData? cupertinoOverrideTheme, Iterable<ThemeExtension<dynamic>>? extensions, Object? inputDecorationTheme, MaterialTapTargetSize? materialTapTargetSize, PageTransitionsTheme? pageTransitionsTheme, TargetPlatform? platform, ScrollbarThemeData? scrollbarTheme, InteractiveInkFeatureFactory? splashFactory, bool? useMaterial3, bool? useSystemColors, VisualDensity? visualDensity, ColorScheme? colorScheme, Brightness? brightness, Color? colorSchemeSeed, Color? canvasColor, Color? cardColor, Color? disabledColor, Color? dividerColor, Color? focusColor, Color? highlightColor, Color? hintColor, Color? hoverColor, Color? primaryColor, Color? primaryColorDark, Color? primaryColorLight, MaterialColor? primarySwatch, Color? scaffoldBackgroundColor, Color? secondaryHeaderColor, Color? shadowColor, Color? splashColor, Color? unselectedWidgetColor, String? fontFamily, List<String>? fontFamilyFallback, String? package, IconThemeData? iconTheme, IconThemeData? primaryIconTheme, TextTheme? primaryTextTheme, TextTheme? textTheme, Typography? typography, ActionIconThemeData? actionIconTheme, Object? appBarTheme, BadgeThemeData? badgeTheme, MaterialBannerThemeData? bannerTheme, BottomAppBarThemeData? bottomAppBarTheme, BottomNavigationBarThemeData? bottomNavigationBarTheme, BottomSheetThemeData? bottomSheetTheme, ButtonThemeData? buttonTheme, CardThemeData? cardTheme, CarouselViewThemeData? carouselViewTheme, CheckboxThemeData? checkboxTheme, ChipThemeData? chipTheme, DataTableThemeData? dataTableTheme, DatePickerThemeData? datePickerTheme, DialogThemeData? dialogTheme, DividerThemeData? dividerTheme, DrawerThemeData? drawerTheme, DropdownMenuThemeData? dropdownMenuTheme, ElevatedButtonThemeData? elevatedButtonTheme, ExpansionTileThemeData? expansionTileTheme, FilledButtonThemeData? filledButtonTheme, FloatingActionButtonThemeData? floatingActionButtonTheme, IconButtonThemeData? iconButtonTheme, ListTileThemeData? listTileTheme, MenuBarThemeData? menuBarTheme, MenuButtonThemeData? menuButtonTheme, MenuThemeData? menuTheme, NavigationBarThemeData? navigationBarTheme, NavigationDrawerThemeData? navigationDrawerTheme, NavigationRailThemeData? navigationRailTheme, OutlinedButtonThemeData? outlinedButtonTheme, PopupMenuThemeData? popupMenuTheme, ProgressIndicatorThemeData? progressIndicatorTheme, RadioThemeData? radioTheme, SearchBarThemeData? searchBarTheme, SearchViewThemeData? searchViewTheme, SegmentedButtonThemeData? segmentedButtonTheme, SliderThemeData? sliderTheme, SnackBarThemeData? snackBarTheme, SwitchThemeData? switchTheme, TabBarThemeData? tabBarTheme, TextButtonThemeData? textButtonTheme, TextSelectionThemeData? textSelectionTheme, TimePickerThemeData? timePickerTheme, ToggleButtonsThemeData? toggleButtonsTheme, TooltipThemeData? tooltipTheme, ButtonBarThemeData? buttonBarTheme, Color? dialogBackgroundColor, Color? indicatorColor})
```

Create a [ThemeData] that's used to configure a [Theme].

The [colorScheme] and [textTheme] are used by the Material components to compute default values for visual properties. The API documentation for each component widget explains exactly how the defaults are computed.

When providing a [ColorScheme], apps can either provide one directly with the [colorScheme] parameter, or have one generated for them by using the [colorSchemeSeed] and [brightness] parameters. A generated color scheme will be based on the tones of [colorSchemeSeed] and all of its contrasting color will meet accessibility guidelines for readability. (See [ColorScheme.fromSeed] for more details.)

If the app wants to customize a generated color scheme, it can use [ColorScheme.fromSeed] directly and then [ColorScheme.copyWith] on the result to override any colors that need to be replaced. The result of this can be used as the [colorScheme] directly.

For historical reasons, instead of using a [colorSchemeSeed] or [colorScheme], you can provide either a [primaryColor] or [primarySwatch] to construct the [colorScheme], but the results will not be as complete as when using generation from a seed color.

If [colorSchemeSeed] is non-null then [colorScheme], [primaryColor] and [primarySwatch] must all be null.

The [textTheme] [TextStyle] colors are black if the color scheme's brightness is [Brightness.light], and white for [Brightness.dark].

To override the appearance of specific components, provide a component theme parameter like [sliderTheme], [toggleButtonsTheme], or [bottomNavigationBarTheme].

When [useSystemColors] is true and the platform supports system colors, then the system colors will be used to override certain theme colors. The [colorScheme], [textTheme], [elevatedButtonTheme], [outlinedButtonTheme], [textButtonTheme], [filledButtonTheme], and [floatingActionButtonTheme] are overriden by the system colors.

See also:

- [ThemeData.from], which creates a ThemeData from a [ColorScheme].
- [ThemeData.light], which creates the default light theme.
- [ThemeData.dark], which creates the default dark theme.
- [ColorScheme.fromSeed], which is used to create a [ColorScheme] from a seed color.

### ThemeData.raw()

```dart
ThemeData.raw({required Map<Type, Adaptation<Object>> adaptationMap, required bool applyElevationOverlayColor, required NoDefaultCupertinoThemeData? cupertinoOverrideTheme, required Map<Object, ThemeExtension<dynamic>> extensions, required InputDecorationThemeData inputDecorationTheme, required MaterialTapTargetSize materialTapTargetSize, required PageTransitionsTheme pageTransitionsTheme, required TargetPlatform platform, required ScrollbarThemeData scrollbarTheme, required InteractiveInkFeatureFactory splashFactory, required bool useMaterial3, required VisualDensity visualDensity, required ColorScheme colorScheme, required Color canvasColor, required Color cardColor, required Color disabledColor, required Color dividerColor, required Color focusColor, required Color highlightColor, required Color hintColor, required Color hoverColor, required Color primaryColor, required Color primaryColorDark, required Color primaryColorLight, required Color scaffoldBackgroundColor, required Color secondaryHeaderColor, required Color shadowColor, required Color splashColor, required Color unselectedWidgetColor, required IconThemeData iconTheme, required IconThemeData primaryIconTheme, required TextTheme primaryTextTheme, required TextTheme textTheme, required Typography typography, required ActionIconThemeData? actionIconTheme, required AppBarThemeData appBarTheme, required BadgeThemeData badgeTheme, required MaterialBannerThemeData bannerTheme, required BottomAppBarThemeData bottomAppBarTheme, required BottomNavigationBarThemeData bottomNavigationBarTheme, required BottomSheetThemeData bottomSheetTheme, required ButtonThemeData buttonTheme, required CardThemeData cardTheme, required CarouselViewThemeData carouselViewTheme, required CheckboxThemeData checkboxTheme, required ChipThemeData chipTheme, required DataTableThemeData dataTableTheme, required DatePickerThemeData datePickerTheme, required DialogThemeData dialogTheme, required DividerThemeData dividerTheme, required DrawerThemeData drawerTheme, required DropdownMenuThemeData dropdownMenuTheme, required ElevatedButtonThemeData elevatedButtonTheme, required ExpansionTileThemeData expansionTileTheme, required FilledButtonThemeData filledButtonTheme, required FloatingActionButtonThemeData floatingActionButtonTheme, required IconButtonThemeData iconButtonTheme, required ListTileThemeData listTileTheme, required MenuBarThemeData menuBarTheme, required MenuButtonThemeData menuButtonTheme, required MenuThemeData menuTheme, required NavigationBarThemeData navigationBarTheme, required NavigationDrawerThemeData navigationDrawerTheme, required NavigationRailThemeData navigationRailTheme, required OutlinedButtonThemeData outlinedButtonTheme, required PopupMenuThemeData popupMenuTheme, required ProgressIndicatorThemeData progressIndicatorTheme, required RadioThemeData radioTheme, required SearchBarThemeData searchBarTheme, required SearchViewThemeData searchViewTheme, required SegmentedButtonThemeData segmentedButtonTheme, required SliderThemeData sliderTheme, required SnackBarThemeData snackBarTheme, required SwitchThemeData switchTheme, required TabBarThemeData tabBarTheme, required TextButtonThemeData textButtonTheme, required TextSelectionThemeData textSelectionTheme, required TimePickerThemeData timePickerTheme, required ToggleButtonsThemeData toggleButtonsTheme, required TooltipThemeData tooltipTheme, ButtonBarThemeData? buttonBarTheme, required Color dialogBackgroundColor, required Color indicatorColor})
```

Create a [ThemeData] given a set of exact values. Most values must be specified. They all must also be non-null except for [cupertinoOverrideTheme], and deprecated members.

This will rarely be used directly. It is used by [lerp] to create intermediate themes based on two themes created with the [ThemeData] constructor.

### ThemeData.from()

```dart
ThemeData.from({required ColorScheme colorScheme, TextTheme? textTheme, bool? useMaterial3})
```

Create a [ThemeData] based on the colors in the given [colorScheme] and text styles of the optional [textTheme].

If [colorScheme].brightness is [Brightness.dark] then [ThemeData.applyElevationOverlayColor] will be set to true to support the Material dark theme method for indicating elevation by applying a semi-transparent onSurface color on top of the surface color.

This is the recommended method to theme your application. As we move forward we will be converting all the widget implementations to only use colors or colors derived from those in [ColorScheme].

{@tool snippet} This example will set up an application to use the baseline Material Design light and dark themes.

```dart
MaterialApp(
  theme: ThemeData.from(colorScheme: const ColorScheme.light()),
  darkTheme: ThemeData.from(colorScheme: const ColorScheme.dark()),
)
```

{@end-tool}

See <https://material.io/design/color/> for more discussion on how to pick the right colors.

### ThemeData.light()

```dart
ThemeData.light({bool? useMaterial3})
```

A default light theme.

This theme does not contain text geometry. Instead, it is expected that this theme is localized using text geometry using [ThemeData.localize].

### ThemeData.dark()

```dart
ThemeData.dark({bool? useMaterial3})
```

A default dark theme.

This theme does not contain text geometry. Instead, it is expected that this theme is localized using text geometry using [ThemeData.localize].

### ThemeData.fallback()

```dart
ThemeData.fallback({bool? useMaterial3})
```

The default color theme. Same as [ThemeData.light].

This is used by [Theme.of] when no theme has been specified.

This theme does not contain text geometry. Instead, it is expected that this theme is localized using text geometry using [ThemeData.localize].

Most applications would use [Theme.of], which provides correct localized text geometry.

### getAdaptation()

```dart
Adaptation<T>? getAdaptation<T>()
```

Used to obtain a particular [Adaptation] from [adaptationMap].

To get an adaptation, use `Theme.of(context).getAdaptation<MyAdaptation>()`.

### brightness

```dart
Brightness get brightness
```

The overall theme brightness.

The default [TextStyle] color for the [textTheme] is black if the theme is constructed with [Brightness.light] and white if the theme is constructed with [Brightness.dark].

### applyElevationOverlayColor

```dart
bool applyElevationOverlayColor
```

Apply a semi-transparent overlay color on Material surfaces to indicate elevation for dark themes.

If [useMaterial3] is true, then this flag is ignored as there is a new [Material.surfaceTintColor] used to create an overlay for Material 3. This flag is meant only for the Material 2 elevation overlay for dark themes.

Material drop shadows can be difficult to see in a dark theme, so the elevation of a surface should be portrayed with an "overlay" in addition to the shadow. As the elevation of the component increases, the overlay increases in opacity. [applyElevationOverlayColor] turns the application of this overlay on or off for dark themes.

If true and [brightness] is [Brightness.dark], a semi-transparent version of [ColorScheme.onSurface] will be applied on top of [Material] widgets that have a [ColorScheme.surface] color. The level of transparency is based on [Material.elevation] as per the Material Dark theme specification.

If false the surface color will be used unmodified.

Defaults to false in order to maintain backwards compatibility with apps that were built before the Material Dark theme specification was published. New apps should set this to true for any themes where [brightness] is [Brightness.dark].

See also:

- [Material.elevation], which effects the level of transparency of the overlay color.
- [ElevationOverlay.applyOverlay], which is used by [Material] to apply the overlay color to its surface color.
- <https://material.io/design/color/dark-theme.html>, which specifies how the overlay should be applied.

### cupertinoOverrideTheme

```dart
NoDefaultCupertinoThemeData? cupertinoOverrideTheme
```

Components of the [CupertinoThemeData] to override from the Material [ThemeData] adaptation.

By default, [cupertinoOverrideTheme] is null and Cupertino widgets descendant to the Material [Theme] will adhere to a [CupertinoTheme] derived from the Material [ThemeData]. e.g. [ThemeData]'s [ColorScheme] will also inform the [CupertinoThemeData]'s `primaryColor` etc.

This cascading effect for individual attributes of the [CupertinoThemeData] can be overridden using attributes of this [cupertinoOverrideTheme].

### extensions

```dart
Map<Object, ThemeExtension<dynamic>> extensions
```

Arbitrary additions to this theme.

To define extensions, pass an [Iterable] containing one or more [ThemeExtension] subclasses to [ThemeData.new] or [copyWith].

To obtain an extension, use [extension].

{@tool dartpad} This sample shows how to create and use a subclass of [ThemeExtension] that defines two colors.

** See code in examples/api/lib/material/theme/theme_extension.1.dart ** {@end-tool}

See also:

- [extension], a convenience function for obtaining a specific extension.

### extension()

```dart
T? extension<T>()
```

Used to obtain a particular [ThemeExtension] from [extensions].

Obtain with `Theme.of(context).extension<MyThemeExtension>()`.

See [extensions] for an interactive example.

### adaptationMap

```dart
Map<Type, Adaptation<Object>> adaptationMap
```

A map which contains the adaptations for the theme. The entry's key is the type of the adaptation; the value is the adaptation itself.

To obtain an adaptation, use [getAdaptation].

### inputDecorationTheme

```dart
InputDecorationThemeData inputDecorationTheme
```

The default [InputDecoration] values for [InputDecorator], [TextField], and [TextFormField] are based on this theme.

See [InputDecoration.applyDefaults].

### materialTapTargetSize

```dart
MaterialTapTargetSize materialTapTargetSize
```

Configures the hit test size of certain Material widgets.

Defaults to a [platform]-appropriate size: [MaterialTapTargetSize.padded] on mobile platforms, [MaterialTapTargetSize.shrinkWrap] on desktop platforms.

### pageTransitionsTheme

```dart
PageTransitionsTheme pageTransitionsTheme
```

Default [MaterialPageRoute] transitions per [TargetPlatform].

[MaterialPageRoute.buildTransitions] delegates to a [platform] specific [PageTransitionsBuilder]. If a matching builder is not found, a builder whose platform is null is used.

### platform

```dart
TargetPlatform platform
```

The platform the material widgets should adapt to target.

Defaults to the current platform, as exposed by [defaultTargetPlatform]. This should be used in order to style UI elements according to platform conventions.

Widgets from the material library should use this getter (via [Theme.of]) to determine the current platform for the purpose of emulating the platform behavior (e.g. scrolling or haptic effects). Widgets and render objects at lower layers that try to emulate the underlying platform can depend on [defaultTargetPlatform] directly, or may require that the target platform be provided as an argument. The [dart:io.Platform] object should only be used directly when it's critical to actually know the current platform, without any overrides possible (for example, when a system API is about to be called).

In a test environment, the platform returned is [TargetPlatform.android] regardless of the host platform. (Android was chosen because the tests were originally written assuming Android-like behavior, and we added platform adaptations for other platforms later). Tests can check behavior for other platforms by setting the [platform] of the [Theme] explicitly to another [TargetPlatform] value, or by setting [debugDefaultTargetPlatformOverride].

Determines the defaults for [typography] and [materialTapTargetSize].

### scrollbarTheme

```dart
ScrollbarThemeData scrollbarTheme
```

A theme for customizing the colors, thickness, and shape of [Scrollbar]s.

### splashFactory

```dart
InteractiveInkFeatureFactory splashFactory
```

Defines the appearance of ink splashes produces by [InkWell] and [InkResponse].

See also:

- [InkSplash.splashFactory], which defines the default splash.
- [InkRipple.splashFactory], which defines a splash that spreads out more aggressively than the default.
- [InkSparkle.splashFactory], which defines a more aggressive and organic splash with sparkle effects.

### useMaterial3

```dart
bool useMaterial3
```

A temporary flag that can be used to opt-out of Material 3 features.

This flag is _true_ by default. If false, then components will continue to use the colors, typography and other features of Material 2.

In the long run this flag will be deprecated and eventually only Material 3 will be supported. We recommend that applications migrate to Material 3 as soon as that's practical. Until that migration is complete, this flag can be set to false.

## Defaults

If a [ThemeData] is _constructed_ with [useMaterial3] set to true, then some properties will get updated defaults. However, the [ThemeData.copyWith] method with [useMaterial3] set to true will _not_ change any of these properties in the resulting [ThemeData].

 <style>table,td,th { border-collapse: collapse; padding: 0.45em; } td { border: 1px solid }</style>

| Property        | Material 3 default             | Material 2 default             |
| :-------------- | :----------------------------- | :----------------------------- |
| [colorScheme]   | M3 baseline light color scheme | M2 baseline light color scheme |
| [typography]    | [Typography.material2021]      | [Typography.material2014]      |
| [splashFactory] | [InkSparkle]* or [InkRipple]   | [InkSplash]                    |

\* if the target platform is Android and the app is not running on the web, otherwise it will fallback to [InkRipple].

If [brightness] is [Brightness.dark] then the default color scheme will be either the M3 baseline dark color scheme or the M2 baseline dark color scheme depending on [useMaterial3].

## Affected widgets

This flag affects styles and components.

### Styles

- Color: [ColorScheme], [Material] (see table above)
- Shape: (see components below)
- Typography: [Typography] (see table above)

### Components

- Badges: [Badge]
- Bottom app bar: [BottomAppBar]
- Bottom sheets: [BottomSheet]
- Buttons - Common buttons: [ElevatedButton], [FilledButton], [FilledButton.tonal], [OutlinedButton], [TextButton] - FAB: [FloatingActionButton], [FloatingActionButton.extended] - Icon buttons: [IconButton], [IconButton.filled] (_new_), [IconButton.filledTonal], [IconButton.outlined] - Segmented buttons: [SegmentedButton] (replacing [ToggleButtons])
- Cards: [Card]
- Checkbox: [Checkbox], [CheckboxListTile]
- Chips: - [ActionChip] (used for Assist and Suggestion chips), - [FilterChip], [ChoiceChip] (used for single selection filter chips), - [InputChip]
- Date pickers: [showDatePicker], [showDateRangePicker], [DatePickerDialog], [DateRangePickerDialog], [InputDatePickerFormField]
- Dialogs: [AlertDialog], [Dialog.fullscreen]
- Divider: [Divider], [VerticalDivider]
- Lists: [ListTile]
- Menus: [MenuAnchor], [DropdownMenu], [MenuBar]
- Navigation bar: [NavigationBar] (replacing [BottomNavigationBar])
- Navigation drawer: [NavigationDrawer] (replacing [Drawer])
- Navigation rail: [NavigationRail]
- Progress indicators: [CircularProgressIndicator], [LinearProgressIndicator]
- Radio button: [Radio], [RadioListTile]
- Search: [SearchBar], [SearchAnchor],
- Snack bar: [SnackBar]
- Slider: [Slider], [RangeSlider]
- Switch: [Switch], [SwitchListTile]
- Tabs: [TabBar], [TabBar.secondary]
- TextFields: [TextField] together with its [InputDecoration]
- Time pickers: [showTimePicker], [TimePickerDialog]
- Top app bar: [AppBar], [SliverAppBar], [SliverAppBar.medium], [SliverAppBar.large]

In addition, this flag enables features introduced in Android 12.

- Stretch overscroll: [MaterialScrollBehavior]
- Ripple: `splashFactory` (see table above)

See also:

- [Material 3 specification](https://m3.material.io/).

### visualDensity

```dart
VisualDensity visualDensity
```

The density value for specifying the compactness of various UI components.

{@template flutter.material.themedata.visualDensity} Density, in the context of a UI, is the vertical and horizontal "compactness" of the elements in the UI. It is unitless, since it means different things to different UI elements. For buttons, it affects the spacing around the centered label of the button. For lists, it affects the distance between baselines of entries in the list.

Typically, density values are integral, but any value in range may be used. The range includes values from [VisualDensity.minimumDensity] (which is -4), to [VisualDensity.maximumDensity] (which is 4), inclusive, where negative values indicate a denser, more compact, UI, and positive values indicate a less dense, more expanded, UI. If a component doesn't support the value given, it will clamp to the nearest supported value.

The default for visual densities is zero for both vertical and horizontal densities, which corresponds to the default visual density of components in the Material Design specification.

As a rule of thumb, a change of 1 or -1 in density corresponds to 4 logical pixels. However, this is not a strict relationship since components interpret the density values appropriately for their needs.

A larger value translates to a spacing increase (less dense), and a smaller value translates to a spacing decrease (more dense).

In Material Design 3, the [visualDensity] does not override the default visual for the following components which are set to [VisualDensity.standard] for all platforms:

- [IconButton] - To override the default value of [IconButton.visualDensity], use [ThemeData.iconButtonTheme] instead.
- [Checkbox] - To override the default value of [Checkbox.visualDensity], use [ThemeData.checkboxTheme] instead. {@endtemplate}

### canvasColor

```dart
Color canvasColor
```

The default color of [MaterialType.canvas] [Material].

### cardColor

```dart
Color cardColor
```

The color of [Material] when it is used as a [Card].

### colorScheme

```dart
ColorScheme colorScheme
```

{@macro flutter.material.color_scheme.ColorScheme}

This property was added much later than the theme's set of highly specific colors, like [cardColor], [canvasColor] etc. New components can be defined exclusively in terms of [colorScheme]. Existing components will gradually migrate to it, to the extent that is possible without significant backwards compatibility breaks.

### disabledColor

```dart
Color disabledColor
```

The color used for widgets that are inoperative, regardless of their state. For example, a disabled checkbox (which may be checked or unchecked).

### dividerColor

```dart
Color dividerColor
```

The color of [Divider]s and [PopupMenuDivider]s, also used between [ListTile]s, between rows in [DataTable]s, and so forth.

To create an appropriate [BorderSide] that uses this color, consider [Divider.createBorderSide].

### focusColor

```dart
Color focusColor
```

The focus color used indicate that a component has the input focus.

### highlightColor

```dart
Color highlightColor
```

The highlight color used during ink splash animations or to indicate an item in a menu is selected.

### hintColor

```dart
Color hintColor
```

The color to use for hint text or placeholder text, e.g. in [TextField] fields.

### hoverColor

```dart
Color hoverColor
```

The hover color used to indicate when a pointer is hovering over a component.

### primaryColor

```dart
Color primaryColor
```

The background color for major parts of the app (toolbars, tab bars, etc)

The theme's [colorScheme] property contains [ColorScheme.primary], as well as a color that contrasts well with the primary color called [ColorScheme.onPrimary]. It might be simpler to just configure an app's visuals in terms of the theme's [colorScheme].

### primaryColorDark

```dart
Color primaryColorDark
```

A darker version of the [primaryColor].

### primaryColorLight

```dart
Color primaryColorLight
```

A lighter version of the [primaryColor].

### scaffoldBackgroundColor

```dart
Color scaffoldBackgroundColor
```

The default color of the [Material] that underlies the [Scaffold]. The background color for a typical material app or a page within the app.

### secondaryHeaderColor

```dart
Color secondaryHeaderColor
```

The color of the header of a [PaginatedDataTable] when there are selected rows.

### shadowColor

```dart
Color shadowColor
```

The color that the [Material] widget uses to draw elevation shadows.

Defaults to fully opaque black.

Shadows can be difficult to see in a dark theme, so the elevation of a surface should be rendered with an "overlay" in addition to the shadow. As the elevation of the component increases, the overlay increases in opacity. The [applyElevationOverlayColor] property turns the elevation overlay on or off for dark themes.

### splashColor

```dart
Color splashColor
```

The color of ink splashes.

See also:

- [splashFactory], which defines the appearance of the splash.

### unselectedWidgetColor

```dart
Color unselectedWidgetColor
```

The color used for widgets in their inactive (but enabled) state. For example, an unchecked checkbox. See also [disabledColor].

### iconTheme

```dart
IconThemeData iconTheme
```

An icon theme that contrasts with the card and canvas colors.

### primaryIconTheme

```dart
IconThemeData primaryIconTheme
```

An icon theme that contrasts with the primary color.

### primaryTextTheme

```dart
TextTheme primaryTextTheme
```

A text theme that contrasts with the primary color.

### textTheme

```dart
TextTheme textTheme
```

Text with a color that contrasts with the card and canvas colors.

### typography

```dart
Typography typography
```

The color and geometry [TextTheme] values used to configure [textTheme].

Defaults to a [platform]-appropriate typography.

### actionIconTheme

```dart
ActionIconThemeData? actionIconTheme
```

A theme for customizing icons of [BackButtonIcon], [CloseButtonIcon], [DrawerButtonIcon], or [EndDrawerButtonIcon].

### appBarTheme

```dart
AppBarThemeData appBarTheme
```

A theme for customizing the color, elevation, brightness, iconTheme and textTheme of [AppBar]s.

### badgeTheme

```dart
BadgeThemeData badgeTheme
```

A theme for customizing the color of [Badge]s.

### bannerTheme

```dart
MaterialBannerThemeData bannerTheme
```

A theme for customizing the color and text style of a [MaterialBanner].

### bottomAppBarTheme

```dart
BottomAppBarThemeData bottomAppBarTheme
```

A theme for customizing the shape, elevation, and color of a [BottomAppBar].

### bottomNavigationBarTheme

```dart
BottomNavigationBarThemeData bottomNavigationBarTheme
```

A theme for customizing the appearance and layout of [BottomNavigationBar] widgets.

### bottomSheetTheme

```dart
BottomSheetThemeData bottomSheetTheme
```

A theme for customizing the color, elevation, and shape of a bottom sheet.

### buttonTheme

```dart
ButtonThemeData buttonTheme
```

Defines the default configuration of button widgets, like [DropdownButton] and [ButtonBar].

### cardTheme

```dart
CardThemeData cardTheme
```

The colors and styles used to render [Card].

This is the value returned from [CardTheme.of].

### carouselViewTheme

```dart
CarouselViewThemeData carouselViewTheme
```

A theme for customizing the appearance and layout of [CarouselView] widgets.

### checkboxTheme

```dart
CheckboxThemeData checkboxTheme
```

A theme for customizing the appearance and layout of [Checkbox] widgets.

### chipTheme

```dart
ChipThemeData chipTheme
```

The colors and styles used to render [Chip]s.

This is the value returned from [ChipTheme.of].

### dataTableTheme

```dart
DataTableThemeData dataTableTheme
```

A theme for customizing the appearance and layout of [DataTable] widgets.

### datePickerTheme

```dart
DatePickerThemeData datePickerTheme
```

A theme for customizing the appearance and layout of [DatePickerDialog] widgets.

### dialogTheme

```dart
DialogThemeData dialogTheme
```

A theme for customizing the shape of a dialog.

### dividerTheme

```dart
DividerThemeData dividerTheme
```

A theme for customizing the color, thickness, and indents of [Divider]s, [VerticalDivider]s, etc.

### drawerTheme

```dart
DrawerThemeData drawerTheme
```

A theme for customizing the appearance and layout of [Drawer] widgets.

### dropdownMenuTheme

```dart
DropdownMenuThemeData dropdownMenuTheme
```

A theme for customizing the appearance and layout of [DropdownMenu] widgets.

### elevatedButtonTheme

```dart
ElevatedButtonThemeData elevatedButtonTheme
```

A theme for customizing the appearance and internal layout of [ElevatedButton]s.

### expansionTileTheme

```dart
ExpansionTileThemeData expansionTileTheme
```

A theme for customizing the visual properties of [ExpansionTile]s.

### filledButtonTheme

```dart
FilledButtonThemeData filledButtonTheme
```

A theme for customizing the appearance and internal layout of [FilledButton]s.

### floatingActionButtonTheme

```dart
FloatingActionButtonThemeData floatingActionButtonTheme
```

A theme for customizing the shape, elevation, and color of a [FloatingActionButton].

### iconButtonTheme

```dart
IconButtonThemeData iconButtonTheme
```

A theme for customizing the appearance and internal layout of [IconButton]s.

### listTileTheme

```dart
ListTileThemeData listTileTheme
```

A theme for customizing the appearance of [ListTile] widgets.

### menuBarTheme

```dart
MenuBarThemeData menuBarTheme
```

A theme for customizing the color, shape, elevation, and other [MenuStyle] aspects of the menu bar created by the [MenuBar] widget.

### menuButtonTheme

```dart
MenuButtonThemeData menuButtonTheme
```

A theme for customizing the color, shape, elevation, and text style of cascading menu buttons created by [SubmenuButton] or [MenuItemButton].

### menuTheme

```dart
MenuThemeData menuTheme
```

A theme for customizing the color, shape, elevation, and other [MenuStyle] attributes of menus created by the [SubmenuButton] widget.

### navigationBarTheme

```dart
NavigationBarThemeData navigationBarTheme
```

A theme for customizing the background color, text style, and icon themes of a [NavigationBar].

### navigationDrawerTheme

```dart
NavigationDrawerThemeData navigationDrawerTheme
```

A theme for customizing the background color, text style, and icon themes of a [NavigationDrawer].

### navigationRailTheme

```dart
NavigationRailThemeData navigationRailTheme
```

A theme for customizing the background color, elevation, text style, and icon themes of a [NavigationRail].

### outlinedButtonTheme

```dart
OutlinedButtonThemeData outlinedButtonTheme
```

A theme for customizing the appearance and internal layout of [OutlinedButton]s.

### popupMenuTheme

```dart
PopupMenuThemeData popupMenuTheme
```

A theme for customizing the color, shape, elevation, and text style of popup menus.

### progressIndicatorTheme

```dart
ProgressIndicatorThemeData progressIndicatorTheme
```

A theme for customizing the appearance and layout of [ProgressIndicator] widgets.

### radioTheme

```dart
RadioThemeData radioTheme
```

A theme for customizing the appearance and layout of [Radio] widgets.

### searchBarTheme

```dart
SearchBarThemeData searchBarTheme
```

A theme for customizing the appearance and layout of [SearchBar] widgets.

### searchViewTheme

```dart
SearchViewThemeData searchViewTheme
```

A theme for customizing the appearance and layout of search views created by [SearchAnchor] widgets.

### segmentedButtonTheme

```dart
SegmentedButtonThemeData segmentedButtonTheme
```

A theme for customizing the appearance and layout of [SegmentedButton] widgets.

### sliderTheme

```dart
SliderThemeData sliderTheme
```

A theme for customizing the appearance and layout of [Slider] widgets.

### snackBarTheme

```dart
SnackBarThemeData snackBarTheme
```

A theme for customizing colors, shape, elevation, and behavior of a [SnackBar].

### switchTheme

```dart
SwitchThemeData switchTheme
```

A theme for customizing the appearance and layout of [Switch] widgets.

### tabBarTheme

```dart
TabBarThemeData tabBarTheme
```

A theme for customizing the size, shape, and color of the tab bar indicator.

### textButtonTheme

```dart
TextButtonThemeData textButtonTheme
```

A theme for customizing the appearance and internal layout of [TextButton]s.

### textSelectionTheme

```dart
TextSelectionThemeData textSelectionTheme
```

A theme for customizing the appearance for text selection in [TextField] and [SelectableText] widgets.

### timePickerTheme

```dart
TimePickerThemeData timePickerTheme
```

A theme for customizing the appearance and layout of time picker widgets.

### toggleButtonsTheme

```dart
ToggleButtonsThemeData toggleButtonsTheme
```

A theme for customizing the appearance and layout of [ToggleButtons] widgets.

### tooltipTheme

```dart
TooltipThemeData tooltipTheme
```

A theme for customizing the appearance and layout of [Tooltip] widgets.

### buttonBarTheme

```dart
ButtonBarThemeData get buttonBarTheme
```

A theme for customizing the appearance and layout of [ButtonBar] widgets.

### dialogBackgroundColor

```dart
Color dialogBackgroundColor
```

The background color of [Dialog] elements.

### indicatorColor

```dart
Color indicatorColor
```

The color of the selected tab indicator in a tab bar.

### copyWith()

```dart
ThemeData copyWith({Iterable<Adaptation<Object>>? adaptations, bool? applyElevationOverlayColor, NoDefaultCupertinoThemeData? cupertinoOverrideTheme, Iterable<ThemeExtension<dynamic>>? extensions, Object? inputDecorationTheme, MaterialTapTargetSize? materialTapTargetSize, PageTransitionsTheme? pageTransitionsTheme, TargetPlatform? platform, ScrollbarThemeData? scrollbarTheme, InteractiveInkFeatureFactory? splashFactory, VisualDensity? visualDensity, ColorScheme? colorScheme, Brightness? brightness, Color? canvasColor, Color? cardColor, Color? disabledColor, Color? dividerColor, Color? focusColor, Color? highlightColor, Color? hintColor, Color? hoverColor, Color? primaryColor, Color? primaryColorDark, Color? primaryColorLight, Color? scaffoldBackgroundColor, Color? secondaryHeaderColor, Color? shadowColor, Color? splashColor, Color? unselectedWidgetColor, IconThemeData? iconTheme, IconThemeData? primaryIconTheme, TextTheme? primaryTextTheme, TextTheme? textTheme, Typography? typography, ActionIconThemeData? actionIconTheme, Object? appBarTheme, BadgeThemeData? badgeTheme, MaterialBannerThemeData? bannerTheme, BottomAppBarThemeData? bottomAppBarTheme, BottomNavigationBarThemeData? bottomNavigationBarTheme, BottomSheetThemeData? bottomSheetTheme, ButtonThemeData? buttonTheme, CardThemeData? cardTheme, CarouselViewThemeData? carouselViewTheme, CheckboxThemeData? checkboxTheme, ChipThemeData? chipTheme, DataTableThemeData? dataTableTheme, DatePickerThemeData? datePickerTheme, DialogThemeData? dialogTheme, DividerThemeData? dividerTheme, DrawerThemeData? drawerTheme, DropdownMenuThemeData? dropdownMenuTheme, ElevatedButtonThemeData? elevatedButtonTheme, ExpansionTileThemeData? expansionTileTheme, FilledButtonThemeData? filledButtonTheme, FloatingActionButtonThemeData? floatingActionButtonTheme, IconButtonThemeData? iconButtonTheme, ListTileThemeData? listTileTheme, MenuBarThemeData? menuBarTheme, MenuButtonThemeData? menuButtonTheme, MenuThemeData? menuTheme, NavigationBarThemeData? navigationBarTheme, NavigationDrawerThemeData? navigationDrawerTheme, NavigationRailThemeData? navigationRailTheme, OutlinedButtonThemeData? outlinedButtonTheme, PopupMenuThemeData? popupMenuTheme, ProgressIndicatorThemeData? progressIndicatorTheme, RadioThemeData? radioTheme, SearchBarThemeData? searchBarTheme, SearchViewThemeData? searchViewTheme, SegmentedButtonThemeData? segmentedButtonTheme, SliderThemeData? sliderTheme, SnackBarThemeData? snackBarTheme, SwitchThemeData? switchTheme, TabBarThemeData? tabBarTheme, TextButtonThemeData? textButtonTheme, TextSelectionThemeData? textSelectionTheme, TimePickerThemeData? timePickerTheme, ToggleButtonsThemeData? toggleButtonsTheme, TooltipThemeData? tooltipTheme, bool? useMaterial3, ButtonBarThemeData? buttonBarTheme, Color? dialogBackgroundColor, Color? indicatorColor})
```

Creates a copy of this theme but with the given fields replaced with the new values.

The [brightness] value is applied to the [colorScheme].

### localize()

```dart
ThemeData localize(ThemeData baseTheme, TextTheme localTextGeometry)
```

Returns a new theme built by merging the text geometry provided by the [localTextGeometry] theme with the [baseTheme].

For those text styles in the [baseTheme] whose [TextStyle.inherit] is set to true, the returned theme's text styles inherit the geometric properties of [localTextGeometry]. The resulting text styles' [TextStyle.inherit] is set to those provided by [localTextGeometry].

### estimateBrightnessForColor()

```dart
Brightness estimateBrightnessForColor(Color color)
```

Determines whether the given [Color] is [Brightness.light] or [Brightness.dark].

This compares the luminosity of the given color to a threshold value that matches the Material Design specification.

### lerp()

```dart
ThemeData lerp(ThemeData a, ThemeData b, double t)
```

Linearly interpolate between two themes.

{@macro dart.ui.shadow.lerp}

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

# MaterialBasedCupertinoThemeData

```dart
class MaterialBasedCupertinoThemeData extends CupertinoThemeData {}
```

A [CupertinoThemeData] that defers unspecified theme attributes to an upstream Material [ThemeData].

This type of [CupertinoThemeData] is used by the Material [Theme] to harmonize the [CupertinoTheme] with the material theme's colors and text styles.

In the most basic case, [ThemeData]'s `cupertinoOverrideTheme` is null and descendant Cupertino widgets' styling is derived from the Material theme.

To override individual parts of the Material-derived Cupertino styling, `cupertinoOverrideTheme`'s construction parameters can be used.

To completely decouple the Cupertino styling from Material theme derivation, another [CupertinoTheme] widget can be inserted as a descendant of the Material [Theme]. On a [MaterialApp], this can be done using the `builder` parameter on the constructor.

See also:

- [CupertinoThemeData], whose null constructor parameters default to reasonable iOS styling defaults rather than harmonizing with a Material theme.
- [Theme], widget which inserts a [CupertinoTheme] with this [MaterialBasedCupertinoThemeData].

### MaterialBasedCupertinoThemeData()

```dart
MaterialBasedCupertinoThemeData({required ThemeData materialTheme})
```

Create a [MaterialBasedCupertinoThemeData] based on a Material [ThemeData] and its `cupertinoOverrideTheme`.

### brightness

```dart
Brightness get brightness
```

### primaryColor

```dart
Color get primaryColor
```

### primaryContrastingColor

```dart
Color get primaryContrastingColor
```

### scaffoldBackgroundColor

```dart
Color get scaffoldBackgroundColor
```

### copyWith()

```dart
MaterialBasedCupertinoThemeData copyWith({Brightness? brightness, Color? primaryColor, Color? primaryContrastingColor, CupertinoTextThemeData? textTheme, Color? barBackgroundColor, Color? scaffoldBackgroundColor, Color? selectionHandleColor, bool? applyThemeToAll})
```

Copies the [ThemeData]'s `cupertinoOverrideTheme`.

Only the specified override attributes of the [ThemeData]'s `cupertinoOverrideTheme` and the newly specified parameters are in the returned [CupertinoThemeData]. No derived attributes from iOS defaults or from cascaded Material theme attributes are copied.

This [copyWith] cannot change the base Material [ThemeData]. To change the base Material [ThemeData], create a new Material [Theme] and use [ThemeData.copyWith] on the Material [ThemeData] instead.

### resolveFrom()

```dart
CupertinoThemeData resolveFrom(BuildContext context)
```

# CupertinoBasedMaterialThemeData

```dart
class CupertinoBasedMaterialThemeData {}
```

A class for creating a Material theme with a color scheme based off of the colors from a [CupertinoThemeData]. This is intended to be used only in the case when a Material widget is unable to find a Material theme in the tree, but is able to find a Cupertino theme. Most often this will occur when a Material widget is used inside of a [CupertinoApp].

Besides the colors, this theme will use all the defaults from Material's [ThemeData], so if further customization is needed, it is best to manually add a Material [Theme] above the [CupertinoApp].

### CupertinoBasedMaterialThemeData()

```dart
CupertinoBasedMaterialThemeData({required CupertinoThemeData themeData})
```

Creates a Material theme with a color scheme based off of the colors from a [CupertinoThemeData].

### materialTheme

```dart
ThemeData materialTheme
```

The Material theme data with colors based on an existing [CupertinoThemeData].

# VisualDensity

```dart
class VisualDensity with Diagnosticable {}
```

Defines the visual density of user interface components.

Density, in the context of a UI, is the vertical and horizontal "compactness" of the components in the UI. It is unitless, since it means different things to different UI components.

The default for visual densities is zero for both vertical and horizontal densities, which corresponds to the default visual density of components in the Material Design specification. It does not affect text sizes, icon sizes, or padding values.

The default visual density varies by platform: mobile platforms (Android, iOS, Fuchsia) use [VisualDensity.standard], while desktop platforms (macOS, Windows, Linux) use [VisualDensity.compact]. See [defaultDensityForPlatform] for more details.

For example, for buttons, it affects the spacing around the child of the button. For lists, it affects the distance between baselines of entries in the list. For chips, it only affects the vertical size, not the horizontal size.

Here are some examples of widgets that respond to density changes:

- [Checkbox]
- [Chip]
- [ElevatedButton]
- [FilledButton]
- [IconButton]
- [InputDecorator] (which gives density support to [TextField], etc.)
- [ListTile]
- [MaterialButton]
- [OutlinedButton]
- [Radio]
- [RawMaterialButton]
- [TextButton]

See also:

- [ThemeData.visualDensity], where this property is used to specify the base horizontal density of Material components.
- [Material design guidance on density](https://material.io/design/layout/applying-density.html).

### VisualDensity()

```dart
VisualDensity({double horizontal = 0.0, double vertical = 0.0})
```

A const constructor for [VisualDensity].

The [horizontal] and [vertical] arguments must be in the interval between [minimumDensity] and [maximumDensity], inclusive.

### minimumDensity

```dart
double minimumDensity
```

The minimum allowed density.

### maximumDensity

```dart
double maximumDensity
```

The maximum allowed density.

### standard

```dart
VisualDensity standard
```

The default profile for [VisualDensity] in [ThemeData].

This default value represents a visual density that is less dense than either [comfortable] or [compact], and corresponds to density values of zero in both axes.

### comfortable

```dart
VisualDensity comfortable
```

The profile for a "comfortable" interpretation of [VisualDensity].

Individual components will interpret the density value independently, making themselves more visually dense than [standard] and less dense than [compact] to different degrees based on the Material Design specification of the "comfortable" setting for their particular use case.

It corresponds to a density value of -1 in both axes.

### compact

```dart
VisualDensity compact
```

The profile for a "compact" interpretation of [VisualDensity].

Individual components will interpret the density value independently, making themselves more visually dense than [standard] and [comfortable] to different degrees based on the Material Design specification of the "comfortable" setting for their particular use case.

It corresponds to a density value of -2 in both axes.

### adaptivePlatformDensity

```dart
VisualDensity get adaptivePlatformDensity
```

Returns a [VisualDensity] that is adaptive based on the current platform on which the framework is executing, from [defaultTargetPlatform].

When [defaultTargetPlatform] is a desktop platform, this returns [compact], and for other platforms, it returns a default-constructed [VisualDensity].

See also:

- [defaultDensityForPlatform] which returns a [VisualDensity] that is adaptive based on the platform given to it.
- [defaultTargetPlatform] which returns the platform on which the framework is currently executing.

### defaultDensityForPlatform()

```dart
VisualDensity defaultDensityForPlatform(TargetPlatform platform)
```

Returns a [VisualDensity] that is adaptive based on the given [platform].

For mobile platforms (Android, iOS, Fuchsia), this returns [VisualDensity.standard], and for desktop platforms (macOS, Windows, Linux), it returns [VisualDensity.compact].

See also:

- [adaptivePlatformDensity] which returns a [VisualDensity] that is adaptive based on [defaultTargetPlatform].

### copyWith()

```dart
VisualDensity copyWith({double? horizontal, double? vertical})
```

Copy the current [VisualDensity] with the given values replacing the current values.

### horizontal

```dart
double horizontal
```

The horizontal visual density of UI components.

This property affects only the horizontal spacing between and within components, to allow for different UI visual densities. It does not affect text sizes, icon sizes, or padding values. The default value is 0.0, corresponding to the metrics specified in the Material Design specification. The value can range from [minimumDensity] to [maximumDensity], inclusive.

See also:

- [ThemeData.visualDensity], where this property is used to specify the base horizontal density of Material components.
- [Material design guidance on density](https://material.io/design/layout/applying-density.html).

### vertical

```dart
double vertical
```

The vertical visual density of UI components.

This property affects only the vertical spacing between and within components, to allow for different UI visual densities. It does not affect text sizes, icon sizes, or padding values. The default value is 0.0, corresponding to the metrics specified in the Material Design specification. The value can range from [minimumDensity] to [maximumDensity], inclusive.

See also:

- [ThemeData.visualDensity], where this property is used to specify the base vertical density of Material components.
- [Material design guidance on density](https://material.io/design/layout/applying-density.html).

### baseSizeAdjustment

```dart
Offset get baseSizeAdjustment
```

The base adjustment in logical pixels of the visual density of UI components.

The input density values are multiplied by a constant to arrive at a base size adjustment that fits Material Design guidelines.

Individual components may adjust this value based upon their own individual interpretation of density.

### lerp()

```dart
VisualDensity lerp(VisualDensity a, VisualDensity b, double t)
```

Linearly interpolate between two densities.

### effectiveConstraints()

```dart
BoxConstraints effectiveConstraints(BoxConstraints constraints)
```

Return a copy of [constraints] whose minimum width and height have been updated with the [baseSizeAdjustment].

The resulting minWidth and minHeight values are clamped to not exceed the maxWidth and maxHeight values, respectively.

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

### toStringShort()

```dart
String toStringShort()
```
