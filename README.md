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

s