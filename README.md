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

## 2.2 String interpolation

String interpolation는 text에 변수를 추가하는 방법임.  
String interpolation를 사용할땐 " $ "를 써주고 뒤에 추가할 변수 이름을 작성해준다.
```dart
void main() {
    var name = 'nico';
    var greeting = 'Hello everyone, my name is $name';
}
```
이렇게 작성해주면 "Hello everyone, my name is nico"가 출력된다.
그냥 text를 추가하는건 이렇게 작성해주면 됨.  
근데 계산을 해야하는 상황이 생긴다면 아래 코드처럼 작성해 주면됨.

```dart
void main() {
    var name = 'nico';
    var age = 10;
    var greeting = 'Hello everyone, my name is $name and I\'m ${age + 2}';
}
```
그냥 $뒤에 중괄호쓰고 괄호안에 수식을 적으면 끝남.
위 코드에서 오류가 하나 있는데 바로 I'm때문에 오류가 나는거임.
왜냐하면 텍스트 시작을 작은 따옴표로 했는데 I'm에 작은 따옴표가 있기때문에 dart에서 I'm에서 문장이 끝낫다고 생각하기때문임.  
이 오류를 고치려면 I'm대신 I\'m을 써주면된다.

## 2.3 Collection for

```dart
void main() {
    var oldFriends = ['nico', 'lynn'];
    var newFriends = [
        'lewis', 
        'ralph', 
        'darren',
        for(var friend in oldFriends) "❤️ $friend";
    ]
}
```
이렇게 작성한후 newFrien를 출력하면 newFriend라는 리스트안에 있는 요소들을 출력한후에 oldFriends의 요소들앞에 ❤️가 붙어서 나온다.

## 2.4 Maps

```dart
void main() {
    var player = {
        'name' : nico,
        'xp' : 19.99,
        'superpower' : false,
    };
}
```
map은 위에있는 코드와 같이  
'key' : value 
이렇게 작성해주면 된다. 
설명에 들어가기전에 object에 대해 설명하자면
object는 쉽게말해 모든 데이터타입이 될수있는걸 말함.
string이 될수도있고 int가 될수도 있고 bool이 될수도 있음 

값이 비어있는 Map도 만들어줄수 있는데 예를 들면
```dart
void main() {
    Map<int, bool> player = {
        1: true,
        2: false.
    };
}
```
이렇게 작성을 할수 있는데 var대신 map을 적어주고 <>괄호안에 자신이 원하는 key의 데이터 타입, 원하는 value의 데이터타입을 적어주면 된다. 이렇게 적으면 key는 int, value는 bool인 데이터타입 밖에 넣을수없다.

## 2.5 sets
set은 list와 map을 짬뽕시켜놓은 느낌이 조금 있음.
```dart
void main() {
    Set<int> numbers = {1, 2, 3, 4};
}
```
set과 List의 차이는 set에 속한 요소들은 희귀한거임.
이게 무슨 말이냐면
list에선 add 메소드로 똑같은 요소를 여러번 추가해도 list안에 들어가지만 set은 그게아님.  
set에서 add 메소드로 똑같은 요소를 여러번 추가해도 set안에 추가되지않음.

요소가 항상 하나씩만 있어야 되면 set을 사용하고
여러개있어도 상관없다면 list를 사용하면 됨.

## 3.0 defining a function

일단 설명에 앞서 간단한게 function을 만들고 설명함.
```dart
void sayHello(String name) {
    print("Hello $name nice to meet you");
}

void main() {
    print(sayHello('nico'));
}
```
위에있는 코드처럼 sayHello라는 함수를 만들었는데  
void는 이 함수가 아무것도 반환하지 않는다는 의미임.
만약 이 함수에서 string을 반환하고 싶다면 아래처럼 작성해주면 된다.
```dart
String sayHello(String name) {
    return "Hello $name nice to meet you";
}

void main() {
    print(sayHello('nico'));
}
```
이렇게 하면 이 함수는 string을 반환하게 된다.  
이렇게 작성하는 방법말고 다른 방법도 있는데 바로 화살표를 이용하면된다.

```dart
String sayHello(String name) => "Hello $name nice to meet you";

void main() {
    print(sayHello('nico'));
}
```
이렇게 작성하면 된다.  
함수에 포함된 코드가 여러줄이면 첫번째 방법대로 사용하면되고
한줄짜리 함수라면 두번째 방법을 사용하면 된다.

## 3.1 named parameters

이번엔 방금처럼 함수를 만들고 한개의 값이아닌 여러개의 값을 반환하는 함수를 만들어볼것임.

```dart
String sayHello(String name, int age, String country) {
    return "Hello $name, yout are $age, ande you come from $country";
};

void main() {
    print(sayHello('nico', 20, 'USA'));
}
```
대충 이렇게 작성하면 되지만 그렇게 좋은 코드는 아님 왜냐하면
사용자가 sayHell의 순서도 모를수있고 20이 무슨뜻인지 USA가 무슨뜻인지 모를수도 있기 때문임. 

그래서 우리는 
```dart
String sayHello({String name, int age, String country}) {
    return "Hello $name, yout are $age, ande you come from $country";
};

void main() {
    print(sayHello(
        age : 12,
        country : 'cuba',
        name : 'nico',
    ));
}
```
첫번째 코드에선 순서를 다 기억해서 작성해야 했다면 위에보이는 코드는 순서와 상관없이 (변수이름: 값)으로 작성해주고, 함수에서 변수들을 중괄호 묶어주면 된다. 하지만 이렇게 해도 오류가 뜨는데 그 이유는 dart에서 변수의 값이 null이면 어떡하지라는 걱정을 해주고있는거다. 여기서 dart가 하는 말은 만약 사용자가 country,name을 입력해주지 않는다면 어떡하지라고 말하는거다. 이럴땐 두가지의 방법이 있는데

첫번째 방법은 함수를 생성할때 변수에 디폴트값을 줘버리는것이다. 그럼 사용자가 변수에 값을 넣어주지않아도 디폴트값이 있기때문에 상관없기 때문이다. 어떻게 작성하냐면
```dart
String sayHello({String name = 'nana', int age = 12, String country = 'cuda'}) {
    return "Hello $name, yout are $age, ande you come from $country";
};

void main() {
    print(sayHello());
}
```
이렇게 작성해주면 오류가 안난다

두번쨰 방법은 required를 이용해서 사용자가 변수들의 값을 모두 입력하게 만드는것이다. 작성하는 방법은
```dart
String sayHello({ required String name, required int age, required String country}) {
    return "Hello $name, yout are $age, ande you come from $country";
};

void main() {
    print(sayHello(
        age : 12,
        country : 'cuba',
        name : 'nico',
    ));
}
```
이렇게 작성해주면 된다.

## Recap
복습하는 거구연~

## 3.3 optional positional parameters
```dart
String sayHello(String name, int age, String country) => "Hello $name, yout are $age, ande you come from $country";


void main() {
    print(sayHello('nico', 20, 'USA'));
}
```
이 코드에선 모든 변수가 required이다. 하지만 name argument를 사용하지않고 country만 required하지 않게 하려면 어떻게 해야할까?

```dart
String sayHello(
    String name, 
    int age, 
    [String? country = 'cuba']) => 
        "Hello $name, yout are $age, ande you come from $country";

void main() {
    print(sayHello('nico', 20));
}
```
이렇게 함수에서 데이터 타입과 변수명을 대괄호로 묶고 디폴트값을 주고 not requird이라는 뜻인 "?"를 데이터타입 뒤에 적어주면 변수를 required하지 않고도 함수를 호출할수잇다.
