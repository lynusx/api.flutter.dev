@docImport 'package:flutter/painting.dart';

@docImport 'framework.dart';

# RestorableValue

```dart
abstract class RestorableValue<T> extends RestorableProperty<T> {}
```

A [RestorableProperty] that makes the wrapped value accessible to the owning [State] object via the [value] getter and setter.

Whenever a new [value] is set, [didUpdateValue] is called. Subclasses should call [notifyListeners] from this method if the new value changes what [toPrimitives] returns.

## Using a RestorableValue

{@tool dartpad} A [StatefulWidget] that has a restorable [int] property.

** See code in examples/api/lib/widgets/restoration_properties/restorable_value.0.dart ** {@end-tool}

## Creating a subclass

{@tool snippet} This example shows how to create a new [RestorableValue] subclass, in this case for the [Duration] class.

```dart
class RestorableDuration extends RestorableValue<Duration> {
  @override
  Duration createDefaultValue() => Duration.zero;

  @override
  void didUpdateValue(Duration? oldValue) {
    if (oldValue == null || oldValue.inMicroseconds != value.inMicroseconds) {
      notifyListeners();
    }
  }

  @override
  Duration fromPrimitives(Object? data) {
    if (data != null) {
      return Duration(microseconds: data as int);
    }
    return Duration.zero;
  }

  @override
  Object toPrimitives() {
    return value.inMicroseconds;
  }
}
```

{@end-tool}

See also:

- [RestorableProperty], which is the super class of this class.
- [RestorationMixin], to which a [RestorableValue] needs to be registered in order to work.
- [RestorationManager], which provides an overview of how state restoration works in Flutter.

### value

```dart
T get value
```

The current value stored in this property.

A representation of the current value is stored in the restoration data. During state restoration, the property will restore the value to what it was when the restoration data it is getting restored from was collected.

The [value] can only be accessed after the property has been registered with a [RestorationMixin] by calling [RestorationMixin.registerForRestoration].

### value

```dart
set value(T newValue)
```

### initWithValue()

```dart
void initWithValue(T value)
```

### didUpdateValue()

```dart
void didUpdateValue(T? oldValue)
```

Called whenever a new value is assigned to [value].

The new value can be accessed via the regular [value] getter and the previous value is provided as `oldValue`.

Subclasses should call [notifyListeners] from this method, if the new value changes what [toPrimitives] returns.

# RestorableNum

```dart
class RestorableNum<T extends num> extends _RestorablePrimitiveValue<T> {}
```

A [RestorableProperty] that knows how to store and restore a [num].

{@template flutter.widgets.RestorableNum} The current [value] of this property is stored in the restoration data. During state restoration the property is restored to the value it had when the restoration data it is getting restored from was collected.

If no restoration data is available, [value] is initialized to the `defaultValue` given in the constructor. {@endtemplate}

Instead of using the more generic [RestorableNum] directly, consider using one of the more specific subclasses (e.g. [RestorableDouble] to store a [double] and [RestorableInt] to store an [int]).

See also:

- [RestorableNumN] for the nullable version of this class.

### RestorableNum()

```dart
RestorableNum(T defaultValue)
```

Creates a [RestorableNum].

{@template flutter.widgets.RestorableNum.constructor} If no restoration data is available to restore the value in this property from, the property will be initialized with the provided `defaultValue`. {@endtemplate}

# RestorableDouble

```dart
class RestorableDouble extends RestorableNum<double> {}
```

A [RestorableProperty] that knows how to store and restore a [double].

{@macro flutter.widgets.RestorableNum}

See also:

- [RestorableDoubleN] for the nullable version of this class.

### RestorableDouble()

```dart
RestorableDouble(double defaultValue)
```

Creates a [RestorableDouble].

{@macro flutter.widgets.RestorableNum.constructor}

# RestorableInt

```dart
class RestorableInt extends RestorableNum<int> {}
```

A [RestorableProperty] that knows how to store and restore an [int].

