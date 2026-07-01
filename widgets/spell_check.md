@docImport 'editable_text.dart';

# SpellCheckConfiguration

```dart
class SpellCheckConfiguration {}
```

Controls how spell check is performed for text input.

This configuration determines the [SpellCheckService] used to fetch the [List<SuggestionSpan>] spell check results and the [TextStyle] used to mark misspelled words within text input.

### SpellCheckConfiguration()

```dart
SpellCheckConfiguration({SpellCheckService? spellCheckService, Color? misspelledSelectionColor, TextStyle? misspelledTextStyle, EditableTextContextMenuBuilder? spellCheckSuggestionsToolbarBuilder})
```

Creates a configuration that specifies the service and suggestions handler for spell check.

### SpellCheckConfiguration.disabled()

```dart
SpellCheckConfiguration.disabled()
```

Creates a configuration that disables spell check.

### spellCheckService

```dart
SpellCheckService? spellCheckService
```

The service used to fetch spell check results for text input.

### misspelledSelectionColor

```dart
Color? misspelledSelectionColor
```

The color the paint the selection highlight when spell check is showing suggestions for a misspelled word.

For example, on iOS, the selection appears red while the spell check menu is showing.

### misspelledTextStyle

```dart
TextStyle? misspelledTextStyle
```

Style used to indicate misspelled words.

This is nullable to allow style-specific wrappers of [EditableText] to infer this, but this must be specified if this configuration is provided directly to [EditableText] or its construction will fail with an assertion error.

### spellCheckSuggestionsToolbarBuilder

```dart
EditableTextContextMenuBuilder? spellCheckSuggestionsToolbarBuilder
```

Builds the toolbar used to display spell check suggestions for misspelled words.

### spellCheckEnabled

```dart
bool get spellCheckEnabled
```

Whether or not the configuration should enable or disable spell check.

### copyWith()

```dart
SpellCheckConfiguration copyWith({SpellCheckService? spellCheckService, Color? misspelledSelectionColor, TextStyle? misspelledTextStyle, EditableTextContextMenuBuilder? spellCheckSuggestionsToolbarBuilder})
```

Returns a copy of the current [SpellCheckConfiguration] instance with specified overrides.

### toString()

```dart
String toString()
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# buildTextSpanWithSpellCheckSuggestions()

```dart
TextSpan buildTextSpanWithSpellCheckSuggestions(TextEditingValue value, bool composingWithinCurrentTextRange, TextStyle? style, TextStyle misspelledTextStyle, SpellCheckResults spellCheckResults)
```

Builds the [TextSpan] tree given the current state of the text input and spell check results.

The [value] is the current [TextEditingValue] requested to be rendered by a text input widget. The [composingWithinCurrentTextRange] value represents whether or not there is a valid composing region in the [value]. The [style] is the [TextStyle] to render the [value]'s text with, and the [misspelledTextStyle] is the [TextStyle] to render misspelled words within the [value]'s text with. The [spellCheckResults] are the results of spell checking the [value]'s text.
