## var와 let, const

```
var, let 키워드는 변수를 선언할 때 사용하고 const 키워드는 상수를 선언할 때 사용한다.
```

<img src="https://github.com/yookeunbyul/cs-study/assets/91243651/00759945-6f8c-4e9f-bc14-4d4006461251" />

### var

var로 선언하면 같은 이름으로 **중복 선언이 가능**하다. **재할당이 가능하다.**

```
var variable = 1;
var variable = 2;
console.log(variable); // 2
```

**초기값을 할당(초기화)하지 않으면 자동으로 undefined 값으로 초기화된다.**

### const

const는 **중복선언과 재할당이 불가능**하며 선언과 동시에 초기화 해주어야한다.

```
const constance = 0;
constance = 1; // 재할당 x

const initial; // 선언과 동시에 초기화 해주어야한다.

const count = 0;
let count; //중복선언 X
```

### let

let은 초기화해주지 않아도 **재할당이 가능**하다. **중복선언은 불가능하다.**

```
let count;
console.log(count); //undefined

count = 0;
console.log(count); //0 : 재할당 가능
```

<br />

## 스코프

스코프는 코드가 **변수에 접근할 수 있는 범위**를 뜻한다.

- **함수 스코프 : function 함수로 둘러싼 범위**

  ```
  function getName(user){
    return user.name;
  }

  let getAge = function (user) {
    return user.age;
  }
  ```

- **블록 스코프 : 중괄호로 둘러싼 범위**

  ```
  if (true){
    	consol.log(`i am in the block`);
  }

  for (let i =0; i<10;, i++) {
    console.log(i);
   }

   {
  console.log(`it works`);
   }
  ```

- **전역 스코프**

총 세개의 스코프가 있다.

---

<br />

**var 키워드로 선언된 변수는 함수 스코프를 가진다.**

**let 키워드로 선언된 변수는 블록 스코프를 가진다.**

만약 변수가 어느 함수에도 속하지 않은 최상위 함수 외부에 선언된 변수라면 **전역 스코프**를 가진다.

<br />

### 함수 스코프 vs 블록 스코프

```
function varkeyword () {
    var a = 'hello'
    if(true){
    var a = 'hi'
    }
    console.log(a) // hi
    // var 키워드는 함수스코프를 가지기 때문에 if 블럭 안에 있는 변수 a와 바깥에 있는 변수 a는 같은 스코프를 가진다. => 블록 스코프는 그냥 무시.
    // var는 같은 스코프를 가지게 되면 중복 선언을 허용한다. 그러므로 hi 가 출력된다.
}

varkeyword();
```

```
function letkeyword () {
    let a = 'hello'
    if(true){
    let a = 'hi'
    }
    console.log(a); // hello
    // 'hi'값은 if블럭 내부에서만 유효하기 때문에 블럭 바깥에서 접근하는 a 변수는 같은 스코프인 'hello'를 가르킨다.
}

letkeyword();
```

```
function main() {
    for (let i=0; i<5; i++){
        console.log(i); // 0~4 까지 한번씩 찍힌다.
    }
    	console.log(i); // 레퍼런스 에러 => 블록 스코프이기 때문에 접근할 수 없음
}

main()
```

```
function main2() {
    for (var i=0; i<5; i++){
        console.log(i); // 0~4 까지 한번씩 찍힌다.
    }
    console.log(i); // 5 까지 찍힌다.
    //var은 함수스코프이기때문에 for블럭 외부에서도 증감식에 증가된 값이 찍히는 것이다.
}

main2()
```

### 전역 스코프

```
var aVar = 'varHello';
let aLet = 'letHello';
```

이 두 변수는 함수로 감싸져 있지 않기 때문에 프로그램에서 전역적으로 접근 할 수 있는 전역변수라고 볼 수 있다.

<br />

## 호이스팅

변수 호이스팅이란, 프로그램이 실행되기 이전에 **변수의 선언과 변수의 초기화를 분리해서 변수의 선언부분만 프로그램 맨위로 끌어올려주는 것**을 의미한다.

- var

  ```
  console.log(num); // undefined
  // 왜 undefined가 찍힐까??
  //var키워드의 호이스팅 특징이다.
  //var키워드는 변수의 선언을 맨 위로 호이스팅 할때 undefined로 초기화시킨다.

  var num = 10;

  console.log(num); // 10
  ```

- let

  ```
  console.log(num2); // Uncaught ReferenceError: Cannot access 'num2' before initialization
  // 참조 에러 : num2를 초기화하기 이전에 접근 할 수 없다.

  let num2 = 10;
  // let의 호이스팅 특징 - 변수 선언 부분 을 위로 호이스팅을 하긴 하지만 var과 다르게 초기화 시키진 않는다.
  //undefiend로 초기화하는 것이 아닌 에러를 띄워버린다.
  ```

- **둘다 호이스팅은 되지만 var는 undefined로 초기화를 시키고, let은 초기화 시키지 않는다.**

- const

  const 역시 호이스팅은 되지만 undefined로 초기화 되지 않는다.
