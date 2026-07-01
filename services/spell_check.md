@docImport 'package:flutter/widgets.dart';

# SuggestionSpan

```dart
class SuggestionSpan {}
```

A data structure representing a range of misspelled text and the suggested replacements for this range.

For example, one [SuggestionSpan] of the [List<SuggestionSpan>] suggestions of the [SpellCheckResults] corresponding to "Hello, wrold!" may be:

```dart
SuggestionSpan suggestionSpan =
  const SuggestionSpan(
    TextRange(start: 7, end: 12),
    <String>['word', 'world', 'old'],
);
```

### SuggestionSpan()

```dart
SuggestionSpan(TextRange range, List<String> suggestions)
```

Creates a span representing a misspelled range of text and the replacements suggested by a spell checker.

The [range] and replacement [suggestions] must all not be null.

### range

```dart
TextRange range
```

The misspelled range of text.

### suggestions

```dart
List<String> suggestions
```

The alternate suggestions for the misspelled range of text.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# SpellCheckResults

```dart
class SpellCheckResults {}
```

A data structure grouping together the [SuggestionSpan]s and related text of results returned by a spell checker.

### SpellCheckResults()

```dart
SpellCheckResults(String spellCheckedText, List<SuggestionSpan> suggestionSpans)
```

Creates results based off those received by spell checking some text input.

### spellCheckedText

```dart
String spellCheckedText
```

The text that the [suggestionSpans] correspond to.

### suggestionSpans

```dart
List<SuggestionSpan> suggestionSpans
```

The spell check results of the [spellCheckedText].

See also:

- [SuggestionSpan], the ranges of misspelled text and corresponding replacement suggestions.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# SpellCheckService

```dart
abstract class SpellCheckService {}
```

Determines how spell check results are received for text input.

### fetchSpellCheckSuggestions()

```dart
Future<List<SuggestionSpan>?> fetchSpellCheckSuggestions(Locale locale, String text)
```

Facilitates a spell check request.

Returns a [Future] that resolves with a [List] of [SuggestionSpan]s for all misspelled words in the given [String] for the given [Locale].

A return value that resolves to null indicates that fetching the spell check suggestions was unsuccessful. If fetching the suggestions succeeded but none were found, the [Future] should resolve to an empty list.

# DefaultSpellCheckService

```dart
class DefaultSpellCheckService implements SpellCheckService {}
```

The service used by default to fetch spell check results for text input.

Any widget may use this service to spell check text by calling `fetchSpellCheckSuggestions(locale, text)` with an instance of this class. This is currently only supported by Android and iOS.

See also:

- [SpellCheckService], the service that this implements that may be overridden for use by [EditableText].
- [EditableText], which may use this service to fetch results.

### DefaultSpellCheckService()

```dart
DefaultSpellCheckService()
```

Creates service to spell check text input by default via communication over the spell check [MethodChannel].

### lastSavedResults

```dart
SpellCheckResults? lastSavedResults
```

The last received results from the shell side.

### spellCheckChannel

```dart
MethodChannel spellCheckChannel
```

The channel used to communicate with the shell side to complete spell check requests.

### mergeResults()

```dart
List<SuggestionSpan> mergeResults(List<SuggestionSpan> oldResults, List<SuggestionSpan> newResults)
```

Merges two lists of spell check [SuggestionSpan]s.

Used in cases where the text has not changed, but the spell check results received from the shell side have. This case is caused by IMEs (GBoard, for instance) that ignore the composing region when spell checking text.

Assumes that the lists provided as parameters are sorted by range start and that both list of [SuggestionSpan]s apply to the same text.

### fetchSpellCheckSuggestions()

```dart
Future<List<SuggestionSpan>?> fetchSpellCheckSuggestions(Locale locale, String text)
```
