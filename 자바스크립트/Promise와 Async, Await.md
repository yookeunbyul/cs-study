## Promise와 Async, Await

우리는 비동기 처리를 한다.

비동기는 요청을 보내고 응답이 올 동안 기다리는 것이 아닌 다음 작업을 할 수 있다.

그래서 비동기 요청을 하고 응답이 오면 그 응답을 처리할 **콜백 함수**를 호출하게 되는데, 처리 순서를 보장하기 위해 여러 개의 **콜백 함수를 중첩하면서 복잡도가 높아지는 콜백 헬(Callback Hell)이 발생**한다.

```
step1(function(value1) {
  step2(value1, function(value2) {
    step3(value2, function(value3) {
      step4(value3, function(value4) {
        step5(value4, function(value5) {
            // value5를 사용하는 처리
        });
      });
    });
  });
});
```

그래서 이러한 단점때문에 비동기 처리를 위한 또 다른 패턴으로 **프로미스(Promise)를 도입**했다.

<br />

---

### Promise

Promise는 **비동기 연산의 상태를 나타내는 객체**이다.

- 비동기 처리가 진행중이면 'pending'

- 성공이면 'fulfilled'

- 실패면 'rejected'

라는 상태값을 가진다.

그래서 이 상태값을 가지고 **then(promise 객체 반환)이나 catch(에러 처리)와 같은 후속 처리 메소드로 체이닝**하여 여러 개의 프로미스를 연결하고 비동기 프로그래밍을 할 수 있다.

<br />

---

### Async / Await

자바스크립트의 비동기 처리 패턴 중 가장 최근에 나온 문법으로 콜백 함수와 프로미스의 단점을 보완하고 개발자가 읽기 좋은 코드를 작성할 수 있게 도와준다.

```
async function 함수명() {
  await 비동기_처리_메서드_명();
}
```

- async 개념

  function 앞에 async를 붙이면 해당 함수는 항상 **promise 객체**를 반환한다.

- await 개념

  await는 async 함수 안에서만 동작한다.

  async 키워드로 정의한 함수 내에서 호출되는 promise 앞에 await 키워드를 쓰면, **promise가 완료 될 때까지(비동기 처리가 완료될 때까지) 코드의 실행을 멈출 수가 있다.**

  promise가 처리되면 그 결과와 함께 실행이 재개된다.

  이를 통해, 비동기 코드를마치 동기 코드처럼 쉽게 작성할 수 있다.

  처리되는 동안 **엔진이 다른 일(다른 스트립트를 실행, 이벤트 처리 등)을 할 수 있기 때문에**, CPU 리소스가 낭비되지 않는다.

- async await 에러 제어

  await의 에러 핸들링은 반드시 try-catch 블록에서 해야 한다.

  ```
  async function f() {

      try {
          let response = await fetch('http://유효하지-않은-주소');
      } catch(err) {
          alert(err); // TypeError: failed to fetch
      }
  }

      f();
  ```

<br />

### 출처

https://velog.io/@khy226/%EB%8F%99%EA%B8%B0-%EB%B9%84%EB%8F%99%EA%B8%B0%EB%9E%80-Promise-asyncawait-%EA%B0%9C%EB%85%90

https://www.youtube.com/watch?v=cDu9A5dl1J8&list=PLBh_4TgylO6CI4Ezq3OLRRzg2NAn3FLPB&index=3
