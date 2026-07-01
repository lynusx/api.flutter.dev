# WriteBuffer

```dart
class WriteBuffer {}
```

Write-only buffer for incrementally building a [ByteData] instance.

A WriteBuffer instance can be used only once. Attempts to reuse will result in [StateError]s being thrown.

The byte order used is [Endian.host] throughout.

### WriteBuffer()

```dart
WriteBuffer({int startCapacity = 8})
```

Creates an interface for incrementally building a [ByteData] instance.

[startCapacity] determines the start size of the [WriteBuffer] in bytes. The closer that value is to the real size used, the better the performance.

### putUint8()

```dart
void putUint8(int byte)
```

Write a Uint8 into the buffer.

### putUint16()

```dart
void putUint16(int value, {Endian? endian})
```

Write a Uint16 into the buffer.

### putUint32()

```dart
void putUint32(int value, {Endian? endian})
```

Write a Uint32 into the buffer.

### putInt32()

```dart
void putInt32(int value, {Endian? endian})
```

Write an Int32 into the buffer.

### putInt64()

```dart
void putInt64(int value, {Endian? endian})
```

Write an Int64 into the buffer.

### putFloat64()

```dart
void putFloat64(double value, {Endian? endian})
```

Write an Float64 into the buffer.

### putUint8List()

```dart
void putUint8List(Uint8List list)
```

Write all the values from a [Uint8List] into the buffer.

### putInt32List()

```dart
void putInt32List(Int32List list)
```

Write all the values from an [Int32List] into the buffer.

### putInt64List()

```dart
void putInt64List(Int64List list)
```

Write all the values from an [Int64List] into the buffer.

### putFloat32List()

```dart
void putFloat32List(Float32List list)
```

Write all the values from a [Float32List] into the buffer.

### putFloat64List()

```dart
void putFloat64List(Float64List list)
```

Write all the values from a [Float64List] into the buffer.

### done()

```dart
ByteData done()
```

Finalize and return the written [ByteData].

# ReadBuffer

```dart
class ReadBuffer {}
```

Read-only buffer for reading sequentially from a [ByteData] instance.

The byte order used is [Endian.host] throughout.

### ReadBuffer()

```dart
ReadBuffer(ByteData data)
```

Creates a [ReadBuffer] for reading from the specified [data].

### data

```dart
ByteData data
```

The underlying data being read.

### hasRemaining

```dart
bool get hasRemaining
```

Whether the buffer has data remaining to read.

### getUint8()

```dart
int getUint8()
```

Reads a Uint8 from the buffer.

### getUint16()

```dart
int getUint16({Endian? endian})
```

Reads a Uint16 from the buffer.

### getUint32()

```dart
int getUint32({Endian? endian})
```

Reads a Uint32 from the buffer.

### getInt32()

```dart
int getInt32({Endian? endian})
```

Reads an Int32 from the buffer.

### getInt64()

```dart
int getInt64({Endian? endian})
```

Reads an Int64 from the buffer.

### getFloat64()

```dart
double getFloat64({Endian? endian})
```

Reads a Float64 from the buffer.

### getUint8List()

```dart
Uint8List getUint8List(int length)
```

Reads the given number of Uint8s from the buffer.

### getInt32List()

```dart
Int32List getInt32List(int length)
```

Reads the given number of Int32s from the buffer.

### getInt64List()

```dart
Int64List getInt64List(int length)
```

Reads the given number of Int64s from the buffer.

### getFloat32List()

```dart
Float32List getFloat32List(int length)
```

Reads the given number of Float32s from the buffer.

### getFloat64List()

```dart
Float64List getFloat64List(int length)
```

Reads the given number of Float64s from the buffer.
