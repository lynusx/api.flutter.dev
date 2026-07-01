# BinaryCodec

```dart
class BinaryCodec implements MessageCodec<ByteData> {}
```

[MessageCodec] with unencoded binary messages represented using [ByteData].

On Android, messages will be represented using `java.nio.ByteBuffer`. On iOS, messages will be represented using `NSData`.

When sending outgoing messages from Android, be sure to use direct `ByteBuffer` as opposed to indirect. The `wrap()` API provides indirect buffers by default and you will get empty `ByteData` objects in Dart.

### BinaryCodec()

```dart
BinaryCodec()
```

Creates a [MessageCodec] with unencoded binary messages represented using [ByteData].

### decodeMessage()

```dart
ByteData? decodeMessage(ByteData? message)
```

### encodeMessage()

```dart
ByteData? encodeMessage(ByteData? message)
```

# StringCodec

```dart
class StringCodec implements MessageCodec<String> {}
```

[MessageCodec] with UTF-8 encoded String messages.

On Android, messages will be represented using `java.util.String`. On iOS, messages will be represented using `NSString`.

### StringCodec()

```dart
StringCodec()
```

Creates a [MessageCodec] with UTF-8 encoded String messages.

### decodeMessage()

```dart
String? decodeMessage(ByteData? message)
```

### encodeMessage()

```dart
ByteData? encodeMessage(String? message)
```

# JSONMessageCodec

```dart
class JSONMessageCodec implements MessageCodec<Object?> {}
```

[MessageCodec] with UTF-8 encoded JSON messages.

Supported messages are acyclic values of these forms:

- null
- [bool]s
- [num]s
- [String]s
- [List]s of supported values
- [Map]s from strings to supported values

On Android, messages are decoded using the `org.json` library. On iOS, messages are decoded using the `NSJSONSerialization` library. In both cases, the use of top-level simple messages (null, [bool], [num], and [String]) is supported (by the Flutter SDK). The decoded value will be null/nil for null, and identical to what would result from decoding a singleton JSON array with a Boolean, number, or string value, and then extracting its single element.

The type returned from [decodeMessage] is `dynamic` (not `Object?`), which means _no type checking is performed on its return value_. It is strongly recommended that the return value be immediately cast to a known type to prevent runtime errors due to typos that the type checker could otherwise catch.

### JSONMessageCodec()

```dart
JSONMessageCodec()
```

Creates a [MessageCodec] with UTF-8 encoded JSON messages.

### encodeMessage()

```dart
ByteData? encodeMessage(Object? message)
```

### decodeMessage()

```dart
dynamic decodeMessage(ByteData? message)
```

# JSONMethodCodec

```dart
class JSONMethodCodec implements MethodCodec {}
```

[MethodCodec] with UTF-8 encoded JSON method calls and result envelopes.

Values supported as method arguments and result payloads are those supported by [JSONMessageCodec].

### JSONMethodCodec()

```dart
JSONMethodCodec()
```

Creates a [MethodCodec] with UTF-8 encoded JSON method calls and result envelopes.

### encodeMethodCall()

```dart
ByteData encodeMethodCall(MethodCall methodCall)
```

### decodeMethodCall()

```dart
MethodCall decodeMethodCall(ByteData? methodCall)
```

### decodeEnvelope()

```dart
dynamic decodeEnvelope(ByteData envelope)
```

### encodeSuccessEnvelope()

```dart
ByteData encodeSuccessEnvelope(Object? result)
```

### encodeErrorEnvelope()

```dart
ByteData encodeErrorEnvelope({required String code, String? message, Object? details})
```

# StandardMessageCodec

```dart
class StandardMessageCodec implements MessageCodec<Object?> {}
```

[MessageCodec] using the Flutter standard binary encoding.

Supported messages are acyclic values of these forms:

- null
- [bool]s
- [num]s
- [String]s
- [Uint8List]s, [Int32List]s, [Int64List]s, [Float64List]s
- [List]s of supported values
- [Map]s from supported values to supported values

Decoded values will use `List<Object?>` and `Map<Object?, Object?>` irrespective of content.

The type returned from [decodeMessage] is `dynamic` (not `Object?`), which means _no type checking is performed on its return value_. It is strongly recommended that the return value be immediately cast to a known type to prevent runtime errors due to typos that the type checker could otherwise catch.

The codec is extensible by subclasses overriding [writeValue] and [readValueOfType].

## Android specifics

On Android, messages are represented as follows:

- null: null
- [bool]\: `java.lang.Boolean`
- [int]\: `java.lang.Integer` for values that are representable using 32-bit two's complement; `java.lang.Long` otherwise
- [double]\: `java.lang.Double`
- [String]\: `java.lang.String`
- [Uint8List]\: `byte[]`
- [Int32List]\: `int[]`
- [Int64List]\: `long[]`
- [Float64List]\: `double[]`
- [List]\: `java.util.ArrayList`
- [Map]\: `java.util.HashMap`

