# PolynomialFit

```dart
class PolynomialFit {}
```

An nth degree polynomial fit to a dataset.

### PolynomialFit()

```dart
PolynomialFit(int degree)
```

Creates a polynomial fit of the given degree.

There are n + 1 coefficients in a fit of degree n.

### coefficients

```dart
List<double> coefficients
```

The polynomial coefficients of the fit.

For each `i`, the element `coefficients[i]` is the coefficient of the `i`-th power of the variable.

### confidence

```dart
double confidence
```

An indicator of the quality of the fit.

Larger values indicate greater quality. The value ranges from 0.0 to 1.0.

The confidence is defined as the fraction of the dataset's variance that is captured by variance in the fit polynomial. In statistics textbooks this is often called "r-squared".

### toString()

```dart
String toString()
```

# LeastSquaresSolver

```dart
class LeastSquaresSolver {}
```

Uses the least-squares algorithm to fit a polynomial to a set of data.

### LeastSquaresSolver()

```dart
LeastSquaresSolver(List<double> x, List<double> y, List<double> w)
```

Creates a least-squares solver.

### x

```dart
List<double> x
```

The x-coordinates of each data point.

### y

```dart
List<double> y
```

The y-coordinates of each data point.

### w

```dart
List<double> w
```

The weight to use for each data point.

### solve()

```dart
PolynomialFit? solve(int degree)
```

Fits a polynomial of the given degree to the data points.

When there is not enough data to fit a curve null is returned.
