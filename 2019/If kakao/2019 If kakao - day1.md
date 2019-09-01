# 2019 if kakao day1

## 소개
2019년 COEX 그랜드볼룸에서 열린 if kakao에서 여러 발표들을 보고 들은 것을 메모한 문서입니다.

## 컨테이너 CI/CD를 하나의 jenkins pipeline으로 관리하기
* GoCD의 장점은 Jenkins보다 많은 CD기능을 제공한다는 점이고 단점은 하나의 stage가 하나의 job으로 구성하고 너무 많아지고 느려지는 점이다.
* 개발자가 구성요청을 하면 DevOps는 그 요청사항에 맞게 UI까지 생성해서 주어야 했다.
* 자동화를 위해서 jenkins pipeline을 사용했다.
* pipeline은 YAML이나 XML이 아닌 그냥 pipe라인의 코드를 작성하는 것이다.
* 익숙해지면 뭐든할 수 있었고 UI없이 대부분의 기능이 구현이 되고 이력관리가 쉽다는 장점이 있다.
* 단점은 익숙해져서 잘 쓰려면 상당한 학습이 필요하다. 하지만 발표자는 jenkins pipeline을 사용해야했다.
* 그래서 yml로 화이트 박스화했고, 개발자는 Jenkinsfile(yml)만 건드리면 가능했다.
* 그리고 jenkins pipeline은 깃허브와 동기화되어 jenkinsfile이 있는 레포지토리나 브랜치를 View로 뿌려주었다.
* 하지만 K8S yaml은 여전히 수작업으로 이루어졌다.
* 이렇게 하면서 장점은 관리포인트의 단일화와 소모적인 핑퐁 커뮤니케이션이 줄었고 배포 정보의 화이트박스화와 휴먼에러도 줄었다.
* 단점은 CD까지 구격화된 데이터로 처리하는 문제와 너무없는 UI, 계속 복잡해지는 소스와 너무 큰 변경 Risk, 어쩔 수 없이 처리하지 못해 아직 남은 수동 작업들이 있다.
* 그래서 jenkins pipeline을 오픈소스를 도입하여 기능 추가와 배포 개선하기로 하였다.
* 더 많은 기능을 상대적으로 적은 Risk로 구현할 수 있는 Spinnaker를 사용하였고 그로 인해 발생하는 오류는 Sail을 통해 극복하였다.
* Spinnaker는 json으로 파이프라인을 구성이 가능해서 최대한 활용하기로 했다. 그래서 Pipeline의 생성과 업데이트 로직을 Spinnaker로 넘겼다. 또, CD기능을 Spinnaker의 배포 기능으로 넘겼다.
* 그리고 istio를 사용했는데 istio는 소스로 이루어진 pipeline에서 다양한 기능을 분배하고 새로운 기능을 제공하고자할 때 coding보단 templating으로 대체한다. 또 Helm char에 참께 정의가능했고 Desired State 정의가 가능했다.
* 사이드카 패턴임에도 성능이 나올까라는 고민이 있었지만 생각보다 성능이 문제가 되지 않아 도입하게 되었다.
* 점차 많은 부분에서 template을 요구아여 수동으로 관리하기엔 너무 부담스러워서 Sail을 이용하여 HELM에서 필요한 정보를 chart화 하였다.
* 하지만 아직은 배포 대쉬보드가 부족하고 아직은 jenkins.yml이 100% 작성하기 쉽다고 할 수는 없다.
* 최종목표는 구성요청없는 Pipeline이다.
* 발표자님은 Pipeline을 코드로 풀어내는 순간 test도 필요해지고 Devops 개발자에겐 Web UI는 없는게 낫다고 생각하시고 그리고 새로운 시스템을 오픈하는 것은 쉽지만 잘쓰게 하는 건 어렵고 오픈 소스를 만드는 것이 아니라는 느낀점이 있었다고 하신다.

* **정리**: jenkins pipeline을 활용하여 조직 내의 DevOps로서 자동화를 해본 이야기다. jenkins pipeline을 사용하면서 istio, Sail 등의 도구를 활용하였던 경험을 공유하였다.
* **느낀점**: 발표제목이 jenkins가 적혀 있길래 그냥 가봤는데 내가 생각하던 거랑은 조금 다른 발표였지만 인프라 구축에 관해 아무것도 모르던 나도 어느 정도 이해할 수 있을 정도로 이해하기 쉽게 설명해주셨으며 나도 이런 인프라 자동화를 해보고 싶어졌다.

