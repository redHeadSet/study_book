# ButtonStyle

{% embed url="https://api.flutter.dev/flutter/material/ButtonStyle-class.html" %}



```dart
ButtonStyle appbarButtonStyle() {
    var buttonSizeWidth = Adaptive.w(appbarButtonSizeWidthRatio);
    var buttonSizeHeight = Adaptive.h(appbarButtonSizeHeightRatio);
    var buttonIconSize = buttonSizeWidth * 0.9;

    return ButtonStyle(
      minimumSize:
          MaterialStateProperty.all(Size(buttonSizeWidth, buttonSizeHeight)),
      fixedSize:
          MaterialStateProperty.all(Size(buttonSizeWidth, buttonSizeHeight)),
      iconSize: MaterialStateProperty.all(buttonIconSize),
      padding: MaterialStateProperty.all(EdgeInsets.zero),
      shape: MaterialStateProperty.all(
        RoundedRectangleBorder(
          borderRadius: BorderRadius.circular(8.0),
        ),
      ),
      foregroundColor: MaterialStateColor.resolveWith((states) {
        if (states.contains(MaterialState.pressed)) {
          return Colors.blue;
        } else {
          return Colors.white;
        }
      }),
      backgroundColor:
          MaterialStateProperty.all(const Color.fromRGBO(255, 255, 255, 0.3)),
    );
  }
```

* ButtonStyle 의 minimumSize 값은 기본 값이 있다. 작은 버튼을 구현하고 싶다면 해당 값을 조정해야 함.
* Button의 Size 와 버튼 내의 IconSize 값은 별도로 설정이 가능하다 (위에서는 버튼의 90% 사이즈로 설정)
* shape 등을 사용하여 버튼 모양을 디테일하게 변경 가능
* state 값을 이용하여 클릭 이벤트 등에 대해 버튼 모양을 유동적으로 변경이 가능



| 모양                                            | 코드                                                                                                    |
| --------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| ![](<../../../.gitbook/assets/image (4).png>) | <ol><li>ElevatedButton()</li><li>TextButton()</li><li>OutlinedButton()</li><li>IconButton()</li></ol> |

1.  ElevatedButton

    기본 색깔 있는 일반적인 버튼 형태.
2. TextButton\
   버튼의 크기가 가늠되지 않는 형태. 눌렀을 때 버튼 액션 있음
3. OutlinedButton\
   외곽선이 가늘게 보이는 버튼 형태.
4. IconButton\
   특별한 액션을 지정하지 못하는 버튼 형태.



