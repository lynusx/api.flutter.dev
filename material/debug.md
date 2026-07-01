# debugCheckHasMaterial()

```dart
bool debugCheckHasMaterial(BuildContext context)
```

Asserts that the given context has a [Material] ancestor within the closest [LookupBoundary].

Used by many Material Design widgets to make sure that they are only used in contexts where they can print ink onto some material.

To call this function, use the following pattern, typically in the relevant Widget's build method:

```dart
assert(debugCheckHasMaterial(context));
```

Always place this before any early returns, so that the invariant is checked in all cases. This prevents bugs from hiding until a particular codepath is hit.

This method can be expensive (it walks the element tree).

Does nothing if asserts are disabled. Always returns true.

# debugCheckHasMaterialLocalizations()

```dart
bool debugCheckHasMaterialLocalizations(BuildContext context)
```

Asserts that the given context has a [Localizations] ancestor that contains a [MaterialLocalizations] delegate.

Used by many Material Design widgets to make sure that they are only used in contexts where they have access to localizations.

To call this function, use the following pattern, typically in the relevant Widget's build method:

```dart
assert(debugCheckHasMaterialLocalizations(context));
```

Always place this before any early returns, so that the invariant is checked in all cases. This prevents bugs from hiding until a particular codepath is hit.

This function has the side-effect of establishing an inheritance relationship with the nearest [Localizations] widget (see [BuildContext.dependOnInheritedWidgetOfExactType]). This is ok if the caller always also calls [Localizations.of] or [Localizations.localeOf].

Does nothing if asserts are disabled. Always returns true.

# debugCheckHasScaffold()

```dart
bool debugCheckHasScaffold(BuildContext context)
```

Asserts that the given context has a [Scaffold] ancestor.

Used by various widgets to make sure that they are only used in an appropriate context.

To invoke this function, use the following pattern, typically in the relevant Widget's build method:

```dart
assert(debugCheckHasScaffold(context));
```

Always place this before any early returns, so that the invariant is checked in all cases. This prevents bugs from hiding until a particular codepath is hit.

This method can be expensive (it walks the element tree).

Does nothing if asserts are disabled. Always returns true.

# debugCheckHasScaffoldMessenger()

```dart
bool debugCheckHasScaffoldMessenger(BuildContext context)
```

Asserts that the given context has a [ScaffoldMessenger] ancestor.

Used by various widgets to make sure that they are only used in an appropriate context.

To invoke this function, use the following pattern, typically in the relevant Widget's build method:

```dart
assert(debugCheckHasScaffoldMessenger(context));
```

Always place this before any early returns, so that the invariant is checked in all cases. This prevents bugs from hiding until a particular codepath is hit.

This method can be expensive (it walks the element tree).

Does nothing if asserts are disabled. Always returns true.