## 카카오뱅크 모바일앱 DevOps
* DevOps에 대한 설명: 개발 조직은 지속적인 변화를 주고 싶어하고 운영조직은 변화를 원하지 않는다. 그래서 DevOps는 변환에 신속하게 대응하기 위해 존재한다.
* 카카오뱅크는 은행이기 때문에 운영에 더 집중하게 됨. 하지만 유저는 불편하마을 느낌.
* 그래서 카카오뱅크는 도구와 문화로 극복했다.

* 스케줄링
    * 스프린트 봇이라는 도구를 활용했다. 
    * 문화는 주 단위 스프린트를 적용했다.

* 개발
    * 효율적인 개발을 추구하기 때문에 오픈소스라는 도구를 권장한다.
    * 그리고 관찰자와 행위자가 함꼐 하는 페어프로그래밍을 권장하여 위험부담을 감소하였다.
    * 또, 공동 개발 문서화를 한다. 개발 전 이해도를 낮추고 히스토리를 축적하는 등의 일을 한다.
    * 그러고 일일 스크럼 회의도 진행한다.

* 코드리뷰
    * 코드리뷰 사전 자동화라는 도구를 사용한다. 
    * Gitpush가 되면 빌드가 되고 유닛테스트 후 정적 분석을 한 후 코드리뷰를 진행한다. 이 자동화 과정에는 모두 알림 봇이 작동한다.
    * 코드 리부도우미도 만들어 사용한다.
    * 그리고 코드리뷰 규칙 문화와 온라인 코드리뷰와 오프라인 코드리뷰 문화를 적용하였다.
* 빌드/배포 
    * 코드 머지 규칙이 있다. 머지는 최종 책임자만 할 수 있다.
    * 여기서도 빌드/배포 자동화와 봇을 활용하여 사용하고 있다.
    * 1일 다양한 피처들을 다수 배포하는 병렬 배포도 적용하고 있다.
* 테스트
    *  QA 조직과 개발 조직이 협력관계를 맺고 있다.
    * 새롭게 추가된 기능에 한해서 다 같이 모여 테스트하는 Sanity 테스트를 1 ~ 3회를 진행한다.
    * 그러고 통합 테스트를 3 ~ 6주 진행하며, 시나리오 테스트를 진행한다. 이 또한 자동화된다.
    * 시나리오 테스트 자동화를 한다.

* 릴리즈
    * 단계적 출시를 진행한다. 그러면서 알 수 없는 오류가 발생했을 경우 위험을 최소화한다.
    * 앱스토어 리뷰 봇을 만들어 사용하고 있다. 리뷰알림과 자동 리뷰 등을 수행한다.

* 운영 
    * 회고를 진행한다. 지난 릴리즈에 대한 칭찬과 반성을 하고 앞으로 개선해야할 액션플랜을 함께 정한다.
    * 주간 온도라는 동료들의 기분을 알아간다.
    * 기술 세미나와 새롭게 적용해야 하는 것에 대한 합의를 하는 개발 잡담을 진행한다.
    * 그러고 다음 릴리즈 스케줄링을 활성화 한다.

* 모든 금융권이 변화하기를 원하신다고 한다.

* **정리**: 모바일 DevOps로서의 매니징에 대한 발표로 많은 기업에게 귀감이 될만한 현재 카카오뱅크에서 적용 중인 좋은 문화와 도구에 대해 알려주셨다. 
* **느낀점**: 모바일 개발자라면 개발만 할 줄 알았는데 회사에 들어가면 나름의 매니징이 필요하다는 것을 알게 되었고 나도 모바일 DevOps가 되고 싶어졌다. 이 발표에서 좋은 것들을 배웠으니 내 프로젝트 팀에서도 한번 적용해봐야겠다.

## 안드로이드 빌드: 설탕없는 세계
* PostCompilation를 메인으로 다룬다.
* Desugar: 개발자를 위한 편의를 빌드 과정에서 제거하는 것.

