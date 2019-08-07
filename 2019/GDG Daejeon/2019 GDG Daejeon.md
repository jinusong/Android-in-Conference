# GDG Daejeon 2019

## 소개
2019년 GDG Daejeon에서 여러 발표들을 들었는데요, 이를 요약한 문서입니다.


## ML on Google Cloud (백재연님)

- GC를 이용하여 클라우드 환경에서 ML을 구성할 수 있음
- 중소기업이나 소규모로 진행하는 경우에는 비용 측면에서 비효율적일 수 있으니 합리적인 판단이 필요
    - (e.g. 소규모 작업 환경에서는 자체 워크스테이션 구축이 더 효율적일 수 있음)
- Contact Center API
    - 인공지능이 사람과 직접 전화를 하여 예약을 잡아주는 기능
    - (e.g. 미용실 등)

- *정리*: 클라우드 환경에서의 ML은 여러 장점이 존재한다.
- *느낀점*: 클라우드를 활용한 ML은 정말 신기했다. 서비스 제공 목적의 강화학습을 진행할 때 유용해 보였다.

## Web Updates at I/O 2019 (조은님)

- [Google I/O 2019: What's new with Chrome and the Web](https://blog.chromium.org/2019/05/google-io-2019-whats-new-with-chrome.html)

- [Lighthouse](https://developers.google.com/web/tools/lighthouse/?hl=ko)
- [Progressive Web App](https://developers.google.com/web/fundamentals/codelabs/your-first-pwapp/?hl=ko)

- *정리*: 웹 분야에 여러 새로운 기술들이 추가되었다.
- *느낀점*: 열심히 들었던 것 같은데 시간이 꽤 지났더니 기억이 잘 안나네요 ㅠㅠ 죄송합니다

## What's New in Android Studio (노현석님)

- 안드로이드 스튜디오에 몇몇 새로운 기능이 추가됨

### 3.4 Version
- Resource Manager
    - 파일을 보고 이 파일이 어떤 기능을 수행하는지 파악하기에 어려움이 있음
    - 가장 왼쪽 탭에 탑재됨
    - Dependency Image 확인 가능
    - Group, Color, ??로 구성
- Bulk Import 기능
    - 이미지를 사용해야 할 때 드래그 앤 드롭으로 리소스 매니저에 옮기면 Import 됨
- Preview all layouts
    - 모든 레이아웃을 미리 확인 가능
    - 원하는 레이아웃을 검색
- Color Picker
    - Resource XML의 Color를 더블클릭
    - RGB, HSB 지원
- Project Structure Dialog
- Import Intentions
    -  라이브러리 추가 제안
    - Jetpack, Firebase 지원
    - 코드를 복사하여 불러왔을 때, 의존성을 관리하는 것을 도와줌

### 3.5 Version
- Project Marble
    - 시스템 성능 최적화
        - DataBinding UI Freezes
        - 플러그인 관리(기본적으로 35개의 플러그인이 설치됨)
        -> 사용하지 않는 플러그인 disable
        - Build Speed
            - Kotlin Incremental Annotation Processing(그레이들 4.10 지원)
            - Light R class generation
            - Benchmarking
            - 의외로 빌드 과정에서 중복 빌드가 발생하는 경우가 많음
        - I/O File Access for Windows: 윈도우 상에서의 Android Studio는 느리다는 게 일반적인 생각인데, 대부분의 윈도우 환경에서는 코드 파일까지도 바이러스를 체킹하고 있어 성능 저하를 유발함. 이에 Android Studio에서 Event 탭에 관련 내용을 알림으로써 성능 저하를 막고자 함
    - 기능
        - Foldable Support
            - Android Q부터 지원
            - Emulator 사용 가능
        - App Deployment Flow
        - Increase Heap: 평균적으로 1.2GB를 Android Studio에서 사용
        -> Memory Settings에서 관리 가능(더 많은 메모리를 할당하여 성능 향상)
        - Layout Editor
            - Zoom in/out 기능
            - 깜빡임이 사라짐
            - Layout Editor Property Panel 개선
    - Apply Changes
        - Instant Run?
            - hot-swap을 위한 추가 작업 -> 느려짐
            - 64K 이상의 경우 빌드 오류
            - 내부 품질 기준 미달
        - Platform API로 빠르게 앱 실행
            - Runtime Instrumentation 활용 -> 클래스를 즉시 재정의
    - bugs
        - Fixed Memory Leak

### Summary
- 요청: System Exception 날려주세요!
-> 오류 발생시 Android Studio 팀에 보고하면 보고가 많은 순으로 개선되어 적용됨
- *요약*: 안드로이드 스튜디오는 사용자의 요구사항을 적용하기 위해 노력하고 있으며, 버전이 올라갈수록 지원되는 기능이 많아진다.
- *느낀점*: 안드로이드 스튜디오는 Intellij와 비슷하면서도 다른 점이 미묘한 호기심을 주는 것 같다.
        
## 구글의 AI, 그리고 소프트웨어(전태균님)

- 주요 내용
    - AI for Mobile and IoT Devices: TensorFlow Lite
    - Federated Learning: Machine learning on Decentralized Data

- AI/ML Software
    - **수십억개의 기계**를 통해 **인공지능 서비스**를 제공키 위해 **사용자의 보안**을 지키며 꾸준히 **높은 수준의 기능**을 제공하기 위해 필요한 것은 무엇인가?
    - TensorFlow Lite + Federated Learning

- TensorFlow Lite
    - Edge ML Explosion
    - New opportunities -> use little computing power device
    - ML Kit
    - Easy to get started
        - Jump start
        - Custom model(can use TF Lite Converter)
        - Performance
            - Incredible inference performance
            - Edge *TPU* Delegate ->  Small physical and power footprint
        - Optimize
    - MCU on TF Lite with a single framework

- Federated Learning
    - Decentralized data
        - (e.g. Gboard: mobile keyboard)
    - Federated computation
        - On-device datasets -> 오래된 데이터는 삭제
        - distributed aggregation을 통해 서버에 데이터 저장
    - Model deployment workflow -> reference of server, client 
    - Federated learning
        - On-device data 
    - TensorFlow Federated
    
- *정리*: 제한된 환경에서의 머신 러닝은 여러 흥미로운 방법들을 이용해 진행된다.
- *느낀점*: 머신러닝은 언제나 대단해보인다. 난 그릇이 안돼서 ㅠ

## Flutter And beyond Web(조성윤님)

- Flutter has
    - 하나의 코드 베이스로 다양한 플랫폼에 적용할 수 있음
    (모바일, 웹, 데스크탑, 임베디드)
    - Dart로 개발
    - Declarative UI
    - Widget Lifecycle
        - StatefulWidget이 새로운 State object를 BuildContext당 생성함(?)
    - Platform Chanel
        - Native API 또는 3rd Parth API를 호출하기 위해 Platform Chanel 이용
- Hummingbird
    - How to work?
        - 초기에는 모든 렌더링 대상을 HTML Elements 형태로 변환
        - 꽤 좋았으나 기존 Flutter API와 비교하여 큰 변화가 필요
        - 접근방식을 HTML, CSS, Canvas 형태로 변경
        - pixelation
            - 염려가 없는 그림 -> DomCanvas
            - 일어나는 그림 -> BitmapCanvas
        - 그림의 크기 조정 발생시 크기에 맞춰 캔버스의 크기도 변경해 주어야 했음
    - Composition Multiple Canvas
    - Dom, Canvas, CSS의 적절한 조합을 가지고 모던 브라우저에서의 유저 경험 제공
    - Dart 2 JS Compiler를 통해 JS로 Dart 코드 변환

- *정리*: Flutter를 이용해 여러 플랫폼에서 구동할 수 있는 애플리케이션을 만들 수 있다.
- *느낀점*: 발표자님이 Flutter가 매우 좋다고 하시는데 언제 한 번 시간 되면 써봐야겠다.(된다면)
