@docImport 'package:flutter/material.dart';

# AutocompleteOptionsBuilder

```dart
typedef AutocompleteOptionsBuilder<T extends Object> = FutureOr<Iterable<T>> Function(TextEditingValue textEditingValue)
```

The type of the [RawAutocomplete] callback which computes the list of optional completions for the widget's field, based on the text the user has entered so far.

See also:

- [RawAutocomplete.optionsBuilder], which is of this type.

# AutocompleteOnSelected

```dart
typedef AutocompleteOnSelected<T extends Object> = void Function(T option)
```

The type of the callback used by the [RawAutocomplete] widget to indicate that the user has selected an option.

See also:

- [RawAutocomplete.onSelected], which is of this type.

# AutocompleteOptionsViewBuilder

```dart
typedef AutocompleteOptionsViewBuilder<T extends Object> = Widget Function(BuildContext context, AutocompleteOnSelected<T> onSelected, Iterable<T> options)
```

The type of the [RawAutocomplete] callback which returns a [Widget] that displays the specified [options] and calls [onSelected] if the user selects an option.

The returned widget from this callback will be wrapped in an [AutocompleteHighlightedOption] inherited widget. This will allow this callback to determine which option is currently highlighted for keyboard navigation.

See also:

- [RawAutocomplete.optionsViewBuilder], which is of this type.

# AutocompleteFieldViewBuilder

```dart
typedef AutocompleteFieldViewBuilder = Widget Function(BuildContext context, TextEditingController textEditingController, FocusNode focusNode, VoidCallback onFieldSubmitted)
```

The type of the Autocomplete callback which returns the widget that contains the input [TextField] or [TextFormField].

See also:

- [RawAutocomplete.fieldViewBuilder], which is of this type.

# AutocompleteOptionToString

```dart
typedef AutocompleteOptionToString<T extends Object> = String Function(T option)
```

The type of the [RawAutocomplete] callback that converts an option value to a string which can be displayed in the widget's options menu.

See also:

- [RawAutocomplete.displayStringForOption], which is of this type.

# OptionsViewOpenDirection

```dart
enum OptionsViewOpenDirection {}
```

A direction in which to open the options-view overlay.

See also:

- [RawAutocomplete.optionsViewOpenDirection], which is of this type.
- [RawAutocomplete.optionsViewBuilder] to specify how to build the selectable-options widget.
- [RawAutocomplete.fieldViewBuilder] to optionally specify how to build the corresponding field widget.

Open upward.

The bottom edge of the options view will align with the top edge of the text field built by [RawAutocomplete.fieldViewBuilder].

Open downward.

The top edge of the options view will align with the bottom edge of the text field built by [RawAutocomplete.fieldViewBuilder].

Open in the direction with the most available space within the overlay.

The available space is calculated as the distance from the field's top edge to the overlay's top edge (for upward opening) or from the field's bottom edge to the overlay's bottom edge (for downward opening).

If both directions have the same available space, the options view opens downward.

# RawAutocomplete

```dart
class RawAutocomplete<T extends Object> extends StatefulWidget {}
```

{@template flutter.widgets.RawAutocomplete.RawAutocomplete} A widget for helping the user make a selection by entering some text and choosing from among a list of options.

The user's text input is received in a field built with the [fieldViewBuilder] parameter. The options to be displayed are determined using [optionsBuilder] and rendered with [optionsViewBuilder].

The options view opens when the field gains focus or when the field's text changes, as long as [optionsBuilder] returns at least one option. The options view closes when the user selects an option, when there are no matching options, or when the field loses focus. {@endtemplate}

This is a core framework widget with very basic UI.

{@tool dartpad} This example shows how to create a very basic autocomplete widget using the [fieldViewBuilder] and [optionsViewBuilder] parameters.

** See code in examples/api/lib/widgets/autocomplete/raw_autocomplete.0.dart ** {@end-tool}

The type parameter T represents the type of the options. Most commonly this is a String, as in the example above. However, it's also possible to use another type with a `toString` method, or a custom [displayStringForOption]. Options will be compared using `==`, so it may be beneficial to override [Object.==] and [Object.hashCode] for custom types.

{@tool dartpad} This example is similar to the previous example, but it uses a custom T data type instead of directly using String.

** See code in examples/api/lib/widgets/autocomplete/raw_autocomplete.1.dart ** {@end-tool}

{@tool dartpad} This example shows the use of RawAutocomplete in a form.

