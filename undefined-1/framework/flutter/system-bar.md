# System bar 숨기기

{% embed url="https://api.flutter.dev/flutter/services/SystemChrome/setEnabledSystemUIMode.html" %}

setEnabledSystemUIMode

{% embed url="https://api.flutter.dev/flutter/services/SystemUiMode.html" %}



```dart
// sample 1
SystemChrome.setEnabledSystemUIMode(SystemUiMode.immersive);

// sample 2 - 하단 바만 보이게
SystemChrome.setEnabledSystemUIMode(
  SystemUiMode.manual,
  overlays: [
    SystemUiOverlay.bottom,
  ],
);
```

| 설정 없는 경우                                        | SystemUiMode.immersive                                                  | SystemUiMode.manual                              |
| ----------------------------------------------- | ----------------------------------------------------------------------- | ------------------------------------------------ |
| ![](<../../../.gitbook/assets/image (120).png>) | ![](<../../../.gitbook/assets/image (121).png>)                         |                                                  |
|                                                 | <p>몰입형 UI<br><code>immersiveSticky</code> 사용 시, 가장자리 스와이프로 불러낼 수 있음</p> | 위 샘플 코드와 같이 SystemUiOverlay 값을 사용하여 선택적으로 보이게 가능 |





