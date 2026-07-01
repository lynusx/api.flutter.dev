# kMaxUnsignedSMI

```dart
int kMaxUnsignedSMI
```

The web implementation of [bitfield.kMaxUnsignedSMI].

This value is used as an optimization to coerce some numbers to be within the SMI range and avoid heap allocations. Because number encoding is VM-specific, there's no guarantee that this optimization will be effective on all JavaScript engines. The value picked here should be correct, but it does not have to guarantee efficiency.

# BitField

```dart
class BitField<T extends dynamic> implements bitfield.BitField<T> {}
```

The web implementation of [bitfield.BitField].

### BitField()

```dart
BitField(int length)
```

The web implementation of [bitfield.BitField].

### BitField.filled()

```dart
BitField.filled(int length, bool value)
```

The web implementation of [bitfield.BitField.filled].

### operator []()

```dart
bool operator [](T index)
```

### operator []=()

```dart
void operator []=(T index, bool value)
```

### reset()

```dart
void reset([bool value = false])
```