** See code in examples/api/lib/widgets/autocomplete/raw_autocomplete.2.dart ** {@end-tool}

See also:

- [Autocomplete], which is a Material-styled implementation that is based on RawAutocomplete.

### RawAutocomplete()

```dart
RawAutocomplete({dynamic key, required AutocompleteOptionsViewBuilder<T> optionsViewBuilder, required AutocompleteOptionsBuilder<T> optionsBuilder, OptionsViewOpenDirection optionsViewOpenDirection = OptionsViewOpenDirection.down, AutocompleteOptionToString<T> displayStringForOption = defaultStringForOption, AutocompleteFieldViewBuilder? fieldViewBuilder, FocusNode? focusNode, AutocompleteOnSelected<T>? onSelected, TextEditingController? textEditingController, TextEditingValue? initialValue})
```

Create an instance of RawAutocomplete.

[displayStringForOption], [optionsBuilder] and [optionsViewBuilder] must not be null.

### fieldViewBuilder

```dart
AutocompleteFieldViewBuilder? fieldViewBuilder
```

{@template flutter.widgets.RawAutocomplete.fieldViewBuilder} Builds the field whose input is used to get the options.

Pass the provided [TextEditingController] to the field built here so that RawAutocomplete can listen for changes. {@endtemplate}

If this parameter is null, then a [SizedBox.shrink] is built instead. For how that pattern can be useful, see [textEditingController].

### focusNode

```dart
FocusNode? focusNode
```

The [FocusNode] that is used for the text field.

{@template flutter.widgets.RawAutocomplete.split} The main purpose of this parameter is to allow the use of a separate text field located in another part of the widget tree instead of the text field built by [fieldViewBuilder]. For example, it may be desirable to place the text field in the AppBar and the options below in the main body.

When following this pattern, [fieldViewBuilder] can be omitted, so that a text field is not drawn where it would normally be. A separate text field can be created elsewhere, and a FocusNode and TextEditingController can be passed both to that text field and to RawAutocomplete.

{@tool dartpad} This examples shows how to create an autocomplete widget with the text field in the AppBar and the results in the main body of the app.

** See code in examples/api/lib/widgets/autocomplete/raw_autocomplete.focus_node.0.dart ** {@end-tool} {@endtemplate}

If this parameter is not null, then [textEditingController] must also be non-null.

### optionsViewBuilder

```dart
AutocompleteOptionsViewBuilder<T> optionsViewBuilder
```

{@template flutter.widgets.RawAutocomplete.optionsViewBuilder} Builds the selectable options widgets from a list of options objects.

The options are displayed floating below or above the field inside of an [Overlay], not at the same place in the widget tree as [RawAutocomplete]. To control whether it opens upward or downward, use [optionsViewOpenDirection].

In order to track which item is highlighted by keyboard navigation, the resulting options will be wrapped in an inherited [AutocompleteHighlightedOption] widget. Inside this callback, the index of the highlighted option can be obtained from [AutocompleteHighlightedOption.of] to display the highlighted option with a visual highlight to indicate it will be the option selected from the keyboard.

{@endtemplate}

### optionsViewOpenDirection

```dart
OptionsViewOpenDirection optionsViewOpenDirection
```

{@template flutter.widgets.RawAutocomplete.optionsViewOpenDirection} Determines the direction in which to open the options view.

Defaults to [OptionsViewOpenDirection.down]. {@endtemplate}

### displayStringForOption

```dart
AutocompleteOptionToString<T> displayStringForOption
```

{@template flutter.widgets.RawAutocomplete.displayStringForOption} Returns the string to display in the field when the option is selected.

This is useful when using a custom T type and the string to display is different than the string to search by.

If not provided, will use `option.toString()`. {@endtemplate}

### onSelected

```dart
AutocompleteOnSelected<T>? onSelected
```

{@template flutter.widgets.RawAutocomplete.onSelected} Called when an option is selected by the user. {@endtemplate}

### optionsBuilder

```dart
AutocompleteOptionsBuilder<T> optionsBuilder
```

{@template flutter.widgets.RawAutocomplete.optionsBuilder} A function that returns the current selectable options objects given the current TextEditingValue. {@endtemplate}

### textEditingController

```dart
TextEditingController? textEditingController
```

The [TextEditingController] that is used for the text field.

{@macro flutter.widgets.RawAutocomplete.split}

If this parameter is not null, then [focusNode] must also be non-null.

### initialValue

```dart
TextEditingValue? initialValue
```

