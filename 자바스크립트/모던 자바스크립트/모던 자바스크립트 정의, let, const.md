## 모던 자바스크립트 정의, let, const

### 모던 자바 스크립트란?

ECMAScript? JavaScript?

ECMA는 European Computer Manufacturer's Association 의 약자로 **정보 통신 시스템을 위한 표준화 기구**

다양한 브라우저에서 Javascript가 동일하게 동작하려면 표준이 필요했고, **이 표준을 정해준 곳이 ECMA**이며 그 표준 명이 ECMAScript이다.

즉, javascript의 사용설명서, 표준이 곧 ECMAScript이다.

---

### 그래서 모던 자바 스크립트가 뭔데?

**모든 모던 브라우저에서 지원하는 자바 스크립트 코드** 라고 정의할 수 있다.

모던 브라우저란? 우리가 사용하는 chrome, firefox, safari, edge.. 등이 있다.

let, const, arrow function 등의 현재 자바스크립트의 주요 문법들이 **ES6(ECMA2015)** 에서부터 시작되었으므로, 현재의 모던 자바 스크립트가 위와 같은 정의가 된다고 할 수 있다.

결국 **모던 자바 스크립트란 ES6+ 이상을 사용하는 자바 스크립트이다.**

---

### let, const

모던 자바스크립트를 사용하려면

#### let, const을 사용해 변수를 선언하자

ES5로 개발하던 개발자들은 var를 이용해서 변수를 선언할 것이다.

하지만 많은 문제점이 존재했고 이를 해소하기 위해 let과 const가 등장했다.

---

### const

const를 사용해서 변하지않는 상수를 표현하자!

**var는 중복선언, 재할당이 가능하다.**

이러한 특징들이 코드가 길어질수록 **모든 코드를 읽어보게끔 했고, 동작의 결과를 유추하는데 어려움을 준다.**

```
var plusPrice = 0.2;
var productPrice = 1000;
var totalPrice = productPrice + (productPrice*plusPrice);

return `최종 금액은 ${totalPrice} 입니다.`;
```

이렇게 짧은 코드는 사실 var를 사용해도 아무런 문제가 없다.

하지만 저 가운데 엄청나게 많은 코드가 있다면 어떻게 될까?

```
var plusPrice = 0.2;
var productPrice = 1000;
var totalPrice = productPrice + (productPrice*plusPrice);

// 또 다른 코드들 1
// 또 다른 코드들 2
// 또 다른 코드들 3
// .
// .
// .
// .
// .
// .
// .
// .
// 또 다른 코드들 100


return `최종 금액은 ${totalPrice} 입니다.`;
```

var로 선언된 변수들은 언제든지 수정이 가능하기에(어디서든 접근 O) 이 코드의 결과가 명확해지지않고 이 사이의 코드들을 다 읽어야 한다.

그래서 var의 특성을 보완하고자 const라는 것이 탄생했다.

**const는 동일 블록 내에서 재할당이 되지 않는 변수 선언 방식**이다.

즉 값 자체가 절대 바뀌지 않는다는 것인데, **ES6는 대신 배열이나 객체에서의 값 변경은 가능하다.**

```
const plusPrice = 0.2;
const productPrice = 1000;
const totalPrice = productPrice + (productPrice*plusPrice);

// 또 다른 코드들 1
// 또 다른 코드들 2
// 또 다른 코드들 3
// .
// .
// .
// .
// .
// .
// .
// .
// 또 다른 코드들 100


return `최종 금액은 ${totalPrice} 입니다.`;
```

이렇게 변수를 선언해주면 중간에 어떤 코드가 들어와도 위에 const는 변하지 않으니 결과를 빠르게 유추할 수 있게된다.

---

### let

let은 const처럼 중복선언은 불가능하다 재할당이 가능하다.

즉, 변할 수가 있다.

var는 렉시컬 스코프(자바스크립트 엔진은 어디서 호출했는지가 아니라 **함수를 어디서 정의했는지에 따라 상위 스코프를 결정**)이고 let은 블록 스코프다. const도 블록 스코프를 따른다.

var는 모든 범위에서 사용이 가능하지만 왜냐? 어디에서 정의하느냐에 스코프가 결정되니깐..

let과 const는 중괄호 내부 { } 에서 사용이 가능하다고 말할 수 있다.

---

### let, const 사용 이유 정리

결국 var를 사용하면 코드를 예측하기가 힘들고 어디서든지 변경 위험성이 있기 때문에

우리는 let과 const를 사용해야 한다.

const를 기본, let을 변경 될 값에 사용해 **예측 가능하도록** 만드는 것이 중요하다.

---

### 출처

https://velog.io/@himprover/%EC%9D%B4%EC%A0%9C%EB%8A%94-%EB%AA%A8%EB%8D%98-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%A5%BC-%EC%95%8C%EC%95%84%EC%95%BC%EC%A7%80-%EC%A0%95%EC%9D%98-let-const#%EA%B7%B8%EB%9E%98%EC%84%9C-%EB%AA%A8%EB%8D%98-%EC%9E%90%EB%B0%94-%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%8A%94-%EB%AD%94%EB%8D%B0
