# Paint

{% embed url="https://api.flutter.dev/flutter/dart-ui/Paint-class.html" %}



## CustomPaint

{% embed url="https://api.flutter.dev/flutter/widgets/CustomPaint-class.html" %}

<img src="../../../.gitbook/assets/image (39).png" alt="" data-size="original">

<img src="../../../.gitbook/assets/image (107).png" alt="" data-size="original">



## CustomPainter

{% embed url="https://api.flutter.dev/flutter/rendering/CustomPainter-class.html" %}

사용자 정의 페인터 구현

![](<../../../.gitbook/assets/image (62).png>)







### Paint 에 그러데이션 적용

{% embed url="https://stackoverflow.com/questions/60019684/use-gradient-with-paint-object-in-flutter-canvas" %}

```dart
import 'package:flutter/painting.dart';

// In your paint method
final paint = Paint()
  ..shader = RadialGradient(
    colors: [
      color1,
      color2,
    ],
  ).createShader(Rect.fromCircle(
    center: offset,
    radius: radius,
  ));
```