{@macro flutter.widgets.RestorableNum}

See also:

- [RestorableIntN] for the nullable version of this class.

### RestorableInt()

```dart
RestorableInt(int defaultValue)
```

Creates a [RestorableInt].

{@macro flutter.widgets.RestorableNum.constructor}

# RestorableString

```dart
class RestorableString extends _RestorablePrimitiveValue<String> {}
```

A [RestorableProperty] that knows how to store and restore a [String].

{@macro flutter.widgets.RestorableNum}

See also:

- [RestorableStringN] for the nullable version of this class.

### RestorableString()

```dart
RestorableString(String defaultValue)
```

Creates a [RestorableString].

{@macro flutter.widgets.RestorableNum.constructor}

# RestorableBool

```dart
class RestorableBool extends _RestorablePrimitiveValue<bool> {}
```

A [RestorableProperty] that knows how to store and restore a [bool].

{@macro flutter.widgets.RestorableNum}

See also:

- [RestorableBoolN] for the nullable version of this class.

### RestorableBool()

```dart
RestorableBool(bool defaultValue)
```

Creates a [RestorableBool].

{@macro flutter.widgets.RestorableNum.constructor}

# RestorableBoolN

```dart
class RestorableBoolN extends _RestorablePrimitiveValueN<bool?> {}
```

A [RestorableProperty] that knows how to store and restore a [bool] that is nullable.

{@macro flutter.widgets.RestorableNum}

See also:

- [RestorableBool] for the non-nullable version of this class.

### RestorableBoolN()

```dart
RestorableBoolN(bool? defaultValue)
```

Creates a [RestorableBoolN].

{@macro flutter.widgets.RestorableNum.constructor}

# RestorableNumN

```dart
class RestorableNumN<T extends num?> extends _RestorablePrimitiveValueN<T> {}
```

A [RestorableProperty] that knows how to store and restore a [num] that is nullable.

{@macro flutter.widgets.RestorableNum}

Instead of using the more generic [RestorableNumN] directly, consider using one of the more specific subclasses (e.g. [RestorableDoubleN] to store a [double] and [RestorableIntN] to store an [int]).

See also:

- [RestorableNum] for the non-nullable version of this class.

### RestorableNumN()

```dart
RestorableNumN(T defaultValue)
```

Creates a [RestorableNumN].

{@macro flutter.widgets.RestorableNum.constructor}

# RestorableDoubleN

```dart
class RestorableDoubleN extends RestorableNumN<double?> {}
```

A [RestorableProperty] that knows how to store and restore a [double] that is nullable.

{@macro flutter.widgets.RestorableNum}

See also:

- [RestorableDouble] for the non-nullable version of this class.

### RestorableDoubleN()

```dart
RestorableDoubleN(double? defaultValue)
```

Creates a [RestorableDoubleN].

{@macro flutter.widgets.RestorableNum.constructor}

# RestorableIntN

```dart
class RestorableIntN extends RestorableNumN<int?> {}
```

A [RestorableProperty] that knows how to store and restore an [int] that is nullable.

{@macro flutter.widgets.RestorableNum}

See also:

- [RestorableInt] for the non-nullable version of this class.

### RestorableIntN()

```dart
RestorableIntN(int? defaultValue)
```

Creates a [RestorableIntN].

{@macro flutter.widgets.RestorableNum.constructor}

# RestorableStringN

```dart
class RestorableStringN extends _RestorablePrimitiveValueN<String?> {}
```

A [RestorableProperty] that knows how to store and restore a [String] that is nullable.

{@macro flutter.widgets.RestorableNum}

See also:

- [RestorableString] for the non-nullable version of this class.

### RestorableStringN()

```dart
RestorableStringN(String? defaultValue)
```

Creates a [RestorableString].

{@macro flutter.widgets.RestorableNum.constructor}

# RestorableDateTime

```dart
class RestorableDateTime extends RestorableValue<DateTime> {}
```

