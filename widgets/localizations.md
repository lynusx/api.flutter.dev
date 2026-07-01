@docImport 'package:flutter/material.dart'; @docImport 'package:flutter_localizations/flutter_localizations.dart';

@docImport 'app.dart'; @docImport 'reorderable_list.dart';

# LocalizationsDelegate

```dart
abstract class LocalizationsDelegate<T> {}
```

A factory for a set of localized resources of type `T`, to be loaded by a [Localizations] widget.

Typical applications have one [Localizations] widget which is created by the [WidgetsApp] and configured with the app's `localizationsDelegates` parameter (a list of delegates). The delegate's [type] is used to identify the object created by an individual delegate's [load] method.

An example of a class used as the value of `T` here would be [MaterialLocalizations].

### LocalizationsDelegate()

```dart
LocalizationsDelegate()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### isSupported()

```dart
bool isSupported(Locale locale)
```

Whether resources for the given locale can be loaded by this delegate.

Return true if the instance of `T` loaded by this delegate's [load] method supports the given `locale`'s language.

### load()

```dart
Future<T> load(Locale locale)
```

Start loading the resources for `locale`. The returned future completes when the resources have finished loading.

It's assumed that this method will return an object that contains a collection of related string resources (typically defined with one method per resource). The object will be retrieved with [Localizations.of].

### shouldReload()

```dart
bool shouldReload(LocalizationsDelegate<T> old)
```

Returns true if the resources for this delegate should be loaded again by calling the [load] method.

This method is called whenever its [Localizations] widget is rebuilt. If it returns true then dependent widgets will be rebuilt after [load] has completed.

### type

```dart
Type get type
```

The type of the object returned by the [load] method, T by default.

This type is used to retrieve the object "loaded" by this [LocalizationsDelegate] from the [Localizations] inherited widget. For example the object loaded by `LocalizationsDelegate<Foo>` would be retrieved with:

```dart
Foo foo = Localizations.of<Foo>(context, Foo)!;
```

It's rarely necessary to override this getter.

### toString()

```dart
String toString()
```

# WidgetsLocalizations

```dart
abstract class WidgetsLocalizations {}
```

Interface for localized resource values for the lowest levels of the Flutter framework.

This class also maps locales to a specific [Directionality] using the [textDirection] property.

See also:

- [DefaultWidgetsLocalizations], which implements this interface and supports a variety of locales.

### textDirection

```dart
TextDirection get textDirection
```

The reading direction for text in this locale.

### reorderItemToStart

```dart
String get reorderItemToStart
```

The semantics label used for [SliverReorderableList] to reorder an item in the list to the start of the list.

### reorderItemToEnd

```dart
String get reorderItemToEnd
```

The semantics label used for [SliverReorderableList] to reorder an item in the list to the end of the list.

### reorderItemUp

```dart
String get reorderItemUp
```

The semantics label used for [SliverReorderableList] to reorder an item in the list one space up the list.

### reorderItemDown

```dart
String get reorderItemDown
```

The semantics label used for [SliverReorderableList] to reorder an item in the list one space down the list.

### reorderItemLeft

```dart
String get reorderItemLeft
```

The semantics label used for [SliverReorderableList] to reorder an item in the list one space left in the list.

### reorderItemRight

```dart
String get reorderItemRight
```

The semantics label used for [SliverReorderableList] to reorder an item in the list one space right in the list.

### searchResultsFound

```dart
String get searchResultsFound
```

The semantics label used for [RawAutocomplete] when the options list goes from empty to non-empty.

### noResultsFound

```dart
String get noResultsFound
```

The semantics label used for [RawAutocomplete] when the options list goes from non-empty to empty.

### copyButtonLabel

```dart
String get copyButtonLabel
```

Label for "copy" edit buttons and menu items.

### cutButtonLabel

```dart
String get cutButtonLabel
```

Label for "cut" edit buttons and menu items.

### pasteButtonLabel

```dart
String get pasteButtonLabel
```

Label for "paste" edit buttons and menu items.

### selectAllButtonLabel

```dart
String get selectAllButtonLabel
```

Label for "select all" edit buttons and menu items.

### lookUpButtonLabel

```dart
String get lookUpButtonLabel
```

Label for "look up" edit buttons and menu items.

### searchWebButtonLabel

```dart
String get searchWebButtonLabel
```

Label for "search web" edit buttons and menu items.

### shareButtonLabel

```dart
String get shareButtonLabel
```

Label for "share" edit buttons and menu items.

### radioButtonUnselectedLabel

```dart
String get radioButtonUnselectedLabel
```

The accessibility hint for an unselected radio button.

### of()

```dart
WidgetsLocalizations of(BuildContext context)
```

The `WidgetsLocalizations` from the closest [Localizations] instance that encloses the given context.

This method is just a convenient shorthand for: `Localizations.of<WidgetsLocalizations>(context, WidgetsLocalizations)!`.

References to the localized resources defined by this class are typically written in terms of this method. For example:

```dart
textDirection: WidgetsLocalizations.of(context).textDirection,
```

# DefaultWidgetsLocalizations

```dart
class DefaultWidgetsLocalizations implements WidgetsLocalizations {}
```

US English localizations for the widgets library.

See also:

- [GlobalWidgetsLocalizations], which provides widgets localizations for many languages.
- [WidgetsApp.localizationsDelegates], which automatically includes [DefaultWidgetsLocalizations.delegate] by default.

### DefaultWidgetsLocalizations()

```dart
DefaultWidgetsLocalizations()
```

Construct an object that defines the localized values for the widgets library for US English (only).

[LocalizationsDelegate] implementations typically call the static [load]

### reorderItemUp

```dart
String get reorderItemUp
```

### reorderItemDown

```dart
String get reorderItemDown
```

### reorderItemLeft

```dart
String get reorderItemLeft
```

### reorderItemRight

```dart
String get reorderItemRight
```

### reorderItemToEnd

```dart
String get reorderItemToEnd
```

### reorderItemToStart

```dart
String get reorderItemToStart
```

### searchResultsFound

```dart
String get searchResultsFound
```

### noResultsFound

```dart
String get noResultsFound
```

### copyButtonLabel

```dart
String get copyButtonLabel
```

### cutButtonLabel

```dart
String get cutButtonLabel
```

### pasteButtonLabel

```dart
String get pasteButtonLabel
```

### selectAllButtonLabel

```dart
String get selectAllButtonLabel
```

### lookUpButtonLabel

```dart
String get lookUpButtonLabel
```

### searchWebButtonLabel

```dart
String get searchWebButtonLabel
```

### shareButtonLabel

```dart
String get shareButtonLabel
```

### radioButtonUnselectedLabel

```dart
String get radioButtonUnselectedLabel
```

### textDirection

```dart
TextDirection get textDirection
```

### load()

```dart
Future<WidgetsLocalizations> load(Locale locale)
```

Creates an object that provides US English resource values for the lowest levels of the widgets library.

The [locale] parameter is ignored.

This method is typically used to create a [LocalizationsDelegate]. The [WidgetsApp] does so by default.

### delegate

```dart
LocalizationsDelegate<WidgetsLocalizations> delegate
```

A [LocalizationsDelegate] that uses [DefaultWidgetsLocalizations.load] to create an instance of this class.

[WidgetsApp] automatically adds this value to [WidgetsApp.localizationsDelegates].

# Localizations

```dart
class Localizations extends StatefulWidget {}
```

Defines the [Locale] for its `child` and the localized resources that the child depends on.

## Defining localized resources

{@tool snippet}

This following class is defined in terms of the [Dart `intl` package](https://github.com/dart-lang/i18n/tree/main/pkgs/intl). Using the `intl` package isn't required.

```dart
class MyLocalizations {
  MyLocalizations(this.locale);

