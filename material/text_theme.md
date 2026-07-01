@docImport 'elevated_button.dart'; @docImport 'material.dart'; @docImport 'outlined_button.dart'; @docImport 'text_button.dart'; @docImport 'theme.dart'; @docImport 'theme_data.dart';

# TextTheme

```dart
class TextTheme with Diagnosticable {}
```

Material design text theme.

Definitions for the various typographical styles found in Material Design (e.g., labelLarge, bodySmall). Rather than creating a [TextTheme] directly, you can obtain an instance as [Typography.black] or [Typography.white].

To obtain the current text theme, call [TextTheme.of] with the current [BuildContext]. This is equivalent to calling [Theme.of] and reading the [ThemeData.textTheme] property.

The names of the TextTheme properties match this table from the [Material Design spec](https://m3.material.io/styles/typography/tokens).

![](https://lh3.googleusercontent.com/Yvngs5mQSjXa_9T4X3JDucO62c5hdZHPDa7qeRH6DsJQvGr_q7EBrTkhkPiQd9OeR1v_Uk38Cjd9nUpP3nevDyHpKWuXSfQ1Gq78bOnBN7sr=s0)

The Material Design typography scheme was significantly changed in the current (2021) version of the specification ([https://m3.material.io/styles/typography/tokens](https://m3.material.io/styles/typography/tokens)).

The **2021** spec has fifteen text styles:

| NAME           | SIZE | HEIGHT | WEIGHT  | SPACING |     |
| -------------- | ---- | ------ | ------- | ------- | --- |
| displayLarge   | 57.0 | 64.0   | regular | -0.25   |     |
| displayMedium  | 45.0 | 52.0   | regular | 0.0     |     |
| displaySmall   | 36.0 | 44.0   | regular | 0.0     |     |
| headlineLarge  | 32.0 | 40.0   | regular | 0.0     |     |
| headlineMedium | 28.0 | 36.0   | regular | 0.0     |     |
| headlineSmall  | 24.0 | 32.0   | regular | 0.0     |     |
| titleLarge     | 22.0 | 28.0   | regular | 0.0     |     |
| titleMedium    | 16.0 | 24.0   | medium  | 0.15    |     |
| titleSmall     | 14.0 | 20.0   | medium  | 0.1     |     |
| bodyLarge      | 16.0 | 24.0   | regular | 0.5     |     |
| bodyMedium     | 14.0 | 20.0   | regular | 0.25    |     |
| bodySmall      | 12.0 | 16.0   | regular | 0.4     |     |
| labelLarge     | 14.0 | 20.0   | medium  | 0.1     |     |
| labelMedium    | 12.0 | 16.0   | medium  | 0.5     |     |
| labelSmall     | 11.0 | 16.0   | medium  | 0.5     |     |

...where "regular" is `FontWeight.w400` and "medium" is `FontWeight.w500`.

The names of the 2018 TextTheme properties match this table from the [Material Design spec](https://material.io/design/typography/the-type-system.html#type-scale) with a few exceptions: the styles called H1-H6 in the spec are displayLarge-titleLarge in the API chart, body1,body2 are called bodyLarge and bodyMedium, caption is now bodySmall, button is labelLarge, and overline is now labelSmall.

The **2018** spec has thirteen text styles:

| NAME           | SIZE | WEIGHT  | SPACING |     |
| -------------- | ---- | ------- | ------- | --- |
| displayLarge   | 96.0 | light   | -1.5    |     |
| displayMedium  | 60.0 | light   | -0.5    |     |
| displaySmall   | 48.0 | regular | 0.0     |     |
| headlineMedium | 34.0 | regular | 0.25    |     |
| headlineSmall  | 24.0 | regular | 0.0     |     |
| titleLarge     | 20.0 | medium  | 0.15    |     |
| titleMedium    | 16.0 | regular | 0.15    |     |
| titleSmall     | 14.0 | medium  | 0.1     |     |
| bodyLarge      | 16.0 | regular | 0.5     |     |
| bodyMedium     | 14.0 | regular | 0.25    |     |
| bodySmall      | 12.0 | regular | 0.4     |     |
| labelLarge     | 14.0 | medium  | 1.25    |     |
| labelSmall     | 10.0 | regular | 1.5     |     |

...where "light" is `FontWeight.w300`, "regular" is `FontWeight.w400` and "medium" is `FontWeight.w500`.

By default, text styles are initialized to match the 2018 Material Design specification as listed above. To provide backwards compatibility, the 2014 specification is also available.

To explicitly configure a [Theme] for the 2018 sizes, weights, and letter spacings, you can initialize its [ThemeData.typography] value using [Typography.material2018]. The [Typography] constructor defaults to this configuration. To configure a [Theme] for the 2014 sizes, weights, and letter spacings, initialize its [ThemeData.typography] value using [Typography.material2014].

See also:

- [Typography], the class that generates [TextTheme]s appropriate for a platform.
- [Theme], for other aspects of a Material Design application that can be globally adjusted, such as the color scheme.
- <https://material.io/design/typography/>

### TextTheme()

```dart
TextTheme({TextStyle? displayLarge, TextStyle? displayMedium, TextStyle? displaySmall, TextStyle? headlineLarge, TextStyle? headlineMedium, TextStyle? headlineSmall, TextStyle? titleLarge, TextStyle? titleMedium, TextStyle? titleSmall, TextStyle? bodyLarge, TextStyle? bodyMedium, TextStyle? bodySmall, TextStyle? labelLarge, TextStyle? labelMedium, TextStyle? labelSmall})
```

Creates a text theme that uses the given values.

Rather than creating a new text theme, consider using [Typography.black] or [Typography.white], which implement the typography styles in the Material Design specification:

<https://material.io/design/typography/#type-scale>

If you do decide to create your own text theme, consider using one of those predefined themes as a starting point for [copyWith] or [apply].

The 2018 styles cannot be mixed with the 2021 styles. Only one or the other is allowed in this constructor. The 2018 styles are deprecated and will eventually be removed.

### displayLarge

```dart
TextStyle? displayLarge
```

Largest of the display styles.

As the largest text on the screen, display styles are reserved for short, important text or numerals. They work best on large screens.

### displayMedium

```dart
TextStyle? displayMedium
```

Middle size of the display styles.

As the largest text on the screen, display styles are reserved for short, important text or numerals. They work best on large screens.

### displaySmall

```dart
TextStyle? displaySmall
```

Smallest of the display styles.

As the largest text on the screen, display styles are reserved for short, important text or numerals. They work best on large screens.

### headlineLarge

```dart
TextStyle? headlineLarge
```

Largest of the headline styles.

Headline styles are smaller than display styles. They're best-suited for short, high-emphasis text on smaller screens.

### headlineMedium

```dart
TextStyle? headlineMedium
```

Middle size of the headline styles.

Headline styles are smaller than display styles. They're best-suited for short, high-emphasis text on smaller screens.

### headlineSmall

```dart
TextStyle? headlineSmall
```

Smallest of the headline styles.

Headline styles are smaller than display styles. They're best-suited for short, high-emphasis text on smaller screens.

### titleLarge

```dart
TextStyle? titleLarge
```

Largest of the title styles.

Titles are smaller than headline styles and should be used for shorter, medium-emphasis text.

### titleMedium

```dart
TextStyle? titleMedium
```

Middle size of the title styles.

Titles are smaller than headline styles and should be used for shorter, medium-emphasis text.

### titleSmall

```dart
TextStyle? titleSmall
```

Smallest of the title styles.

Titles are smaller than headline styles and should be used for shorter, medium-emphasis text.

### bodyLarge

```dart
TextStyle? bodyLarge
```

Largest of the body styles.

Body styles are used for longer passages of text.

### bodyMedium

```dart
TextStyle? bodyMedium
```

Middle size of the body styles.

Body styles are used for longer passages of text.

The default text style for [Material].

### bodySmall

```dart
TextStyle? bodySmall
```

Smallest of the body styles.

Body styles are used for longer passages of text.

### labelLarge

```dart
TextStyle? labelLarge
```

Largest of the label styles.

Label styles are smaller, utilitarian styles, used for areas of the UI such as text inside of components or very small supporting text in the content body, like captions.

Used for text on [ElevatedButton], [TextButton] and [OutlinedButton].

### labelMedium

```dart
TextStyle? labelMedium
```

Middle size of the label styles.

Label styles are smaller, utilitarian styles, used for areas of the UI such as text inside of components or very small supporting text in the content body, like captions.

### labelSmall

```dart
TextStyle? labelSmall
```

Smallest of the label styles.

Label styles are smaller, utilitarian styles, used for areas of the UI such as text inside of components or very small supporting text in the content body, like captions.

### copyWith()

```dart
TextTheme copyWith({TextStyle? displayLarge, TextStyle? displayMedium, TextStyle? displaySmall, TextStyle? headlineLarge, TextStyle? headlineMedium, TextStyle? headlineSmall, TextStyle? titleLarge, TextStyle? titleMedium, TextStyle? titleSmall, TextStyle? bodyLarge, TextStyle? bodyMedium, TextStyle? bodySmall, TextStyle? labelLarge, TextStyle? labelMedium, TextStyle? labelSmall})
```

Creates a copy of this text theme but with the given fields replaced with the new values.

Consider using [Typography.black] or [Typography.white], which implement the typography styles in the Material Design specification, as a starting point.

{@tool snippet}

```dart
/// A Widget that sets the ambient theme's title text color for its
/// descendants, while leaving other ambient theme attributes alone.
class TitleColorThemeCopy extends StatelessWidget {
  const TitleColorThemeCopy({super.key, required this.titleColor, required this.child});

  final Color titleColor;
  final Widget child;

  @override
  Widget build(BuildContext context) {
    final ThemeData theme = Theme.of(context);
    return Theme(
      data: theme.copyWith(
        textTheme: theme.textTheme.copyWith(
          titleLarge: theme.textTheme.titleLarge!.copyWith(
            color: titleColor,
          ),
        ),
      ),
      child: child,
    );
  }
}
```

{@end-tool}

See also:

- [merge] is used instead of [copyWith] when you want to merge all of the fields of a TextTheme instead of individual fields.

### merge()

```dart
TextTheme merge(TextTheme? other)
```

Creates a new [TextTheme] where each text style from this object has been merged with the matching text style from the `other` object.

The merging is done by calling [TextStyle.merge] on each respective pair of text styles from this and the [other] text themes and is subject to the value of [TextStyle.inherit] flag. For more details, see the documentation on [TextStyle.merge] and [TextStyle.inherit].

If this theme, or the `other` theme has members that are null, then the non-null one (if any) is used. If the `other` theme is itself null, then this [TextTheme] is returned unchanged. If values in both are set, then the values are merged using [TextStyle.merge].

This is particularly useful if one [TextTheme] defines one set of properties and another defines a different set, e.g. having colors defined in one text theme and font sizes in another, or when one [TextTheme] has only some fields defined, and you want to define the rest by merging it with a default theme.

{@tool snippet}

```dart
/// A Widget that sets the ambient theme's title text color for its
/// descendants, while leaving other ambient theme attributes alone.
class TitleColorTheme extends StatelessWidget {
  const TitleColorTheme({super.key, required this.child, required this.titleColor});

  final Color titleColor;
  final Widget child;

  @override
  Widget build(BuildContext context) {
    ThemeData theme = Theme.of(context);
    // This partialTheme is incomplete: it only has the title style
    // defined. Just replacing theme.textTheme with partialTheme would
    // set the title, but everything else would be null. This isn't very
    // useful, so merge it with the existing theme to keep all of the
    // preexisting definitions for the other styles.
    final TextTheme partialTheme = TextTheme(titleLarge: TextStyle(color: titleColor));
    theme = theme.copyWith(textTheme: theme.textTheme.merge(partialTheme));
    return Theme(data: theme, child: child);
  }
}
```

{@end-tool}

See also:

- [copyWith] is used instead of [merge] when you wish to override individual fields in the [TextTheme] instead of merging all of the fields of two [TextTheme]s.

### apply()

```dart
TextTheme apply({String? fontFamily, List<String>? fontFamilyFallback, String? package, double fontSizeFactor = 1.0, double fontSizeDelta = 0.0, double letterSpacingFactor = 1.0, double letterSpacingDelta = 0.0, double wordSpacingFactor = 1.0, double wordSpacingDelta = 0.0, double heightFactor = 1.0, double heightDelta = 0.0, Color? displayColor, Color? bodyColor, TextDecoration? decoration, Color? decorationColor, TextDecorationStyle? decorationStyle})
```

Creates a copy of this text theme but with the given field replaced in each of the individual text styles.

The `displayColor` is applied to [displayLarge], [displayMedium], [displaySmall], [headlineLarge], [headlineMedium], and [bodySmall]. The `bodyColor` is applied to the remaining text styles.

Consider using [Typography.black] or [Typography.white], which implement the typography styles in the Material Design specification, as a starting point.

### lerp()

```dart
TextTheme lerp(TextTheme? a, TextTheme? b, double t)
```

Linearly interpolate between two text themes.

{@macro dart.ui.shadow.lerp}

### of()

```dart
TextTheme of(BuildContext context)
```

The [ThemeData.textTheme] property of the ambient [Theme].

Equivalent to `Theme.of(context).textTheme`.

See also:

- [TextTheme.primaryOf], which returns the [ThemeData.primaryTextTheme] property of the ambient [Theme] instead.

### primaryOf()

```dart
TextTheme primaryOf(BuildContext context)
```

The [ThemeData.primaryTextTheme] property of the ambient [Theme].

Equivalent to `Theme.of(context).primaryTextTheme`.

See also:

- [TextTheme.of], which returns the [ThemeData.textTheme] property of the ambient [Theme] instead.

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