A [RestorableValue] that knows how to save and restore [DateTime].

{@macro flutter.widgets.RestorableNum}.

### RestorableDateTime()

```dart
RestorableDateTime(DateTime defaultValue)
```

Creates a [RestorableDateTime].

{@macro flutter.widgets.RestorableNum.constructor}

### createDefaultValue()

```dart
DateTime createDefaultValue()
```

### didUpdateValue()

```dart
void didUpdateValue(DateTime? oldValue)
```

### fromPrimitives()

```dart
DateTime fromPrimitives(Object? data)
```

### toPrimitives()

```dart
Object? toPrimitives()
```

# RestorableDateTimeN

```dart
class RestorableDateTimeN extends RestorableValue<DateTime?> {}
```

A [RestorableValue] that knows how to save and restore [DateTime] that is nullable.

{@macro flutter.widgets.RestorableNum}.

### RestorableDateTimeN()

```dart
RestorableDateTimeN(DateTime? defaultValue)
```

Creates a [RestorableDateTime].

{@macro flutter.widgets.RestorableNum.constructor}

### createDefaultValue()

```dart
DateTime? createDefaultValue()
```

### didUpdateValue()

```dart
void didUpdateValue(DateTime? oldValue)
```

### fromPrimitives()

```dart
DateTime? fromPrimitives(Object? data)
```

### toPrimitives()

```dart
Object? toPrimitives()
```

# RestorableListenable

```dart
abstract class RestorableListenable<T extends Listenable> extends RestorableProperty<T> {}
```

A base class for creating a [RestorableProperty] that stores and restores a [Listenable].

This class may be used to implement a [RestorableProperty] for a [Listenable], whose information it needs to store in the restoration data change whenever the [Listenable] notifies its listeners.

The [RestorationMixin] this property is registered with will call [toPrimitives] whenever the wrapped [Listenable] notifies its listeners to update the information that this property has stored in the restoration data.

### value

```dart
T get value
```

The [Listenable] stored in this property.

A representation of the current value of the [Listenable] is stored in the restoration data. During state restoration, the [Listenable] returned by this getter will be restored to the state it had when the restoration data the property is getting restored from was collected.

The [value] can only be accessed after the property has been registered with a [RestorationMixin] by calling [RestorationMixin.registerForRestoration].

### initWithValue()

```dart
void initWithValue(T value)
```

### dispose()

```dart
void dispose()
```

# RestorableChangeNotifier

```dart
abstract class RestorableChangeNotifier<T extends ChangeNotifier> extends RestorableListenable<T> {}
```

A base class for creating a [RestorableProperty] that stores and restores a [ChangeNotifier].

This class may be used to implement a [RestorableProperty] for a [ChangeNotifier], whose information it needs to store in the restoration data change whenever the [ChangeNotifier] notifies its listeners.

The [RestorationMixin] this property is registered with will call [toPrimitives] whenever the wrapped [ChangeNotifier] notifies its listeners to update the information that this property has stored in the restoration data.

Furthermore, the property will dispose the wrapped [ChangeNotifier] when either the property itself is disposed or its value is replaced with another [ChangeNotifier] instance.

### initWithValue()

```dart
void initWithValue(T value)
```

### dispose()

```dart
void dispose()
```

# RestorableTextEditingController

```dart
class RestorableTextEditingController extends RestorableChangeNotifier<TextEditingController> {}
```

A [RestorableProperty] that knows how to store and restore a [TextEditingController].

The [TextEditingController] is accessible via the [value] getter. During state restoration, the property will restore [TextEditingController.text] to the value it had when the restoration data it is getting restored from was collected.

### RestorableTextEditingController()

```dart
RestorableTextEditingController({String? text})
```

Creates a [RestorableTextEditingController].

This constructor treats a null `text` argument as if it were the empty string.

### RestorableTextEditingController.fromValue()

