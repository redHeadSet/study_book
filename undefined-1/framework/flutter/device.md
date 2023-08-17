# Device

## MediaQuery.of(context)

cf. MediaQuery 가 없는 경우, of 함수가 예외를 던질 수 있다.\
maybeOf 함수를 사용하여 없는 경우에 null 을 반환하도록 할 수 있다.



### size

현재 창의 너비와 높이 처리 시 유용

```dart
MediaQuery.of(context).size.width     // 너비
MediaQuery.of(context).size.height    // 높이
```

하지만 플러터에서 모든 값이 픽셀 단위의 절대값으로 처리되기 때문에, 화면 비율상의 어떠한 처리를 위해서는 가로-세로 비율 처리가 필요함.

ex. responsive\_sizer

{% embed url="https://pub.dev/packages/responsive_sizer" %}



### Padding, viewPadding, viewInsets

{% embed url="https://velog.io/@cyb9701/Flutter-MediaQuery%EC%9D%98-padding-viewPadding-%EC%99%80-viewInsets" %}

* Android 에서는 문제없이 전체적인 프레임이 정상 표시되지만, ios 의 노치 + 다이나믹 아일랜드 모델의 경우에 표시상의 문제가 발생하여 찾아보게 됨
* MediaQuery 등을 사용하여 디바이스 화면 크기를 알아내게 되는데, 이 화면에는 상단바나 노치, 하단 바의 넓이가 포함되어 있기에 비정상적으로 표시될 수 있는 걸로 보인다.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><img src="../../../.gitbook/assets/image (103).png" alt="" data-size="original"></td><td></td><td></td></tr><tr><td><img src="../../../.gitbook/assets/image (34).png" alt="" data-size="original"></td><td></td><td></td></tr></tbody></table>

* 검은 색 영역 : 앱이 그릴 수 없는 시스템 UI (padding) (완전히 보이지 않을 수 있는 영역)
* 빨간 색 영역 : 제스처를 감지하지 못하고 그리기를 원하지 않을 수 있는 영역 (viewPadding)
* 회색 영역 : 시스템 키보드 (viewInsets) - 키보드가 열렸을 경우에만 값이 0보다 크게 나옴

viewPadding, viewInsets 값은 서로 무관\
padding 은 viewPadding, viewInsets 값에서 파생됨

but, padding 영역에 다른 값이 보여지고 있다면 (viewInsets 의 키보드라던지...) 이 값은 0으로 변경됨





## Platform

```dart
import 'dart:io' show Platform;

Platform.isAndroid
Platform.isFuchsia
Platform.isIOS
Platform.isLinux
Platform.isMacOS
Platform.isWindows

// 웹 확인이 필요한 경우
import 'package:flutter/foundation.dart' show kIsWeb
if (kIsWeb) { ... }
```

```dart
Theme.of(context).platform == TargetPlatform.iOS
```



