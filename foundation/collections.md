@docImport 'package:collection/collection.dart';

# setEquals()

```dart
bool setEquals<T>(Set<T>? a, Set<T>? b)
```

Compares two sets for element-by-element equality.

Returns true if the sets are both null, or if they are both non-null, have the same length, and contain the same members. Returns false otherwise. Order is not compared.

If the elements are maps, lists, sets, or other collections/composite objects, then the contents of those elements are not compared element by element unless their equality operators ([Object.==]) do so. For checking deep equality, consider using the [DeepCollectionEquality] class.

See also:

- [listEquals], which does something similar for lists.
- [mapEquals], which does something similar for maps.

# listEquals()

```dart
bool listEquals<T>(List<T>? a, List<T>? b)
```

Compares two lists for element-by-element equality.

Returns true if the lists are both null, or if they are both non-null, have the same length, and contain the same members in the same order. Returns false otherwise.

If the elements are maps, lists, sets, or other collections/composite objects, then the contents of those elements are not compared element by element unless their equality operators ([Object.==]) do so. For checking deep equality, consider using the [DeepCollectionEquality] class.

See also:

- [setEquals], which does something similar for sets.
- [mapEquals], which does something similar for maps.

# mapEquals()

```dart
bool mapEquals<T, U>(Map<T, U>? a, Map<T, U>? b)
```

Compares two maps for element-by-element equality.

Returns true if the maps are both null, or if they are both non-null, have the same length, and contain the same keys associated with the same values. Returns false otherwise.

If the elements are maps, lists, sets, or other collections/composite objects, then the contents of those elements are not compared element by element unless their equality operators ([Object.==]) do so. For checking deep equality, consider using the [DeepCollectionEquality] class.

See also:

- [setEquals], which does something similar for sets.
- [listEquals], which does something similar for lists.

# binarySearch()

```dart
int binarySearch<T extends Comparable<Object>>(List<T> sortedList, T value)
```

Returns the position of `value` in the `sortedList`, if it exists.

Returns `-1` if the `value` is not in the list. Requires the list items to implement [Comparable] and the `sortedList` to already be ordered.

# mergeSort()

```dart
void mergeSort<T>(List<T> list, {int start = 0, int? end, int Function(T, T)? compare})
```

Sorts a list between `start` (inclusive) and `end` (exclusive) using the merge sort algorithm.

If `compare` is omitted, this defaults to calling [Comparable.compareTo] on the objects. If any object is not [Comparable], this throws a [TypeError] (The stack trace may call it `_CastError` or `_TypeError`, but to catch it, use [TypeError]).

Merge-sorting works by splitting the job into two parts, sorting each recursively, and then merging the two sorted parts.

This takes on the order of `n * log(n)` comparisons and moves to sort `n` elements, but requires extra space of about the same size as the list being sorted.

This merge sort is stable: Equal elements end up in the same order as they started in.

For small lists (less than 32 elements), [mergeSort] automatically uses an insertion sort instead, as that is more efficient for small lists. The insertion sort is also stable.
