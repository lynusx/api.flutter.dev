# debugCheckHasCupertinoLocalizations()

```dart
bool debugCheckHasCupertinoLocalizations(BuildContext context)
```

Asserts that the given context has a [Localizations] ancestor that contains a [CupertinoLocalizations] delegate.

To call this function, use the following pattern, typically in the relevant Widget's build method:

```dart
assert(debugCheckHasCupertinoLocalizations(context));
```

Always place this before any early returns, so that the invariant is checked in all cases. This prevents bugs from hiding until a particular codepath is hit.

Does nothing if asserts are disabled. Always returns true.
