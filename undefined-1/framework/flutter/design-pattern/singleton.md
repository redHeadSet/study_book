# Singleton

{% embed url="https://dart.dev/language/constructors#factory-constructors" %}

> Use the `factory` keyword when implementing a constructor that doesn’t always create a new instance of its class.

* factory 키워드를 사용하여 Singleton 생성 가능

```dart
// 공식 예제
class Logger {
  final String name;
  bool mute = false;

  // _cache is library-private, thanks to
  // the _ in front of its name.
  static final Map<String, Logger> _cache = <String, Logger>{};

  factory Logger(String name) {
    return _cache.putIfAbsent(name, () => Logger._internal(name));
  }

  factory Logger.fromJson(Map<String, Object> json) {
    return Logger(json['name'].toString());
  }

  Logger._internal(this.name);

  void log(String msg) {
    if (!mute) print(msg);
  }
}
```

```dart
// 샘플 구현
class GlobalData {
  late bool isLogin;
  UserData? userData;

  static final GlobalData _singleton = GlobalData._internal();

  factory GlobalData() => _singleton;

  // 클래스 최초 생성 시 1회 호출됨
  GlobalData._internal() {
    isLogin = false;
  }
}
```

```dart
// 사용
globalData = GlobalData();
```

* 참고
  * \_internal 은 예약어는 아님. flutter 의 Named Constructor. (fromJson 같은...)
  * factory 키워드로 인해 항상 동일한 처리를 하도록 만들 수 있음
  * 위처럼, factory 에서 static final 객체를 반환하므로 항상 동일한 인스턴스를 반환



