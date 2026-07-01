# StepState

```dart
enum StepState {}
```

The state of a [Step] which is used to control the style of the circle and text.

See also:

- [Step]

A step that displays its index in its circle.

A step that displays a pencil icon in its circle.

A step that displays a tick icon in its circle.

A step that is disabled and does not to react to taps.

A step that is currently having an error. e.g. the user has submitted wrong input.

# StepperType

```dart
enum StepperType {}
```

Defines the [Stepper]'s main axis.

A vertical layout of the steps with their content in-between the titles.

A horizontal layout of the steps with their content below the titles.

# ControlsDetails

```dart
class ControlsDetails {}
```

Container for all the information necessary to build a Stepper widget's forward and backward controls for any given step.

Used by [Stepper.controlsBuilder].

### ControlsDetails()

```dart
ControlsDetails({required int currentStep, required int stepIndex, VoidCallback? onStepCancel, VoidCallback? onStepContinue})
```

Creates a set of details describing the Stepper.

### currentStep

```dart
int currentStep
```

Index that is active for the surrounding [Stepper] widget. This may be different from [stepIndex] if the user has just changed steps and we are currently animating toward that step.

### stepIndex

```dart
int stepIndex
```

Index of the step for which these controls are being built. This is not necessarily the active index, if the user has just changed steps and this step is animating away. To determine whether a given builder is building the active step or the step being navigated away from, see [isActive].

### onStepContinue

```dart
VoidCallback? onStepContinue
```

The callback called when the 'continue' button is tapped.

If null, the 'continue' button will be disabled.

### onStepCancel

```dart
VoidCallback? onStepCancel
```

The callback called when the 'cancel' button is tapped.

If null, the 'cancel' button will be disabled.

### isActive

```dart
bool get isActive
```

True if the indicated step is also the current active step. If the user has just activated the transition to a new step, some [Stepper.type] values will lead to both steps being rendered for the duration of the animation shifting between steps.

# ControlsWidgetBuilder

```dart
typedef ControlsWidgetBuilder = Widget Function(BuildContext context, ControlsDetails details)
```

A builder that creates a widget given the two callbacks `onStepContinue` and `onStepCancel`.

Used by [Stepper.controlsBuilder].

See also:

- [WidgetBuilder], which is similar but only takes a [BuildContext].

# StepIconBuilder

```dart
typedef StepIconBuilder = Widget? Function(int stepIndex, StepState stepState)
```

A builder that creates the icon widget for the [Step] at [stepIndex], given [stepState].

# Step

```dart
class Step {}
```

A material step used in [Stepper]. The step can have a title and subtitle, an icon within its circle, some content and a state that governs its styling.

See also:

- [Stepper]
- <https://material.io/archive/guidelines/components/steppers.html>

### Step()

```dart
Step({required Widget title, Widget? subtitle, required Widget content, StepState state = StepState.indexed, bool isActive = false, Widget? label, StepStyle? stepStyle})
```

Creates a step for a [Stepper].

### title

```dart
Widget title
```

The title of the step that typically describes it.

### subtitle

```dart
Widget? subtitle
```

The subtitle of the step that appears below the title and has a smaller font size. It typically gives more details that complement the title.

If null, the subtitle is not shown.

### content

```dart
Widget content
```

The content of the step that appears below the [title] and [subtitle].

Below the content, every step has a 'continue' and 'cancel' button.

### state

```dart
StepState state
```

The state of the step which determines the styling of its components and whether steps are interactive.

### isActive

```dart
bool isActive
```

Whether or not the step is active. The flag only influences styling.

### label

```dart
Widget? label
```

Only [StepperType.horizontal], Optional widget that appears under the [title]. By default, uses the `bodyLarge` theme.

### stepStyle

```dart
StepStyle? stepStyle
```

Optional overrides for the step's default visual configuration.

# Stepper

```dart
class Stepper extends StatefulWidget {}
```

A material stepper widget that displays progress through a sequence of steps. Steppers are particularly useful in the case of forms where one step requires the completion of another one, or where multiple steps need to be completed in order to submit the whole form.

The widget is a flexible wrapper. A parent class should pass [currentStep] to this widget based on some logic triggered by the three callbacks that it provides.

{@tool dartpad} An example the shows how to use the [Stepper], and the [Stepper] UI appearance.

** See code in examples/api/lib/material/stepper/stepper.0.dart ** {@end-tool}

