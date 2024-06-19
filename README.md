# DART


## 01 Why Dart

### 왜 플러터가 dart를 사용할까?
- dart는 UI에 최적화된 언어이기때문. 

### 컴파일러
- dart는 컴파일러가 2개이다.
    - dart Web
        - dart로 작성한 코드를 JS로 변환해주는 컴파일러
    - dart Native
        - dart로 작성한 코드를 여러 CPU의 아키텍쳐에 맞게 변환해주는 컴파일러

### dart는 어떻게 컴파일되는가?

- just-in-time(JIT)
    - dart VM을 사용하는데 작성한 코드의 결과를 바로 화면에 보여준다.
- ahead-fo-time(AOT)
    - 예를 들어 C,C++, Rust, GO로 코딩한다고 하면 코딩을 끝낸뒤에 컴파일하려면 아키텍쳐를 지정해줘야한다.
    - 만약 C++로 코딩을 끝낸후 window로 배포하고싶다면 작성한 코드를 windows 바이너리(기계어)로 컴파일 해줘야는데, 그 바이너리를 제공하는것이라고 생각하면 편하다 

    #### 요약
    ##### 개발중
    ㄴ flutter로 개발 -> dart VM -> dart 가상 머신이 JIT 컴파일러 제공(풍부한 디버깅 지원(?)과 함께)

    ##### 배포
    flutter로 개발 -> 슬슬 배포가 마려움 -> AOT 컴파일러 -> native ARM, x64 기계어로 컴파일 

## 1.0 Hello World

dart는 반드시 main를 작성해야함.  
ㄴ 왜? main 함수에서 작성한 코드가 호출됨

### Hello world를 직접 실행해보자

```dart
void main() {
    print("Hello World");
}
```
아까 위에 적어놓았던것처럼 
main함수에 코드를작성해야 실행했을때 Hello World가 실행됨.

만약 main함수가 아니라 
```dart 
void hello() {
    print('Hello wolrd');
}
```
hello 함수에다 아무리 적어놔도 main함수가 아니라서 실행이안됨.


## 1.1 변수

dart에서 변수를 선언하는 방법은 두가지 방법이 있는데
 ```dart
void main() {
    var name = '니꼬';
    name = 1;
}
```
첫 번째 변수를 선언하는 방법은 변수 이름 'var'를 붙이는거다 그러면 dart가 알아서 타입을 지정해준다.

두번째 변수 선언하는 방법은
그냥 명시적으로 타입을 지정해주는거다 ㅇㅇ 

대부분 함수, 메소드 내부에 지역 변수를 선언할떄는 var를 사용한다.

class에서 변수나 property를 선언할떄는 타입을 시정해준다.

### dynamic

우리가 변수를 지정할때 var를 사용하고 값을 넣지않았을떄 우리가 선언한 변수는 dynamic type이 된다 우리는 원래 var 방식을 사용해서 변수를 선언하고 초기화를 하면 다른 type으로는 업데이트를 하지못했는데
dynamic type은 어떤 type으로든 업데이트가 가능하다.
정말 필요할때만 써야됨.

## 1.3 Nullable Variables

null safety는 개발자가 null값을 참조할 수 없도록 하는거임 민약 코드에서 null값을 참조하면 runtimeError가 뜨게됨.

런타임 에러는 사용자가 앱을 사용하던 중에 뜨는 에러라는 뜻.
이상적으론 컴파일 이전에 잡아내는게 베스트

```dart
bool is EMpty(String string) => string.length == 0;

main() {
    isEmpty(null);
}
```

이렇게 null safety가 없는 버전의 dart는 실행시키면 런타임 에러가 뜬다. 그리고 그 에러는 NoSuchMethod이다. 왜 이런 오류가 뜨냐면 코드에서 string을 보내야하는 곳에 null값을 보냈기 때문이다.

그럼 null값을 없애면 되는것아니야?
라고 생각할수 있지만 그건 또 정말아님. null은 프로그래밍에서 아주 유용한 값임. null은 아무것도 있지 않음을 뜻한다.
null떄문에 오류가 발생하는 이유는 보통 null값을 참조해서 코드를 짜기떄문이다. 

그래서 dart는 null safety를 도입함. 

그럼 null값을 사용해야할떄 어떻게 쓰냐?

null값을 직접적으로 사용하는게 아니라 이게 null값이 될 수 도 있다라는걸 사용해주면 된다. 예상할순 있지만 직접적으로 null이라곤 해줄수없다 바로 이렇게 작성해주면 된다.

```dart
void main() {
    String? nico = 'nico';
    nico = null;
}
```
이렇게 작성해주면 된다. nico가 string일수도있고 null일수도 있다는걸 dart가 알아차릴수있다.

## 1.4 Final Cariables

우리가 새로 배우게된 dart변수 생성은 var을 이용한방법과 데이터 타입을 직접 지정해주는 방법이 있었는데 두 방법은 변수값을 업데이트 할수 있다는 것이다.
이제 변하지않는 변수를 선언하고 싶다면 var도 데이터타입도 아닌 final을 입력해주면 된다.
```dart
void main() {
    final name = 'nico';
}
```
이렇게 작성해주면 된다.