```dart
RestorableTextEditingController.fromValue(TextEditingValue value)
```

Creates a [RestorableTextEditingController] from an initial [TextEditingValue].

This constructor treats a null `value` argument as if it were [TextEditingValue.empty].

### createDefaultValue()

```dart
TextEditingController createDefaultValue()
```

### fromPrimitives()

```dart
TextEditingController fromPrimitives(Object? data)
```

### toPrimitives()

```dart
Object toPrimitives()
```

# RestorableEnumN

```dart
class RestorableEnumN<T extends Enum> extends RestorableValue<T?> {}
```

A [RestorableProperty] that knows how to store and restore a nullable [Enum] type.

{@macro flutter.widgets.RestorableNum}

The values are serialized using the name of the enum, obtained using the [EnumName.name] extension accessor.

The represented value is accessible via the [value] getter. The set of values in the enum are accessible via the [values] getter. Since [RestorableEnumN] allows null, this set will include null.

See also:

- [RestorableEnum], a class similar to this one that knows how to store and restore non-nullable [Enum] types.

### RestorableEnumN()

```dart
RestorableEnumN(T? defaultValue, {required Iterable<T> values})
```

Creates a [RestorableEnumN].

{@macro flutter.widgets.RestorableNum.constructor}

### createDefaultValue()

```dart
T? createDefaultValue()
```

### value

```dart
set value(T? newValue)
```

### values

```dart
Set<T> values
```

The set of non-null values that this [RestorableEnumN] may represent.

This is a required field that supplies the enum values that are serialized and restored.

If a value is encountered that is not null or a value in this set, [fromPrimitives] will assert when restoring.

It is typically set to the `values` list of the enum type.

In addition to this set, because [RestorableEnumN] allows nullable values, null is also a valid value, even though it doesn't appear in this set.

{@tool snippet} For example, to create a [RestorableEnumN] with an [AxisDirection] enum value, with a default value of null, you would build it like the code below:

```dart
RestorableEnumN<AxisDirection> axis = RestorableEnumN<AxisDirection>(null, values: AxisDirection.values);
```

{@end-tool}

### didUpdateValue()

```dart
void didUpdateValue(T? oldValue)
```

### fromPrimitives()

```dart
T? fromPrimitives(Object? data)
```

### toPrimitives()

```dart
Object? toPrimitives()
```

# RestorableEnum

```dart
class RestorableEnum<T extends Enum> extends RestorableValue<T> {}
```

A [RestorableProperty] that knows how to store and restore an [Enum] type.

{@macro flutter.widgets.RestorableNum}

The values are serialized using the name of the enum, obtained using the [EnumName.name] extension accessor.

The represented value is accessible via the [value] getter.

See also:

- [RestorableEnumN], a class similar to this one that knows how to store and restore nullable [Enum] types.

### RestorableEnum()

```dart
RestorableEnum(T defaultValue, {required Iterable<T> values})
```

Creates a [RestorableEnum].

{@macro flutter.widgets.RestorableNum.constructor}

### createDefaultValue()

```dart
T createDefaultValue()
```

### value

```dart
set value(T newValue)
```

### values

```dart
Set<T> values
```

The set of values that this [RestorableEnum] may represent.

This is a required field that supplies the possible enum values that can be serialized and restored.

If a value is encountered that is not in this set, [fromPrimitives] will assert when restoring.

It is typically set to the `values` list of the enum type.

{@tool snippet} For example, to create a [RestorableEnum] with an [AxisDirection] enum value, with a default value of [AxisDirection.up], you would build it like the code below:

```dart
RestorableEnum<AxisDirection> axis = RestorableEnum<AxisDirection>(AxisDirection.up, values: AxisDirection.values);
```

{@end-tool}

### didUpdateValue()

```dart
void didUpdateValue(T? oldValue)
```

### fromPrimitives()

```dart
T fromPrimitives(Object? data)
```

### toPrimitives()

```dart
Object toPrimitives()
```
