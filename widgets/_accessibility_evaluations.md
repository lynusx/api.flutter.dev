# Violation

```dart
class Violation {}
```

{@template flutter.widgets.accessibility_evaluations.internal} Do not use in production.

Flutter will make breaking changes to this API, even in patch versions. {@endtemplate}

A violation of a semantics node.

### Violation()

```dart
Violation(SemanticsNode node, String reason)
```

Creates a violation.

### node

```dart
SemanticsNode node
```

The semantics node that violates the policy.

### reason

```dart
String reason
```

The reason for the violation.

# EvaluationResult

```dart
class EvaluationResult {}
```

{@macro flutter.widgets.accessibility_evaluations.internal}

The result of evaluating a semantics node by an [AccessibilityEvaluation].

### EvaluationResult()

```dart
EvaluationResult(List<Violation> violations)
```

Creates a passing evaluation.

### violations

```dart
List<Violation> violations
```

A list of violations found. An empty list means the evaluation passed.

# AccessibilityEvaluation

```dart
abstract class AccessibilityEvaluation {}
```

{@macro flutter.widgets.accessibility_evaluations.internal}

A class that evaluates a single accessibility rule.

### AccessibilityEvaluation()

```dart
AccessibilityEvaluation()
```

A const constructor allows subclasses to be const.

### evaluate()

```dart
FutureOr<EvaluationResult> evaluate(WidgetsBinding binding)
```

Evaluate whether the current state of the `binding` conforms to the rule.

# MinimumTapTargetEvaluation

```dart
class MinimumTapTargetEvaluation extends AccessibilityEvaluation {}
```

{@macro flutter.widgets.accessibility_evaluations.internal}

An evaluation which enforces that all tappable semantics nodes have a minimum size.

### MinimumTapTargetEvaluation()

```dart
MinimumTapTargetEvaluation({required Size size})
```

Create a new [MinimumTapTargetEvaluation].

### size

```dart
Size size
```

The minimum allowed size of a tappable node.

### shouldSkipNode()

```dart
bool shouldSkipNode(SemanticsNode node)
```

Returns whether [SemanticsNode] should be skipped for minimum tap target evaluation.

Skips nodes which are link, hidden, or do not have actions.

# LabeledTapTargetEvaluation

```dart
class LabeledTapTargetEvaluation extends AccessibilityEvaluation {}
```

{@macro flutter.widgets.accessibility_evaluations.internal}

An evaluation which enforces that all nodes with a tap or long press action also have a label.

### LabeledTapTargetEvaluation()

```dart
LabeledTapTargetEvaluation()
```

# MinimumTextContrastEvaluation

```dart
class MinimumTextContrastEvaluation extends _ContrastEvaluation {}
```

{@macro flutter.widgets.accessibility_evaluations.internal}

An evaluation which verifies that all nodes that contribute semantics via text meet minimum contrast levels.

The evaluations are defined by the Web Content Accessibility Guidelines, http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html.

### MinimumTextContrastEvaluation()

```dart
MinimumTextContrastEvaluation({required double minNormalTextContrastRatio, required double minLargeTextContrastRatio})
```

Create a new [MinimumTextContrastEvaluation].

### minNormalTextContrastRatio

```dart
double minNormalTextContrastRatio
```

The minimum contrast ratio for normal text.

Normal text is text that is smaller than [kLargeTextMinimumSize] (18.0) or smaller than [kBoldTextMinimumSize] (14.0) if bold.

### minLargeTextContrastRatio

```dart
double minLargeTextContrastRatio
```

The minimum contrast ratio for large text.

Large text is text that is at least [kLargeTextMinimumSize] (18.0) or at least [kBoldTextMinimumSize] (14.0) if bold.

### kLargeTextMinimumSize

```dart
int kLargeTextMinimumSize
```

The minimum text size considered large for contrast checking.

Defined by http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html

### kBoldTextMinimumSize

```dart
int kBoldTextMinimumSize
```

The minimum text size for bold text to be considered large for contrast checking.

Defined by http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html

### kMinimumRatioNormalText

```dart
double kMinimumRatioNormalText
```

The minimum contrast ratio for normal text.

Defined by http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html

### kMinimumRatioLargeText

```dart
double kMinimumRatioLargeText
```

The minimum contrast ratio for large text.

Defined by http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html

### evaluateNodeContent()

```dart
Future<List<Violation>> evaluateNodeContent(SemanticsNode node, SemanticsData data, ui.Image image, ByteData byteData, RenderView renderView)
```

# MinimumNonTextContrastEvaluation

```dart
class MinimumNonTextContrastEvaluation extends _ContrastEvaluation {}
```

{@macro flutter.widgets.accessibility_evaluations.internal}

An evaluation which verifies that all nodes that represent non-text controls meet minimum contrast levels of 3.0.

The evaluations are defined by the Web Content Accessibility Guidelines, https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html

### MinimumNonTextContrastEvaluation()

```dart
MinimumNonTextContrastEvaluation()
```

Create a new [MinimumNonTextContrastEvaluation].

### evaluateNodeContent()

```dart
Future<List<Violation>> evaluateNodeContent(SemanticsNode node, SemanticsData data, ui.Image image, ByteData byteData, RenderView renderView)
```

# UnlabeledLeafNodeEvaluation

```dart
class UnlabeledLeafNodeEvaluation extends AccessibilityEvaluation {}
```

{@macro flutter.widgets.accessibility_evaluations.internal}

An evaluation which enforces that all leaf semantics nodes have a label, value, hint, or tooltip.

### UnlabeledLeafNodeEvaluation()

```dart
UnlabeledLeafNodeEvaluation()
```

# TitleEvaluation

```dart
class TitleEvaluation extends AccessibilityEvaluation {}
```

{@macro flutter.widgets.accessibility_evaluations.internal}

An evaluation which enforces that the application has at least one [Title] widget to set the web page title.

### TitleEvaluation()

```dart
TitleEvaluation()
```

Create a new [TitleEvaluation].
