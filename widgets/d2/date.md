# SelectableDayPredicate

```dart
typedef SelectableDayPredicate = bool Function(DateTime day)
```

用于判断某个日期是否可被选中的谓词函数签名。

参见 [showDatePicker](https://www.yuque.com/thyname/flutter.material/showdatepicker) 和 [showCupertinoModalPopup](https://www.yuque.com/thyname/flutter.cupertino/showcupertinomodalpopup)，它们都拥有一个 [SelectableDayPredicate](https://www.yuque.com/thyname/flutter.widgets/selectabledaypredicate) 参数，用于指定日期选择器中允许选择的日期。
