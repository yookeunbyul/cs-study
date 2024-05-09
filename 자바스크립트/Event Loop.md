## Event Loop

### Javascript의 특징

JavaScript는 **싱글 스레드 언어**(single-threaded language)로 한 번에 하나의 작업만 처리할 수 있다. => 콜 스택이 하나만 있음..

콜 스택이 함수 실행 컨텍스트 push하고 pop하면서 함수를 차례대로 실행...

하지만 실제로 동작하는 웹 애플리케이션은 많은 task가 동시에 처리되는 것처럼 느껴진다.

왜? 자바스크립트가 비동기로 작동하기 때문에..

근데 자바스크립트가 비동기 동작을 지원하는 게 아니라 **핵심 요소는 브라우저가 가지고 있다.**

---

### 브라우저의 구조

<img src="https://github.com/yookeunbyul/cs-study/assets/91243651/ff29cf6e-0066-4fc0-9825-320ddf12142a" />

- 브라우저

  - 자바스크립트 엔진

    - 콜 스택 : **실행된 코드의 환경(실행 컨텍스트)을 저장하는 자료 구조로, 함수 호출 시 이곳에 저장**된다. 함수를 호출하면 해당 함수의 기록을 스택 맨 위에 추가하고, 우리가 함수 결과 값을 반환하면 스택에 쌓여있던 함수는 제거된다. 엔진은 그냥 스택에 들어오는 코드를 순차적으로 실행한다.

    - 메모리 힙 : **메모리 할당**이 일어나는 곳이다.

  - Web APIs : **비동기 작업을 처리하기 위해 브라우저가 제공하는 API.**

    DOM, Ajax, TimeOut 등이 있다. 콜 스택이 비동기 요청을 만나면 **비동기 작업의 정보와 콜백 함수를 함께 Web API에 전달**한다.

    브라우저는 Web API의 비동기 작업을 JavaScript 엔진과 **별개의 스레드에 위임**한다.

    해당 스레드가 **비동기 작업을 완료하면 함께 전달받은 콜백 함수를 콜백 큐에 넣는다.**

  - Callback Queue : Web API에서 비동기 작업이 처리된 후의 **콜백 함수가 보관되는 영역.**

    먼저 들어온 함수를 가장 먼저 처리한다.

  - Event Loop : Event Loop는 Call Stack과 Callback Queue의 상태를 체크하여, **Call Stack이 빈 상태가 되면, Callback Queue의 첫번째 콜백을 꺼내 Call Stack에 추가**한다. 이러한 반복적인 행동을 틱(tick) 이라 부른다.

즉, Event Loop는 콜 스택과 콜백 큐를 비교해서 콜 스택이 비어있을 때 콜백 큐에 가장 앞에 있는 콜백을 콜 스택에 넘겨주는 역할을 한다.

---

### Event Loop 예제

```
  console.log(1);

  setTimeout(
    function cb() {
      console.log(2);
    }
  ,0);

  console.log(3);
```

순서는 1 => 3 => 2 이 순서대로 진행된다.

1. console.log(1)가 Call Stack에 추가된다. 그 이후 실행되어 콘솔에 출력된 뒤, Call Stack에서 제거된다.

2. 그 다음, setTimeOut(...)이 Call Stack에 추가된다.

3. setTimeOut(...)가 실행이 되며 브라우저가 제공하는 timer Web API를 호출하고 Call Stack에서 제거된다.

4. console.log(3)이 Call Stack에 추가된다. 그 이후 실행되어 콘솔에 출력된 뒤, Call Stack에서 제거된다.

5. setTimeOut(...) 함수의 0ms만큼의 시간이 지난 뒤 Callback으로 전달한 cb 함수가 Callback Queue에 추가된다.

6. Event Loop는 Call Stack이 비어있는 것을 확인하고 Callback Queue를 살펴보고, 함수 cb를 발견한 후 Call Stack에 cb 함수를 추가한다.

7. cb 함수가 실행 되고 내부의 console.log(2)가 Call Stack에 추가된다.

8. console.log(2)가 콘솔에 출력되고 Call Stack에서 제거되고, cb 함수도 제거된다.

---

### 출처

https://velog.io/@jinyoung985/JavaScript-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84Event-Loop%EB%9E%80

https://seokzin.tistory.com/entry/JavaScript-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84-Event-Loop#%F-%-F%--%-E%--Promise%EB%-A%--%--%EB%-F%--%EA%B-%B-%EB%-B%A--
