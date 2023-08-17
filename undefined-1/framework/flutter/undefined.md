# 그 외

Scaffold 에서 body 와 bottomNavigationBar 는 서로 같은 z축에 위치해있다\
→ 한 쪽이 커지면, 한 쪽이 작아지는 형태\
→ Stack 형태가 아니다



Navigation.pop 처리 전에 canpop 을 확인하고 처리하는 게 안전하다.\
cf. 일부러 모든 위젯을 날리기 위해 pop 처리를 할 수도 있긴 하다.



서로 다른 위젯 간 통신을 위해 고려할 수 있는 것

1. StreamController
2. ValueNotifier (ValueListenableBuilder)



Flutter 는 각 위젯의 크기를 pixel 단위로 처리한다 [\[링크\]](device.md#size)\
→ 그렇기에, dp 와 같이 비율 처리를 하기 위해서는 MediaQuery 등을 이용한 width-height 를 받아 처리해야 함

\=> [https://pub.dev/packages/flutter\_adaptive\_ui](https://pub.dev/packages/flutter\_adaptive\_ui)\
위와 같은 방법으로 비율 처리도 가능하다