## 1.5 Late Variables

late 수식어는  final이나 var앞애 붙여줄 수 있는 수식어이다 
late는 초기 데이터 없이 변수를 선언할 수 있게 해주는데 

```dart
void main() {
    late final Srting name;
    // 코드 좀 적고, api통신 할떄

    name = 'nico'
}
```
변수를 선언하고 나중에 변수에 값을 넣어 사용해야할때 값을 넣는다. 그래서 수식어 이름이 late 인거 ㅇㅇ
late로 선언한 변수는 값을 넣기전까지 사용할수없기 떄문에 코드를 작성하다가 변수를 사용한다면 dart에서 막아준다

## Constant     

dart의 const는 JS나 typescript와 달리 dart에서 const는 compile-time constant를 만들어준다
물론 JS처럼 업데이트를 할수없는 상수의 역할도 하지만, 가장 중요한건, const는 compile-time에 알고있는 값이어야 한다는것임

compile-time constant가 뭐냐면
```dart
void main() {
    const API = '1212';
}
```
이 코드처럼 API키가 1212일때 API키 값은 절대 바뀌지않을 거고 컴파일이 될떄 그 값을 알고있을거임.
만약에 API요청 같을 걸 한다고하면 
```dart
void main() {
    const API = fetchApi();
}
```
이건 compile-time constant가 아님. 컴파일러는 API 변수의 값을 모름. 왜냐하면 이건 API에서 받아야하는 값이기 떄문이다. 그래서 이 코드는 const가아니라 final이 맞음. const는 컴파일 할 때 알고 있는 값에 사용하는거임. 앱을 배포하기 전에 알고 있는 값이라는 거임. 그게 const가 하는 일임. 만약 앱을 배포하기 전에 값을 알고 있다면 그건 const가 되는게 맞는데 어떤 값인지 모르고, 그 값이 API로 부터 온다거나 사용자가 화면에서 입력해야하는 값이라면 var이나 final이 맞음. 

## 1.7 recap

1.6까지 복습.

## 2.0 data types

dart는 기본적으로 알고있는 자료형은 대부분 다 있음.

```dart
void main() {
    String name = "nico" // 큰 따옴표를 쓰던 작은 따옴표를 쓰던 노알빠 
    bool alive = true;
    int age = 12;
    double money = 69.99;
}
```
사실 dart의 거의 전부가 object임. 심지어 function도 object임.
이게 dart가 진정한 객체 지향 언어로 불리는 이유.

dart엔 아주 특별한 데이터 타입이 있는데 바로 num임.

```dart
void main() {
    num x = 12;
    x = 1.1;
}
```
num 데이터 타입은 그 값이 int수도 있고 double일 수도 있음.
왜냐하면 num은 int와 double의 부모 class이기 때문임.

## 2.1 list

리스트는 아주 좋은 기능이고 flutter에서 자주 쓴다.
리스트 생성방법은 
```dart
void main() {
    var number = [1, 2, 3, 4];
}
```
이렇게 생성해주면 dart가 알아서 데이터 타입이 뭔지 파악한다. 또 다룬방벙도 있는데
```dart
void main() {
    List<int> numbers = [1, 2, 3, 4];
}
```
이렇게 작성해주면 된다. 첫번째는 var를 이용해서 dart가 자동으로 인식하게 했다면
두번쨰 방법은 직접 데이터 타입을 dart에게 알려주는 것임.

그냥 처음에는 var을 먼저 작성하고 모든 class를 작성한 후에 두번째 방법으로 수정하자.

나중에 리스트에 값을 추가할떈 처음 작성한 리스트의 데이터 타입만 추가할수 있음
예를 들면 
```dart
void main() {
    List <int> numbers = [1, 2, 3, 4];
    numbers.add(1);
}
```
이렇게 작성해주면됨. 

그리고 가끔 마지막요소나, 첫번쨰 요소를 가져와야하는데 요소가 몇 개나 있는지 모를때 
last나 first를 사용해주면 된다.

```dart
void main() {
    List <int> numbers = [1, 2, 3, 4];
    numbers.last;
    // numbers.first
}
```
이렇게 작성해주면된다.
그리고 리스트를 작성할때 마지막 요소다음으로 ','하나를 적어주면 저절로 여러줄로 포매팅됨.

다음으로는 collection if에 대해 배워보자.
collection if로는 list를 만들 수 있는데 if으로 존재할 수도 안할 수도 있는 요소를 가지고 만들 수 있음.
예를 들면
```dart
void main() {
    var giveMeFive = true;
    var numbers = [
        1, 
        2, 
        3, 
        4,

        if(giveMeFive) 5,
    ];
}
```
이렇게 작성해주면 만약 giveMeFive가 ture라면 numbers라는 list에 5를 추가하라는 코드이다.
이코드는 아래 작성되어있는 코드랑 같은 코드인데 위에 적은 코드가 더 효율적이다.
이렇게 작성할수 있는 언어는 별로없음.

```dart
void main() {
    var giveMeFive = true;
    var numbers = [
        1, 
        2, 
        3, 
        4,
    ];
    if (giveMeFive) {
        numbers.add(5);
    }
}
```
