See also:

- [Step]
- <https://material.io/archive/guidelines/components/steppers.html>

### Stepper()

```dart
Stepper({dynamic key, required List<Step> steps, ScrollController? controller, ScrollPhysics? physics, StepperType type = StepperType.vertical, int currentStep = 0, ValueChanged<int>? onStepTapped, VoidCallback? onStepContinue, VoidCallback? onStepCancel, ControlsWidgetBuilder? controlsBuilder, double? elevation, EdgeInsetsGeometry? margin, WidgetStateProperty<Color>? connectorColor, double? connectorThickness, StepIconBuilder? stepIconBuilder, double? stepIconHeight, double? stepIconWidth, EdgeInsets? stepIconMargin, Clip clipBehavior = Clip.none, EdgeInsetsGeometry? headerPadding, EdgeInsetsGeometry? contentPadding})
```

Creates a stepper from a list of steps.

This widget is not meant to be rebuilt with a different list of steps unless a key is provided in order to distinguish the old stepper from the new one.

### steps

```dart
List<Step> steps
```

The steps of the stepper whose titles, subtitles, icons always get shown.

The length of [steps] must not change.

### physics

```dart
ScrollPhysics? physics
```

How the stepper's scroll view should respond to user input.

For example, determines how the scroll view continues to animate after the user stops dragging the scroll view.

If the stepper is contained within another scrollable it can be helpful to set this property to [ClampingScrollPhysics].

### controller

```dart
ScrollController? controller
```

An object that can be used to control the position to which this scroll view is scrolled.

To control the initial scroll offset of the scroll view, provide a [controller] with its [ScrollController.initialScrollOffset] property set.

### type

```dart
StepperType type
```

The type of stepper that determines the layout. In the case of [StepperType.horizontal], the content of the current step is displayed underneath as opposed to the [StepperType.vertical] case where it is displayed in-between.

### currentStep

```dart
int currentStep
```

The index into [steps] of the current step whose content is displayed.

### onStepTapped

```dart
ValueChanged<int>? onStepTapped
```

The callback called when a step is tapped, with its index passed as an argument.

### onStepContinue

```dart
VoidCallback? onStepContinue
```

The callback called when the 'continue' button is tapped.

If null, the 'continue' button will be disabled.

### onStepCancel

```dart
VoidCallback? onStepCancel
```

The callback called when the 'cancel' button is tapped.

If null, the 'cancel' button will be disabled.

### controlsBuilder

```dart
ControlsWidgetBuilder? controlsBuilder
```

The callback for creating custom controls.

If null, the default controls from the current theme will be used.

This callback which takes in a context and a [ControlsDetails] object, which contains step information and two functions: [onStepContinue] and [onStepCancel]. These can be used to control the stepper. For example, reading the [ControlsDetails.currentStep] value within the callback can change the text of the continue or cancel button depending on which step users are at.

{@tool dartpad} Creates a stepper control with custom buttons.

```dart
Widget build(BuildContext context) {
  return Stepper(
    controlsBuilder:
      (BuildContext context, ControlsDetails details) {
         return Row(
           children: <Widget>[
             TextButton(
               onPressed: details.onStepContinue,
               child: Text('Continue to Step ${details.stepIndex + 1}'),
             ),
             TextButton(
               onPressed: details.onStepCancel,
               child: Text('Back to Step ${details.stepIndex - 1}'),
             ),
           ],
         );
      },
    steps: const <Step>[
      Step(
        title: Text('A'),
        content: SizedBox(
          width: 100.0,
          height: 100.0,
        ),
      ),
      Step(
        title: Text('B'),
        content: SizedBox(
          width: 100.0,
          height: 100.0,
        ),
      ),
    ],
  );
}
```

** See code in examples/api/lib/material/stepper/stepper.controls_builder.0.dart ** {@end-tool}

### elevation

```dart
double? elevation
```

The elevation of this stepper's [Material] when [type] is [StepperType.horizontal].

### margin

```dart
EdgeInsetsGeometry? margin
```

Custom margin on vertical stepper.

### connectorColor

```dart
WidgetStateProperty<Color>? connectorColor
```

Customize connected lines colors.

Resolves in the following states:

- [WidgetState.selected].
- [WidgetState.disabled].

If not set then the widget will use default colors, primary for selected state and grey.shade400 for disabled state.

### connectorThickness

```dart
double? connectorThickness
```

