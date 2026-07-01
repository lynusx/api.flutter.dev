# Autocomplete

```dart
class Autocomplete<T extends Object> extends StatelessWidget {}
```

{@macro flutter.widgets.RawAutocomplete.RawAutocomplete}

{@youtube 560 315 https://www.youtube.com/watch?v=-Nny8kzW380}

{@tool dartpad} This example shows how to create a very basic Autocomplete widget using the default UI.

** See code in examples/api/lib/material/autocomplete/autocomplete.0.dart ** {@end-tool}

{@tool dartpad} This example shows how to create an Autocomplete widget with a custom type. Try searching with text from the name or email field.

** See code in examples/api/lib/material/autocomplete/autocomplete.1.dart ** {@end-tool}

{@tool dartpad} This example shows how to create an Autocomplete widget whose options are fetched over the network.

** See code in examples/api/lib/material/autocomplete/autocomplete.2.dart ** {@end-tool}

{@tool dartpad} This example shows how to create an Autocomplete widget whose options are fetched over the network. It uses debouncing to wait to perform the network request until after the user finishes typing.

** See code in examples/api/lib/material/autocomplete/autocomplete.3.dart ** {@end-tool}

{@tool dartpad} This example shows how to create an Autocomplete widget whose options are fetched over the network. It includes both debouncing and error handling, so that failed network requests show an error to the user and can be recovered from. Try toggling the network Switch widget to simulate going offline.

** See code in examples/api/lib/material/autocomplete/autocomplete.4.dart ** {@end-tool}

See also:

- [RawAutocomplete], which is what Autocomplete is built upon, and which contains more detailed examples.

### Autocomplete()

```dart
Autocomplete({dynamic key, required AutocompleteOptionsBuilder<T> optionsBuilder, AutocompleteOptionToString<T> displayStringForOption = RawAutocomplete.defaultStringForOption, AutocompleteFieldViewBuilder fieldViewBuilder = _defaultFieldViewBuilder, FocusNode? focusNode, AutocompleteOnSelected<T>? onSelected, double optionsMaxHeight = 200.0, AutocompleteOptionsViewBuilder<T>? optionsViewBuilder, OptionsViewOpenDirection optionsViewOpenDirection = OptionsViewOpenDirection.down, TextEditingController? textEditingController, TextEditingValue? initialValue})
```

Creates an instance of [Autocomplete].

### displayStringForOption

```dart
AutocompleteOptionToString<T> displayStringForOption
```

{@macro flutter.widgets.RawAutocomplete.displayStringForOption}

### fieldViewBuilder

```dart
AutocompleteFieldViewBuilder fieldViewBuilder
```

{@macro flutter.widgets.RawAutocomplete.fieldViewBuilder}

If not provided, will build a standard Material-style text field by default.

### focusNode

```dart
FocusNode? focusNode
```

The [FocusNode] that is used for the text field.

{@macro flutter.widgets.RawAutocomplete.split}

If this parameter is not null, then [textEditingController] must also be non-null.

### onSelected

```dart
AutocompleteOnSelected<T>? onSelected
```

{@macro flutter.widgets.RawAutocomplete.onSelected}

### optionsBuilder

```dart
AutocompleteOptionsBuilder<T> optionsBuilder
```

{@macro flutter.widgets.RawAutocomplete.optionsBuilder}

### optionsViewBuilder

```dart
AutocompleteOptionsViewBuilder<T>? optionsViewBuilder
```

{@macro flutter.widgets.RawAutocomplete.optionsViewBuilder}

If not provided, will build a standard Material-style list of results by default.

### optionsViewOpenDirection

```dart
OptionsViewOpenDirection optionsViewOpenDirection
```

{@macro flutter.widgets.RawAutocomplete.optionsViewOpenDirection}

### optionsMaxHeight

```dart
double optionsMaxHeight
```

The maximum height used for the default Material options list widget.

When [optionsViewBuilder] is `null`, this property sets the maximum height that the options widget can occupy.

The default value is set to 200.

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

{@macro flutter.widgets.RawAutocomplete.initialValue}

### build()

```dart
Widget build(BuildContext context)
```