{@template flutter.widgets.RawAutocomplete.initialValue} The initial value to use for the text field. {@endtemplate}

Setting the initial value does not notify [textEditingController]'s listeners, and thus will not cause the options UI to appear.

This parameter is ignored if [textEditingController] is defined.

### onFieldSubmitted()

```dart
void onFieldSubmitted<T extends Object>(GlobalKey key)
```

Calls [AutocompleteFieldViewBuilder]'s onFieldSubmitted callback for the RawAutocomplete widget indicated by the given [GlobalKey].

This is not typically used unless a custom field is implemented instead of using [fieldViewBuilder]. In the typical case, the onFieldSubmitted callback is passed via the [AutocompleteFieldViewBuilder] signature. When not using fieldViewBuilder, the same callback can be called by using this static method.

See also:

- [focusNode] and [textEditingController], which contain a code example showing how to create a separate field outside of fieldViewBuilder.

### defaultStringForOption()

```dart
String defaultStringForOption(Object? option)
```

The default way to convert an option to a string in [displayStringForOption].

Uses the `toString` method of the given `option`.

### createState()

```dart
State<RawAutocomplete<T>> createState()
```

# AutocompletePreviousOptionIntent

```dart
class AutocompletePreviousOptionIntent extends Intent {}
```

An [Intent] to highlight the previous option in the autocomplete list.

### AutocompletePreviousOptionIntent()

```dart
AutocompletePreviousOptionIntent()
```

Creates an instance of AutocompletePreviousOptionIntent.

# AutocompleteNextOptionIntent

```dart
class AutocompleteNextOptionIntent extends Intent {}
```

An [Intent] to highlight the next option in the autocomplete list.

### AutocompleteNextOptionIntent()

```dart
AutocompleteNextOptionIntent()
```

Creates an instance of AutocompleteNextOptionIntent.

# AutocompleteFirstOptionIntent

```dart
class AutocompleteFirstOptionIntent extends Intent {}
```

An [Intent] to highlight the first option in the autocomplete list.

### AutocompleteFirstOptionIntent()

```dart
AutocompleteFirstOptionIntent()
```

Creates an instance of AutocompleteFirstOptionIntent.

# AutocompleteLastOptionIntent

```dart
class AutocompleteLastOptionIntent extends Intent {}
```

An [Intent] to highlight the last option in the autocomplete list.

### AutocompleteLastOptionIntent()

```dart
AutocompleteLastOptionIntent()
```

Creates an instance of AutocompleteLastOptionIntent.

# AutocompleteNextPageOptionIntent

```dart
class AutocompleteNextPageOptionIntent extends Intent {}
```

An [Intent] to highlight the option one page after the currently highlighted option in the autocomplete list.

### AutocompleteNextPageOptionIntent()

```dart
AutocompleteNextPageOptionIntent()
```

Creates an instance of AutocompleteNextPageOptionIntent.

# AutocompletePreviousPageOptionIntent

```dart
class AutocompletePreviousPageOptionIntent extends Intent {}
```

An [Intent] to highlight the option one page before the currently highlighted option in the autocomplete list.

### AutocompletePreviousPageOptionIntent()

```dart
AutocompletePreviousPageOptionIntent()
```

Creates an instance of AutocompletePreviousPageOptionIntent.

# AutocompleteHighlightedOption

```dart
class AutocompleteHighlightedOption extends InheritedNotifier<ValueNotifier<int>> {}
```

An inherited widget used to indicate which autocomplete option should be highlighted for keyboard navigation.

The `RawAutocomplete` widget will wrap the options view generated by the `optionsViewBuilder` with this widget to provide the highlighted option's index to the builder.

In the builder callback the index of the highlighted option can be obtained by using the static [of] method:

```dart
int highlightedIndex = AutocompleteHighlightedOption.of(context);
```

which can then be used to tell which option should be given a visual indication that will be the option selected with the keyboard.

### AutocompleteHighlightedOption()

```dart
AutocompleteHighlightedOption({dynamic key, required ValueNotifier<int> highlightIndexNotifier, required Widget child})
```

Create an instance of AutocompleteHighlightedOption inherited widget.

### of()

```dart
int of(BuildContext context)
```

Returns the index of the highlighted option from the closest [AutocompleteHighlightedOption] ancestor.

If there is no ancestor, it returns 0.

Typical usage is as follows:

```dart
int highlightedIndex = AutocompleteHighlightedOption.of(context);
```