The thickness of the connecting lines.

### stepIconBuilder

```dart
StepIconBuilder? stepIconBuilder
```

Callback for creating custom icons for the [steps].

When overriding icon for [StepState.error], please return a widget whose width and height are 14 pixels or less to avoid overflow.

If null, the default icons will be used for respective [StepState].

### stepIconHeight

```dart
double? stepIconHeight
```

Overrides the default step icon size height.

### stepIconWidth

```dart
double? stepIconWidth
```

Overrides the default step icon size width.

### stepIconMargin

```dart
EdgeInsets? stepIconMargin
```

Overrides the default step icon margin.

### clipBehavior

```dart
Clip clipBehavior
```

The [Step.content] will be clipped to this Clip type.

Defaults to [Clip.none].

See also:

- [Clip], which explains how to use this property.

### headerPadding

```dart
EdgeInsetsGeometry? headerPadding
```

The padding around the header row in both [StepperType.vertical] and [StepperType.horizontal] steppers.

Defaults to to `EdgeInsets.symmetric(horizontal: 24.0)`.

### contentPadding

```dart
EdgeInsetsGeometry? contentPadding
```

The padding around the content area in both [StepperType.vertical] and [StepperType.horizontal] steppers.

For [StepperType.horizontal], defaults to `EdgeInsets.all(24.0)`.

For [StepperType.vertical], defaults to `EdgeInsetsDirectional.only(start: 60.0, end: 24.0, bottom: 24.0)`. The `start` padding is also increased by the `left` value of [stepIconMargin] if it is provided.

### createState()

```dart
State<Stepper> createState()
```

# StepStyle

```dart
class StepStyle with Diagnosticable {}
```

This class is used to override the default visual properties of [Step] widgets within a [Stepper].

To customize the appearance of a [Step] create an instance of this class with non-null parameters for the step properties whose default value you want to override.

Example usage:

```dart
Step(
  title: const Text('Step 1'),
  content: const Text('Content for Step 1'),
  stepStyle: StepStyle(
    color: Colors.blue,
    errorColor: Colors.red,
    border: Border.all(color: Colors.grey),
    boxShadow: const BoxShadow(blurRadius: 3.0, color: Colors.black26),
    gradient: const LinearGradient(colors: <Color>[Colors.red, Colors.blue]),
    indexStyle: const TextStyle(color: Colors.white),
  ),
)
```

{@tool dartpad} An example that uses [StepStyle] to customize the appearance of each [Step] in a [Stepper].

** See code in examples/api/lib/material/stepper/step_style.0.dart ** {@end-tool}

### StepStyle()

```dart
StepStyle({Color? color, Color? errorColor, Color? connectorColor, double? connectorThickness, BoxBorder? border, BoxShadow? boxShadow, Gradient? gradient, TextStyle? indexStyle})
```

Constructs a [StepStyle].

### color

```dart
Color? color
```

Overrides the default color of the circle in the step.

### errorColor

```dart
Color? errorColor
```

Overrides the default color of the error indicator in the step.

### connectorColor

```dart
Color? connectorColor
```

Overrides the default color of the connector line between two steps.

This property only applies when [Stepper.type] is [StepperType.horizontal].

### connectorThickness

```dart
double? connectorThickness
```

Overrides the default thickness of the connector line between two steps.

This property only applies when [Stepper.type] is [StepperType.horizontal].

### border

```dart
BoxBorder? border
```

Add a border around the step.

Will be applied to the circle in the step.

### boxShadow

```dart
BoxShadow? boxShadow
```

Add a shadow around the step.

### gradient

```dart
Gradient? gradient
```

Add a gradient around the step.

If [gradient] is specified, [color] will be ignored.

### indexStyle

```dart
TextStyle? indexStyle
```

Overrides the default style of the index in the step.

### copyWith()

```dart
StepStyle copyWith({Color? color, Color? errorColor, Color? connectorColor, double? connectorThickness, BoxBorder? border, BoxShadow? boxShadow, Gradient? gradient, TextStyle? indexStyle})
```

Returns a copy of this ButtonStyle with the given fields replaced with the new values.

### merge()

```dart
StepStyle merge(StepStyle? stepStyle)
```

Returns a copy of this StepStyle where the non-null fields in [stepStyle] have replaced the corresponding null fields in this StepStyle.

In other words, [stepStyle] is used to fill in unspecified (null) fields this StepStyle.

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
