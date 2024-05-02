## this란

핵심1. this는 '**자신이 속한 객체를 가리키는 변수**'이다.

핵심2. this는 '**자신을 호출하는 방법에 따라 다른 값**'을 가르킨다.

즉, **자신이 속한 객체를 가리키는 변수지만 호출하는 방법에 따라 가르키는 값이 달라질 수 있다.**

---

<br />

```
var someone = {
    name: 'KMS',
    someFunction: function() {
        console.log(this);
    }
}
```

someone 객체를 만들고 객체 내의 함수인 someFunction()을 호출한다.

```
someone.someFunction();
```

그럼 콘솔에 this가 찍히게 되는데, **당연히 자신이 속한 객체인 someone을 가리키고 있다.**

```
{name: 'KMS', someFunction: f}
```

someFunction()을 직접적으로 호출(실행)한 객체가 someone이기 때문이다.

만약 객체 내의 함수를 직접적으로 호출하지않고 새롭게 정의해서 부르면 어떻게 될까?

```
ver myFunction = someone.someFunction;
myFunction(); // 호출
```

그럼 똑같이 콘솔에 this가 찍히는데, 이번에는 someone 객체가 아닌 window 객체가 콘솔에 찍히게 된다.

```
Window {window: Window, self: Window, documnet: document, name: '', loaction: Location, ...}
```

왜지? **바로 myFunction 함수를 호출하는건 someone 객체가 아닌 전역객체인 window 객체이기 때문이다.**

그렇다면

```
document.getElementById('btn').addEventListener('click', someone.someFunction);
```

이렇게 버튼이벤트를 등록해 버튼을 클릭했을 때 함수가 호출되도록 하면 this는 무엇을 가르키겠는가?

```
<button id="btn">Button</button>
```

바로 함수를 부른 버튼을 가르킨다.

**이렇게 this는 호출하는 방법에 따라 가르키는 값이 달라진다.**

그럼 이 this 값을 고정시킬 수는 없을까?

있다. **함수를 어떻게 호출했는지 상관하지 않고 this 값을 설정할 수 있는 bind 메서드가 있다!**

```
var bindedSomeFunction = myFunction.bind(someone);
//아까 위에서 만들었던 myFunction 함수에 someone 객체를 바인드 해준다.

bindedSomeFunction();
document.getElementById('btn').addEventListener('click', bindedSomeFunction);
```

그냥 호출해도 버튼으로 이벤트를 등록해서 호출해도

```
{name: 'KMS', someFunction: f}
```

동일하게 bind 해놓은 someone 객체를 가리키고 있다.

### 출처

https://1nnovator.tistory.com/66
