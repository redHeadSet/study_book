# Animation

## AnimationContainer

{% embed url="https://docs.flutter.dev/cookbook/animation/animated-container" %}

가장 간단한 Container 를 이용한 구현인 것으로 보인다



## Animation

### AnimationController

{% embed url="https://api.flutter.dev/flutter/animation/AnimationController-class.html" %}

1. 애니메이션을 정방향(forward) / 역방향(reverse) / 중지(stop) 가능
   * 애니메이션 완료 시 TickerFuture 반환
   * 애니메이션이 진행되는 동안의 상태는 AnimationStatus.forward
   * 애니메이션 종료 시에는 AnimationStatus.completed
2. 애니메이션을 특정 value 로 설정 가능
   * value 라는 내부 변수가 있고, 아마 애니메이션이 얼마나 진행되었는지에 대한 표시
     * lowerBound == 0 && upperBound == 1 일 때,\
       애니메이션이 절반 진행되었다면, value = 0.5&#x20;
   * 이 값은 lowerBound \~ upperBound 값 사이에 있음 (double 형)
   * 이를 설정하면 애니메이션이 즉시 중지 (TickerFuture.orCancel → TickerCanceled 오류)
   * 모든 리스너에게 value 값이 변경된 것을 알려서 수정되는 것으로 보임.
3. 애니메이션의 upperBound / lowerBound 값 정의
   * lowerBound : 최소값 - 시작
   * upperBound : 최대값 - 완료
4. 물리 시뮬레이션을 사용하여 fling 애니메이션 효과 적용

일반적으로 초당 60개의 값을 생성

생성 시, TickerProvider 필요

Stateful 위젯의 State 개체에서 AnimationController 가 생성되는 경우, \
State는 TickerProviderStateMixin, SingleTickerProviderStateMixin 을 사용하여 적합한 TickerProvider 를 얻을 수 있음

사용되지 않을 때 폐기하는 것이 누수에 유리\
→ initState 에서 생성 & dispose 에서 삭제



### Ticker

{% embed url="https://api.flutter.dev/flutter/scheduler/Ticker-class.html" %}

애니메이션 프레임 당 1번씩 콜백 호출

start, stop 은 Ticker 사용자가 처리

Ticker 의 제어는 TickerProvider 에서 담당

SchedulerBinding 에 의해 구동 ([SchedulerBinding.scheduleFrameCallback](https://api.flutter.dev/flutter/scheduler/SchedulerBinding/scheduleFrameCallback.html))

기본적으로 프레임이 트리거 될 때마다 알림을 받고자하는 모든 객체에서 사용이 가능하지만, 주로 AnimationController 에서 사용됨



### TickerProvider

{% embed url="https://api.flutter.dev/flutter/scheduler/TickerProvider-class.html" %}

Ticker 객체를 판매(?)하는 객체 → 제공하는 객체가 맞는 거 같음

Stateful 위젯의 State 개체에서 AnimationController 가 생성되는 경우, \
State는 TickerProviderStateMixin, SingleTickerProviderStateMixin 을 사용하여 적합한 TickerProvider 를 얻을 수 있음

#### SingleTickerProviderStateMixin

stateful widget 을 확장

단일 AnimationController 를 사용하는 경우, 이 클래스를 with 한 후 vsync에 this를 전달

단일 TickerProvider, 단일 AnimationController 만 지원

#### TickerProviderStateMixin

stateful widget 을 확장

새 AnimationController 를 생성할 때마다, vsync 에 this 전달



### Tween

{% embed url="https://api.flutter.dev/flutter/animation/Tween-class.html" %}

begin \~ end 지정하여 animation 의 진행을 구성 가능

ex) begin : Offset(100.0, 50.0), end : Offset(0.0, 100.0) 설정 시 Tween 을 기반으로 Animation 을 구성하면 해당 begin 위치에서 end 위치가지의 이동이 Animation 처리된다

```
_animation = Tween<Offset>(
  begin: const Offset(100.0, 50.0),
  end: const Offset(200.0, 300.0),
).animate(_controller);
```







<details>

<summary>Sample</summary>

특정 위치에서 다른 위치까지 움직이는 예제

```dart
class CustomBottomNavigationBar extends StatefulWidget {
  ...
}

class _CustomBottomNavigationBarState extends State<CustomBottomNavigationBar>
    with SingleTickerProviderStateMixin {
  late AnimationController _animationController;
  late Animation _bottomMoveAnimation;
  
  @override
  void initState() {
    _animationController = AnimationController(
      duration: Duration(milliseconds: 500),
      vsync: this,
    );
    super.initState();
  }
  
  @override
  Widget build(BuildContext context) {
    _bottomMoveAnimation = Tween(
      begin: Offset(0, widget.bottomBarCloseHeight),
      end: Offset(0, widget.bottomBarOpenTopMargin),
    ).animate(_animationController);

    return AnimatedBuilder(
      animation: _animationController,
      child: Container(
        ...
      ),
      builder: (context, child) {
        return Transform.translate(
          offset: _bottomMoveAnimation.value,
          child: child,
        );
      },
    );
  }

  @override
  void dispose() {
    _animationController.dispose();
    super.dispose();
  }

  // stream notification
  void runAnimation(bool isOpen) {
    if (isOpen == true) {
      // print("forward start!");
      _animationController.forward().then((value) {
        // print("is done?");
        cameraStreamController.add(true);
      });
    } else {
      _animationController.reverse();
    }
  }
```

</details>

