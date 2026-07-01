@docImport 'package:flutter/rendering.dart';

# MatrixUtils

```dart
abstract final class MatrixUtils {}
```

Utility functions for working with matrices.

### getAsTranslation()

```dart
Offset? getAsTranslation(Matrix4 transform)
```

Returns the given [transform] matrix as an [Offset], if the matrix is nothing but a 2D translation.

Otherwise, returns null.

### getAsScale()

```dart
double? getAsScale(Matrix4 transform)
```

Returns the given [transform] matrix as a [double] describing a uniform scale, if the matrix is nothing but a symmetric 2D scale transform.

Otherwise, returns null.

### multiplyInPlace()

```dart
void multiplyInPlace(Matrix4 a, Matrix4 b)
```

Computes the result of matrix multiplication `a x b` and stores the result in `b`.

This function does not alter the argument `a`, and is thus useful when you want to left-multiply in-place. For right-multiply in-place, see [Matrix4.multiply].

### matrixEquals()

```dart
bool matrixEquals(Matrix4? a, Matrix4? b)
```

Returns true if the given matrices are exactly equal, and false otherwise. Null values are assumed to be the identity matrix.

### isIdentity()

```dart
bool isIdentity(Matrix4 a)
```

Whether the given matrix is the identity matrix.

### transformPoint()

```dart
Offset transformPoint(Matrix4 transform, Offset point)
```

Applies the given matrix as a perspective transform to the given point.

This function assumes the given point has a z-coordinate of 0.0. The z-coordinate of the result is ignored.

While not common, this method may return (NaN, NaN), iff the given `point` results in a "point at infinity" in homogeneous coordinates after applying the `transform`. For example, a [RenderObject] may set its transform to the zero matrix to indicate its content is currently not visible. Trying to convert an `Offset` to its coordinate space always results in (NaN, NaN).

### transformRect()

```dart
Rect transformRect(Matrix4 transform, Rect rect)
```

Returns a rect that bounds the result of applying the given matrix as a perspective transform to the given rect.

This function assumes the given rect is in the plane with z equals 0.0. The transformed rect is then projected back into the plane with z equals 0.0 before computing its bounding rect.

### inverseTransformRect()

```dart
Rect inverseTransformRect(Matrix4 transform, Rect rect)
```

Returns a rect that bounds the result of applying the inverse of the given matrix as a perspective transform to the given rect.

This function assumes the given rect is in the plane with z equals 0.0. The transformed rect is then projected back into the plane with z equals 0.0 before computing its bounding rect.

### createCylindricalProjectionTransform()

```dart
Matrix4 createCylindricalProjectionTransform({required double radius, required double angle, double perspective = 0.001, Axis orientation = Axis.vertical})
```

Create a transformation matrix which mimics the effects of tangentially wrapping the plane on which this transform is applied around a cylinder and then looking at the cylinder from a point outside the cylinder.

The `radius` simulates the radius of the cylinder the plane is being wrapped onto. If the transformation is applied to a 0-dimensional dot instead of a plane, the dot would translate by ± `radius` pixels along the `orientation` [Axis] when rotating from 0 to ±90 degrees.

A positive radius means the object is closest at 0 `angle` and a negative radius means the object is closest at π `angle` or 180 degrees.

The `angle` argument is the difference in angle in radians between the object and the viewing point. A positive `angle` on a positive `radius` moves the object up when `orientation` is vertical and right when horizontal.

The transformation is always done such that a 0 `angle` keeps the transformed object at exactly the same size as before regardless of `radius` and `perspective` when `radius` is positive.

The `perspective` argument is a number between 0 and 1 where 0 means looking at the object from infinitely far with an infinitely narrow field of view and 1 means looking at the object from infinitely close with an infinitely wide field of view. Defaults to a sane but arbitrary 0.001.

The `orientation` is the direction of the rotation axis.

Because the viewing position is a point, it's never possible to see the outer side of the cylinder at or past ±π/2 or 90 degrees and it's almost always possible to end up seeing the inner side of the cylinder or the back side of the transformed plane before π / 2 when perspective > 0.

### forceToPoint()

```dart
Matrix4 forceToPoint(Offset offset)
```

Returns a matrix that transforms every point to [offset].

# debugDescribeTransform()

```dart
List<String> debugDescribeTransform(Matrix4? transform)
```

Returns a list of strings representing the given transform in a format useful for [TransformProperty].

If the argument is null, returns a list with the single string "null".

# TransformProperty

```dart
class TransformProperty extends DiagnosticsProperty<Matrix4> {}
```

Property which handles [Matrix4] that represent transforms.

### TransformProperty()

```dart
TransformProperty(String name, dynamic value, {dynamic showName, dynamic defaultValue, dynamic level})
```

Create a diagnostics property for [Matrix4] objects.

### valueToString()

```dart
String valueToString({TextTreeConfiguration? parentConfiguration})
```
