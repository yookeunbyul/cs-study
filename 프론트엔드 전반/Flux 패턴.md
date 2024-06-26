## Flux 패턴

Flux는 데이터를 취급하기 위한 패턴이다. 즉, 데이터가 애플리케이션을 흐르는 방식.

### 문제점

Facebook에서 고질적인 알림 버그가 있었다.

메시지 아이콘에 알림이 떠 있지만, 그 아이콘을 클릭해서 들어가면 아무런 메시지가 없는 버그.

팀이 이 버그를 고치고 얼마동안은 괜찮았지만 **[업데이트를 하다보면] 곧 다시 나타났다.**

=> 한마디로 걍 로직이 꼬여있어서 어딜 건들면 버그가 발생하는 느낌?

단기적인 해결책이 필요한 게 아니라, 시스템을 예측 가능하게 만들어서 문제점을 완전히 없애길 원했다.

### 근본적인 문제점

Facebook이 찾은 근본적인 문제점은 데이터가 애플리케이션을 흐르는 방법에 있었다.

기존엔 MVC 패턴을 사용해서 데이터를 가지고 있는 모델이 렌더링을 하기 위해 뷰 레이어로 데이터를 보냈을 것이다.

![04](https://github.com/yookeunbyul/cs-study/assets/91243651/d1e0fb82-4b77-4f3b-994b-2d759b63a73f)

하지만 사용자의 상호작용이 뷰를 통해서 일어나기 때문에 뷰가 가끔씩 모델을 업데이트해야할 필요가 있다.

또한 의존성 모델이 다른 모델을 업데이트해야할 때도 있다.

이게 엉키고 엉키면서 산사태처럼 아주 많은 다른 변경을 초래한다.

데이터가 양방향으로 흐르면서 탁구처럼 공이 어디로 날아갈지 알기가 아주 어렵게 된다.

즉, 데이터 흐름을 디버그하기 어렵게 만든다.

### 해결책: 단방향 데이터 흐름

![05](https://github.com/yookeunbyul/cs-study/assets/91243651/2e24bdde-4a8d-4922-9c82-02571182f878)

그래서 Facebook은 다른 종류의 아키텍처를 시도하기로 했다.

이 구조에서는 데이터는 한 방향으로만 흐르고, 새로운 데이터를 넣으면 처음부터 흐름이 다시 시작된다.

이 아키텍처를 Flux라고 불렀다.

### 캐릭터를 만나보자

- 액션 생성자

  모든 변경사항과 사용자의 상호작용이 거쳐가야 하는 **액션**의 생성을 담당하고 있다. 언제든 애플리케이션의 상태를 변경하거나 뷰를 업데이트하고 싶다면 액션을 생성해야만 한다.

  액션 생성자가 하는 일은 무슨 메시지를 보낼지 알려주면 나머지 시스템이 이해할 수 있는 포맷으로 바꿔준다.

  type과 payload를 포함한 액션을 생성한다.

  - type은 시스템에 정의 된 액션들 중의 하나다.
    모든 가능한 액션들을 아는 시스템을 가짐으로써 시스템에서 제공하는 API 전체 ㅡ 모든 가능한 상태변경 ㅡ을 바로 확인할 수가 있다.

    **일단 액션 생성자가 액션 메시지를 생성한 뒤 디스패쳐로 넘겨준다.**

- 디스패쳐

  디스패쳐는 댁션을 보낼 필요가 있는 모든 스토어를 가지고 있고, 액션 생성자로부터 액션이 넘어오면 여러 스토어에 액션을 보낸다.

  **이 처리는 동기적으로 실행되어서 탁구게임같은 경우를 처리하는데 도움을 준다.**

  액션 타입과 관계없이 등록된 모든 스토어에 보내진다.

  모든 액션을 받은 뒤 처리할지 말지를 결정한다.

- 스토어

  애플리케이션 내의 모든 상태와 그와 관련된 로직을 가지고 있다.

  무조건 액션 생성자/디스패쳐 파이프라인을 거쳐서 액션을 보내야만 한다.

  스토어 내부에서는 보통 switch statement를 사용해서 처리할 액션과 무시할 액션을 결정하게 된다.

  스토어에서 상태 변경을 완료하고 나면, 변경 이벤트를 내보낸다. 이 이벤트는 컨트롤러 뷰에 상태가 변경했다는 것을 알려주게 된다.

- 컨트롤러 뷰와 뷰

  뷰는 상태를 가져오고 유저에게 보여주고 입력받을 화면을 렌더링하는 역할을 맡는다.

  컨트롤러 뷰는 스토어와 뷰 사이의 중간 관리자같은 역할을 한다.

  상태가 변경되었을 때, 스토어가 그 사실을 컨트롤러 뷰에게 알려주면, **컨트롤러 뷰는 자신의 아래에 있는 모든 뷰에게 새로운 상태를 넘겨준다.**

<br />

## 출처

https://bestalign.github.io/translation/cartoon-guide-to-flux/
