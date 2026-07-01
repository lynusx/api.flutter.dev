# kMaxUnsignedSMI

```dart
int kMaxUnsignedSMI
```

The largest SMI value.

See <https://www.dartlang.org/articles/numeric-computation/#smis-and-mints>

When compiling to JavaScript, this value is not supported since it is larger than the maximum safe 32bit integer.

# BitField

```dart
abstract class BitField<T extends dynamic> {}
```

A BitField over an enum (or other class whose values implement "index").

Only the first 62 values of the enum can be used as indices.

When compiling to JavaScript, this class is not supported.

### BitField()

```dart
BitField(int length)
```

Creates a bit field of all zeros.

The given length must be at most 62.

### BitField.filled()

```dart
BitField.filled(int length, bool value)
```

Creates a bit field filled with a particular value.

If the value argument is true, the bits are filled with ones. Otherwise, the bits are filled with zeros.

The given length must be at most 62.

### operator []()

```dart
bool operator [](T index)
```

Returns whether the bit with the given index is set to one.

### operator []=()

```dart
void operator []=(T index, bool value)
```

Sets the bit with the given index to the given value.

If value is true, the bit with the given index is set to one. Otherwise, the bit is set to zero.

### reset()

```dart
void reset([bool value = false])
```

Sets all the bits to the given value.

If the value is true, the bits are all set to one. Otherwise, the bits are all set to zero. Defaults to setting all the bits to zero.