  final Locale locale;

  static Future<MyLocalizations> load(Locale locale) {
    return initializeMessages(locale.toString())
      .then((void _) {
        return MyLocalizations(locale);
      });
  }

  static MyLocalizations of(BuildContext context) {
    return Localizations.of<MyLocalizations>(context, MyLocalizations)!;
  }

  String title() => Intl.message('<title>', name: 'title', locale: locale.toString());
  // ... more Intl.message() methods like title()
}
```

{@end-tool} A class based on the `intl` package imports a generated message catalog that provides the `initializeMessages()` function and the per-locale backing store for `Intl.message()`. The message catalog is produced by an `intl` tool that analyzes the source code for classes that contain `Intl.message()` calls. In this case that would just be the `MyLocalizations` class.

One could choose another approach for loading localized resources and looking them up while still conforming to the structure of this example.

## Loading localized resources

Localized resources are loaded by the list of [LocalizationsDelegate] `delegates`. Each delegate is essentially a factory for a collection of localized resources. There are multiple delegates because there are multiple sources for localizations within an app.

Delegates are typically simple subclasses of [LocalizationsDelegate] that override [LocalizationsDelegate.load]. For example a delegate for the `MyLocalizations` class defined above would be:

```dart
// continuing from previous example...
class _MyDelegate extends LocalizationsDelegate<MyLocalizations> {
  @override
  Future<MyLocalizations> load(Locale locale) => MyLocalizations.load(locale);

