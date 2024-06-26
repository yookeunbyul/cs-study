## React 상태관리 최강자는?

- Redux

  중앙 집중식 Storage => 단일 store (Redux는 store를 하나만 사용하기를 권장한다.)

  업데이트를 위한 Reducer 사용(store 안에 reducer가 있다.)

  단방향 데이터 흐름 => Flux 패턴을 따른다.

  읽기 전용 상태로 상태 업데이트 시 기존 객체를 건드리지않고 새로운 객체를 생성한다.

  **리덕스에 불변성을 유지해야하는 이유는 내부적으로 데이터 변경을 감지하기 위함이다.**

  <br />

  ```
  역시 가장 처음 나온 상태관리 라이브러리라서 많이 사용하는거겠지?
  ```

  - 장점

    오래된 역사로, 단단한 커뮤니티와 개발자 풀이 존재

    단방향 데이터 흐름을 따르기 때문에 디버깅이 쉽고 예측이 가능하다.

    다양한 라이브러리 보유. 비동기 작업이나 로그 작업 처리 가능.

  - 단점

    보일러플레이트 코드가 너무 많다.

    간단한 웹앱 만들 때에 이런게 귀찮게 느껴질 수 있다.

    Recoil, MobX와는 달리 State가 변경 될 때 **Component를 업데이트 해 주는 반응형 메커니즘**이 기본적으로 탑재되지 않았기에, React의 자체 메커니즘을 활용하거나 추가적인 외부 라이브러리를 사용해야 한다.

    => 비동기 처리 라이브러리가 필요하다.

- Recoil

  페이스북이 만든 상태관리 라이브러리

  Context API기반으로 구현된 함수형 컴포넌트에서만 사용 가능

  atom이라는 최소 상태 단위를 통해 관리를 하는데, 이 atom이 업데이트 되면 각각의 구독된 컴포넌트가 반영되면서 리렌더링 된다.

  atom이나 다른 selectors를 입력으로 받는 순수 함수인 selector가 있다.

  selector는 쉽게 말해서 기존에 선언한 atom을 전/후 처리하여 새로운 값을 리턴하거나 기존 atom의 값을 수정하는 역할을 수행한다.

  **store와 같은 외부요인이 아닌 react 내부의상태를 활용하고 context API를 통해 구현되어있기 때문에 더 리액트에 가까운 라이브러리**

  - 장점

    Redux, MobX에 비해 더 간단한 구조를 갖고있기 때문에 작은 프로젝트에 적합

    Recoil을 사용한다면 component가 렌더링 되는 시기, 상태 등을 세밀하게 제어할 수있다.

    위의 Redux와 다르게 Reactive 메커니즘을 탑재하고 있어서 **동적인 기능을 더 쉽게 구현 가능하다.**

    => 비동기 처리 라이브러리에 의존할 필요가 없다.

  - 단점

    아직 베타버전이고, 현재 업데이트도 없고..

    사용자 커뮤니티도 비교적 빈약하다.

    상태관리가 굉장히 세분화 되어있기 때문에 초심자가 디버깅하거나 테스트를 진행하기엔 어려울 수 있다.

- MobX

  Redux의 여러 점을 보완하여 나온 상태관리 라이브러리이다.

  Redux보다 조금 더 객체지향적이며, 불변성을 유지하기 위한 라이브러리를 굳이 사용할 피요가 없다.

  store에 제한이 없다.

  - 장점

    Redux에 비해 조금 더 쉬운 러닝커브를 갖고 있다.

    객체 지향적이고 캡슐화를 지원하기에 개발자 친화적이다.

    Redux에서 제공하지 않는 반응형 메커니즘을 제공 => 조금 더 쉽게 동적 웹앱 제작 가능

  - 단점

    웹앱 규모가 커지면서 로직이 MobX에 자동 업데이트에 의존하기에 디버깅이 조금 어렵다.

    Redux에 비해 커뮤니티가 크지 않다.

    Validation(검증) 구현에 있어 코드가 조금 번잡스럽다 알려져있다.

<br />

## 출처

https://blog.toktokhan.dev/react-%EC%83%81%ED%83%9C%EA%B4%80%EB%A6%AC-%EC%B5%9C%EA%B0%95%EC%9E%90%EB%8A%94-f0753ad7d186

https://velog.io/@fredkeemhaus/Redux-Mobx-Recoil%EC%97%90-%EB%8C%80%ED%95%B4-%EB%B9%84%EA%B5%90%ED%95%98%EA%B3%A0-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90

https://velog.io/@2ast/React-Recoil-selector-%EB%A7%8C%EC%A0%B8%EB%B3%B4%EA%B8%B0