When sending a `java.math.BigInteger` from Java, it is converted into a [String] with the hexadecimal representation of the integer. (The value is tagged as being a big integer; subclasses of this class could be made to support it natively; see the discussion at [writeValue].) This codec does not support sending big integers from Dart.

## iOS specifics

On iOS, messages are represented as follows:

- null: nil
- [bool]\: `NSNumber numberWithBool:`
- [int]\: `NSNumber numberWithInt:` for values that are representable using 32-bit two's complement; `NSNumber numberWithLong:` otherwise
- [double]\: `NSNumber numberWithDouble:`
- [String]\: `NSString`
- [Uint8List], [Int32List], [Int64List], [Float64List]\: `FlutterStandardTypedData`
- [List]\: `NSArray`
- [Map]\: `NSDictionary`

### StandardMessageCodec()

```dart
StandardMessageCodec()
```

Creates a [MessageCodec] using the Flutter standard binary encoding.

### encodeMessage()

```dart
ByteData? encodeMessage(Object? message)
```

### decodeMessage()

```dart
dynamic decodeMessage(ByteData? message)
```

### writeValue()

```dart
void writeValue(WriteBuffer buffer, Object? value)
```

Writes [value] to [buffer] by first writing a type discriminator byte, then the value itself.

This method may be called recursively to serialize container values.

Type discriminators 0 through 127 inclusive are reserved for use by the base class, as follows:

- null = 0
- true = 1
- false = 2
- 32 bit integer = 3
- 64 bit integer = 4
- larger integers = 5 (see below)
- 64 bit floating-point number = 6
- String = 7
- Uint8List = 8
- Int32List = 9
- Int64List = 10
- Float64List = 11
- List = 12
- Map = 13
- Float32List = 14
- Reserved for future expansion: 15..127

The codec can be extended by overriding this method, calling super for values that the extension does not handle. Type discriminators used by extensions must be greater than or equal to 128 in order to avoid clashes with any later extensions to the base class.

The "larger integers" type, 5, is never used by [writeValue]. A subclass could represent big integers from another package using that type. The format is first the type byte (0x05), then the actual number as an ASCII string giving the hexadecimal representation of the integer, with the string's length as encoded by [writeSize] followed by the string bytes. On Android, that would get converted to a `java.math.BigInteger` object. On iOS, the string representation is returned.

### readValue()

```dart
Object? readValue(ReadBuffer buffer)
```

Reads a value from [buffer] as written by [writeValue].

This method is intended for use by subclasses overriding [readValueOfType].

### readValueOfType()

```dart
Object? readValueOfType(int type, ReadBuffer buffer)
```

Reads a value of the indicated [type] from [buffer].

The codec can be extended by overriding this method, calling super for types that the extension does not handle. See the discussion at [writeValue].

### writeSize()

```dart
void writeSize(WriteBuffer buffer, int value)
```

Writes a non-negative 32-bit integer [value] to [buffer] using an expanding 1-5 byte encoding that optimizes for small values.

This method is intended for use by subclasses overriding [writeValue].

### readSize()

```dart
int readSize(ReadBuffer buffer)
```

Reads a non-negative int from [buffer] as written by [writeSize].

This method is intended for use by subclasses overriding [readValueOfType].

# StandardMethodCodec

```dart
class StandardMethodCodec implements MethodCodec {}
```

[MethodCodec] using the Flutter standard binary encoding.

The standard codec is guaranteed to be compatible with the corresponding standard codec for FlutterMethodChannels on the host platform. These parts of the Flutter SDK are evolved synchronously.

Values supported as method arguments and result payloads are those supported by [StandardMessageCodec].

### StandardMethodCodec()

```dart
StandardMethodCodec([StandardMessageCodec messageCodec = const StandardMessageCodec()])
```

Creates a [MethodCodec] using the Flutter standard binary encoding.

### messageCodec

```dart
StandardMessageCodec messageCodec
```

The message codec that this method codec uses for encoding values.

### encodeMethodCall()

```dart
ByteData encodeMethodCall(MethodCall methodCall)
```

### decodeMethodCall()

```dart
MethodCall decodeMethodCall(ByteData? methodCall)
```

### encodeSuccessEnvelope()

```dart
ByteData encodeSuccessEnvelope(Object? result)
```

### encodeErrorEnvelope()

```dart
ByteData encodeErrorEnvelope({required String code, String? message, Object? details})
```

### decodeEnvelope()

```dart
dynamic decodeEnvelope(ByteData envelope)
```