  @override
  bool isSupported(Locale locale) {
    // in a real implementation this would only return true for
    // locales that are definitely supported.
    return true;
  }

  @override
  bool shouldReload(_MyDelegate old) => false;
}
```

Each delegate can be viewed as a factory for objects that encapsulate a set of localized resources. These objects are retrieved with by runtime type with [Localizations.of].

The [WidgetsApp] class creates a [Localizations] widget so most apps will not need to create one. The widget app's [Localizations] delegates can be initialized with [WidgetsApp.localizationsDelegates]. The [MaterialApp] class also provides a `localizationsDelegates` parameter that's just passed along to the [WidgetsApp].

## Obtaining localized resources for use in user interfaces

Apps should retrieve collections of localized resources with `Localizations.of<MyLocalizations>(context, MyLocalizations)`, where MyLocalizations is an app specific class defines one function per resource. This is conventionally done by a static `.of` method on the custom localized resource class (`MyLocalizations` in the example above).

For example, using the `MyLocalizations` class defined above, one would lookup a localized title string like this:

```dart
// continuing from previous example...
MyLocalizations.of(context).title()
```

If [Localizations] were to be rebuilt with a new `locale` then the widget subtree that corresponds to [BuildContext] `context` would be rebuilt after the corresponding resources had been loaded.

This class is effectively an [InheritedWidget]. If it's rebuilt with a new `locale` or a different list of delegates or any of its delegates' [LocalizationsDelegate.shouldReload()] methods returns true, then widgets that have created a dependency by calling `Localizations.of(context)` will be rebuilt after the resources for the new locale have been loaded.

The [Localizations] widget also instantiates [Directionality] in order to support the appropriate [Directionality.textDirection] of the localized resources.

### Localizations()

```dart
Localizations({dynamic key, required Locale locale, required List<LocalizationsDelegate<dynamic>> delegates, Widget? child, bool isApplicationLevel = false})
```

Create a widget from which localizations (like translated strings) can be obtained.

### Localizations.override()

```dart
Localizations.override({Key? key, required BuildContext context, Locale? locale, List<LocalizationsDelegate<dynamic>>? delegates, Widget? child})
```

Overrides the inherited [Locale] or [LocalizationsDelegate]s for `child`.

This factory constructor is used for the (usually rare) situation where part of an app should be localized for a different locale than the one defined for the device, or if its localizations should come from a different list of [LocalizationsDelegate]s than the list defined by [WidgetsApp.localizationsDelegates].

For example you could specify that `myWidget` was only to be localized for the US English locale:

```dart
Widget build(BuildContext context) {
  return Localizations.override(
    context: context,
    locale: const Locale('en', 'US'),
    child: myWidget,
  );
}
```

The `locale` and `delegates` parameters default to the [Localizations.locale] and [Localizations.delegates] values from the nearest [Localizations] ancestor.

To override the [Localizations.locale] or [Localizations.delegates] for an entire app, specify [WidgetsApp.locale] or [WidgetsApp.localizationsDelegates] (or specify the same parameters for [MaterialApp]).

### locale

```dart
Locale locale
```

The resources returned by [Localizations.of] will be specific to this locale.

### delegates

```dart
List<LocalizationsDelegate<dynamic>> delegates
```

This list collectively defines the localized resources objects that can be retrieved with [Localizations.of].

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### isApplicationLevel

```dart
bool isApplicationLevel
```

Whether this is the main localizations widget that represents the app's locale.

### localeOf()

```dart
Locale localeOf(BuildContext context)
```

The locale of the Localizations widget for the widget tree that corresponds to [BuildContext] `context`.

If no [Localizations] widget is in scope then the [Localizations.localeOf] method will throw an exception.

### maybeLocaleOf()

```dart
Locale? maybeLocaleOf(BuildContext context)
```

The locale of the Localizations widget for the widget tree that corresponds to [BuildContext] `context`.

If no [Localizations] widget is in scope then this function will return null.

### of()

```dart
T? of<T>(BuildContext context, Type type)
```

Returns the localized resources object of the given `type` for the widget tree that corresponds to the given `context`.

Returns null if no resources object of the given `type` exists within the given `context`.

This method is typically used by a static factory method on the `type` class. For example Flutter's MaterialLocalizations class looks up Material resources with a method defined like this:

```dart
static MaterialLocalizations of(BuildContext context) {
  return Localizations.of<MaterialLocalizations>(context, MaterialLocalizations)!;
}
```

### createState()

```dart
State<Localizations> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# LocalizationsResolver