* 후처리의 장점
    * 보안을 강화할 수 있다
    * 언어의 한계를 극복할 수 있다 
    * APT의 한계도 극복할 수 있다.
    * 반복적인 작업을 자동화할 수 있다.
    * 교양을 쌓을 수 있다.

* Java VM은 스택기반의 VM이고 32비트 기반의 스택이며 상수의 종류를 구별하지 않는다. 닷넷과는 달리 의존적이다.
* 안드로이드 빌드는 Java 바이트 코드를 ART의 Dalvik 바이트 코드로 변환한다.
* 자바에서는 클래스 별로 별도의 파일로 구성되어 있고 상수 역시 클래스 별로 분리되어 있다. 
* 하지만 DEX는 64K 메서드 단위로 여러 클래스가 하나의 파일에 합쳐져 있고 상수들은 DEX내에서 공유한다.
* 구글이 desugar를 하지 않고 DEX로 한번에 가는 프로젝트를 했지만 망했다.
* 안드로이드 빌드과정은 플러그인 설정 후 AppPlugin 후 ApplicationTaskManager로 연결한후 TaskManager 매니징한다.
* Transform 설정
    * 소비라는 개념은 한번 쓰겠다고 선언하면 그 파일은 다시 재작성해야하는 것이다.
    * getName, getInpuTypes, getOutputTyes, getScope, getParameterInputs 등 이름, 입/출력의 유형을 정의하는 함수들이 있다.
    * 구글에서는 람다 코드를 JVM 구버전에서 돌게만드는 DesugarTransform()을 사용하는데 getName을 하면 desugar가 나온다. 서브 프로젝트, 외부 라이브러리의 클래스 파일을 읽는다.
    * 안드로이드 앱에 프로가드를 적용시키는 트랜스폼인 ProGuardTransform(난독화를 위함)이 있는데 getName을 하면 proguard가 나오고 프로젝트, 서브프로젝트 라이브러리의 클래스와 리소스를 받는다.
    * 이외에도 ShrinkResourcesTransform(사용하지 않는 리소스 제거) 등 여러 Transform이 존재한다.

* **정리**: 후처리에 대해 알아보았다. 그중 desugar에 대한 이야기였는데 안드로이드 빌드 과정의 특징이나 Transform에 대해서도 알아보았다.
* **느낀점**: 지금까지 솔직히 후처리에 대해서는 내가 알아야 하나라는 생각이 강했는데 이번 발표를 듣고 후처리에 대해 알아보고 직접해보면 좋을 것 같다는 생각이 들었다.

## 다음웹툰의 UX (New tab : Top)
* 창의적이고 자연스럽고 유저가 집중할 수 있는 의미있는 UX를 만들자.
* 삼각형의 모양을 변화시켜야 하기 떄문에 6등분시켰고 이를 통해 모양을 변화시켰다.
* 그리고 Sharder를 통해 색상을 주었으나 이슈가 발생해 Gradient를 합치지 않고 각각 4개의 색상을 주었고 rotate와 scale을 주어 색상의 움직임을 표현했다.
* Tabbar Gradient은 삼각형에서 사용했을 때와 동일하게 하여 애니메이션을 주었다.
* 그리고 splash 화면과 연결이 되어야 하는데 이 것은 splash에 배경을 Gradient를 주어 해결했다.
* Tabbar 스위칭 시 색상의 변화를 같이 주어 느낌을 표현하였고 색상이 겹치는 문제는 색상 alpha 처리로 해결하였다.
* 순위표가 줄어드는 Collapse 애니메이션은 onScrolled 함수로 처리했다.
* 작품 배경이 Parallax Effect가 적용되야 하는데 onScrolled 함수로 Image를 처리했고 Image 짤림 문제는 position 문석으로 해결하였다.

* **정리**: 다음 웹툰의 ver 2.3에 대해 알아보았다. 다음 웹툰의 UX 철학을 알 수 있었고 그 철학을 적용시키기 위한 개발자의 노력도 알 수 있었다.
* **느낀점**: Gradient를 지금까지 활용해보지 않았는데 정말 다양한 표현을 할 수 있다는 것을 알게 되었고 UX나 UI적으로 배운 점이 많은 정말 좋은 발표였다. 