```dart
class LocalizationsResolver extends ChangeNotifier with WidgetsBindingObserver {}
```

A helper class used to manage localization resolution.

See also:

- [WidgetsApp], which utilizes [LocalizationsResolver] to handle locales.

### LocalizationsResolver()

```dart
LocalizationsResolver({required Iterable<Locale> supportedLocales, Locale? locale, LocaleListResolutionCallback? localeListResolutionCallback, LocaleResolutionCallback? localeResolutionCallback, Iterable<LocalizationsDelegate<Object?>>? localizationsDelegates})
```

Creates a [LocalizationsResolver] that determines the best-fit locale from the set of [supportedLocales].

If provided, locale resolution will attempt to use [locale] as the current locale rather than the system locale.

Locale resolution behavior can be overridden by providing [localeListResolutionCallback] or [localeResolutionCallback].

The delegates set via [localizationsDelegates] collectively define all of the localized resources for a [Localizations] widget.

See also:

- [LocalizationsResolver.localeListResolutionCallback] and [LocalizationsResolver.localeResolutionCallback] for more details on locale resolution behavior.
- [LocalizationsDelegate] for more details about providing localized resources to a [Localizations] widget.

### dispose()

```dart
void dispose()
```

### update()

```dart
void update({required Locale? locale, required LocaleListResolutionCallback? localeListResolutionCallback, required LocaleResolutionCallback? localeResolutionCallback, required Iterable<LocalizationsDelegate<Object?>>? localizationsDelegates, required Iterable<Locale> supportedLocales})
```

Replace one or more of the properties used for localization resolution and re-resolve the locale.

### locale

```dart
Locale get locale
```

The currently resolved [Locale] based on the current platform locale and the provided set of [supportedLocales].

### localizationsDelegates

```dart
Iterable<LocalizationsDelegate<Object?>> get localizationsDelegates
```

{@macro flutter.widgets.widgetsApp.localizationsDelegates}

### localeListResolutionCallback

```dart
LocaleListResolutionCallback? get localeListResolutionCallback
```

{@macro flutter.widgets.widgetsApp.localeListResolutionCallback}

See also:

- [basicLocaleListResolution], the default locale resolution algorithm.

### localeResolutionCallback

```dart
LocaleResolutionCallback? get localeResolutionCallback
```

{@macro flutter.widgets.LocaleResolutionCallback}

### supportedLocales

```dart
Iterable<Locale> get supportedLocales
```

{@macro flutter.widgets.widgetsApp.supportedLocales}

See also:

- [localeResolutionCallback], an app callback that resolves the app's locale when the device's locale changes.
- [localizationsDelegates], which collectively define all of the localized resources used by this app.
- [basicLocaleListResolution], the default locale resolution algorithm.

### didChangeLocales()

```dart
void didChangeLocales(List<Locale>? locales)
```

### toString()

```dart
String toString()
```
