## javascript와 typescript

자바스크립트는 **동적 타입 언어**이다. 따라서 특정 변수를 선언했을 때 다른 타입으로도 대입할 수 있다.

```
let value = 1;

value = 'Cool';
value = {a: 1};
value = [1,2,3,4,5,6];
```

또한 함수를 만들 때도 파라미터에 어떠한 타입의 값이든 넣어줄 수 있다.

```
function wrap(value){
    return { value };
}

wrap(1);
wrap('Hello Wolrd');
wrap({a: 1});
```

자바스크립트에서는 **변수의 타입이 런타임에 결정**된다. 즉, **코드가 실행되는 단계에서 타입이 결정**된다.

**정적 타입 언어는 변수의 타입이 컴파일 타임에 결정**된다. 따라서 코드를 실행하지 않아도 변수에 잘못된 타입이 들어가는 상황에서 문제를 감지할 수 있다.

동적 타입 언어는 **타입을 유연**하게 가질 수 있고 **컴파일 에러도 존재하지 않기 때문에** 개발 입문자가 배우기 쉽고 프로젝트를 빠르게 개발할 수 있다.

그러나 프로젝트의 규모가 커질수록 실수할 가능성도 높아지고 타입 추론이 일부만 되기 때문에 개발이 불편할 수 있다.

코드를 실행해 결과물을 확인해야만, 코드가 타입 문제없이 제대로 실행됐는지 알 수 있다.

그래서 이 단점을 보완하기 위해 **정적 타입 언어인 타입스크립트**를 사용해보자.

<br />

---

### 기본 타입

타입스크립트에서 변수를 선언할 때 해당 변수의 타입을 지정할 수 있다. 타입을 지정할 때는 변수 이름 뒤에 **: 타입** 형태로 지정한다.

```
let message: string = 'Hello World';
let value: number = 1;

let nullableString: string | null = null;
nullableString = 'Hi';

let undefinedOrNumber: undefined | number;
undefinedOrNumber = 10;

let numberOrStringOrNull: number | string | null = null;
numberOrStringOrNull = 1;
numberOrStringOrNull = 'Bye';
numberOrStringOrNull = null;

let isCompleted: boolean = true;
isCompleted = false;

let anyValue: any = null;
anyValue = undefined;
anyValue = 1;
anyValue = 'hello world';
```

타입을 선언할 때 **| 문자는 Union Type**이라고 부른다.

string | null이라고 되어있으면 이는 문자열 또는 null이라는 것을 의미한다.

any 타입의 경우에는 모든 타입의 값을 대입할 수 있다.

<br />

---

### 합수 타임

```
function sum(a: number, b:number){
    return a + b;
}

const result = sum(1,2);
```

이 함수는 파라미터 a와 b의 타입이 number로 지정되어있다.

또한, 함수를 선언할 때 **반환값의 타입**을 미리 지정할 수도 있다.

```
function s(a:number, b:number): number{
    return a + b;
}
```

이렇게 반환값 타입을 따로 선언할 경우, 함수가 지정한 타입과 다른 값을 반환한다면 오류가 발생할 것이다.

```
function s(a:number, b:number): number{
    if(a === 0){
        return null; //오류 발생
    }
    return a + b;
}
```

<br />

---

### 옵서녈 파라미터(Optional Parameter)

옵서녈 파라미터는 **생략해도 되는 파라미터**를 의마한다.

```
function process(a: number, b:number, isDouble?: boolean){
    const sum = a + b;
    return isDouble ? sum * 2 : sum;
}

const total = process(1,2);
const doubledTotal = process(1,2,true);
```

isDouble 타입은 boolean | undefined로 설정된다.

<br />

---

### 여러 반환값 타입을 지닌 함수

**함수는 여러 반환값 타입을 지닐 수 있다.** 따라서 함수를 선언할 때 타입을 명시해야 하는데, 타입을 미리 명시하지 않으면 해당 함수에서 반환하는 값을 자동으로 추론한다.

```
function hello(value: string, returnNull?: boolean){
    if(returnNull){
        return null;
    }

    return `Hello ${value}`;
}

const result = hello('World');
const nullResult = hello('World', true);
```

반환값의 타입을 string | null로 추론할 수 있다.

만약 이 상황에서 result의 문자열 내장함수를 사용하려고 한다면?

```
const replaced = result.replace('Hello', Bye');
```

그렇담 result가 null일 수도 있기 때문에 오류가 발생한다.

이 오류를 고치려면

```
//null이 아닐 때를 조건걸기
if(result !== null){
    const replaced = result.replace('Hello', 'Bye');
}

//옵서녈 체이닝 연산자(?)를 사용
const replaced = result?.replace('Hello', 'Bye');
```

<br />

---

### interface

interface는 **타입스크립트에서 객체나 클래스를 위한 타입을 정할 때 사용**한다.

```
interface Profile{
    id: number;
    username: stirng;
    displayName: string;
}

function printUsername(profile: Profile){
    console.log(profile.username);
}

const profile: Profile = {
    id: 1,
    username: 'velopert',
    displayNmae: 'Minjun Kim',
}

prinstUsername(profile);
```

또한 다른 interface에서 참조하는 것도 가능하다.

```
interface Profile{
    id: number;
    username: stirng;
    displayName: string;
}

interface Relationship{
    from: Profile;
    to: Profile;
}

const relationship: Relationshop = {
    from: {
        id: 1,
        username: 'velopert',
        displayName: 'Minjun Kim',
    },
    to: {
        id: 2,
        username: 'johndoe',
        displayName: 'John Doe',
    },
};
```

<br />

---

### interface 상속하기

기존 interface 타입에 필드를 더 추가할 때는 상속을 통해 처리할 수 있다.

```
interface Profile{
    id: number;
    username: stirng;
    displayName: string;
}

interface Account extends Profile{
    email: string;
    password: string;
}

const account: Account = {
    id: 1,
    username: 'johndoe',
    displayName: 'John Doe',
    email: 'john@email.com',
    password: '123123',
};
```

<br />

---

### 옵서녈 속성

interface에서 옵서녈 속성을 다룰 때도 똑같이 물음표를 사용한다.

```
interface Profile{
    id: number;
    username: stirng;
    displayName: string;
    photoURL?: string;
}

const profile: Profile = {
    id: 1,
    username: 'velopert',
    displayNmae: 'Minjun Kim',
}

const profile: Profile = {
    id: 1,
    username: 'velopert',
    displayNmae: 'Minjun Kim',
    photoURL: 'photo.png',
}
```

photoURL의 타입은 string | undefined로 지정된다.

<br />

---

### 배열 타입

타입 뒤에 []를 붙여주면 됩니다.

```
const numbers: number[] = [1,2,3,4,5];
const text: string[] = ['hello', 'world'];

interface Person {
    name: string;
}

const people: Person[] = [{name: 'John Doe}, {name: 'Jane Doe'}];
```

<br />

---

### Type Alias

Type Alias는 타입에 별칭을 붙여주는 기능이다. 이를 통해 객체의 타입을 지정할 수도 있고, 다른 타임에 별칭을 지어줄 수도 있다.

```
type Person = {
    name: string;
};

const person: Person = {
    name = 'john Doe',
};

//Person 타입의 객체로 이루어진 배열
type People = Person[];

const people : People = [{name: 'john Doe'}];

type Color = 'red' | 'orange' | 'yellow';
const color: Color = 'red';
```

객체의 타입은 interface로도 선언할 수 있고, type으로 선언할 수 있다.

Color의 타입은 'red', 'orange', 'yellow' 중 하나의 값만 지정할 수 있는 타입이다.

type을 사용하여 만든 객체 타입에도 필드를 추가할 수 있는데 이때는 & 문자를 사용한다.

```
type Person = {
    name: string;
};

type Employee = Person & {
    job: string;
};

const employee: Employee = {
    name: 'john',
    job: 'Programmer',
};
```

<br />

---

### Generic

제네릭은 함수, 객체, 클래스 타입에서 **사전에 정하지 않은 다양한 타입을 다룰 때 사용**한다.

<br />

---

### 함수에서 Generic 사용하기

만약 Generic을 사용하지않는다면 그냥 any 타입을 사용해야 한다. 사전에 정의하지않았으니까.. 그냥 아무거나 받아야겠지.

```
function wrap(value: any){
    return {value};
}

const result = wrap('Hello Wolrd');
```

이렇게 하면 어떤 값이든 인자로 넣어줄 수 있지만, result의 타입 추론이 불가능하다.

**이런 상황에서 Generic을 사용하면 타입추론이 가능하게 만들 수 있다.**

```
function wrap<T>(value: T){
    return {value};
}

const result = wrap('Hello World');
```

value의 타입이 T라고 지정해주면 result.value의 값이 string인 것이 추론이 된다.

```
function wrap<T>(value: T){
    return {value};
}

interface Person {
    name: string;
}

const person: Person = {name: 'john doe'};

const result = wrap(person);
console.log(result.value.name); //john doe
```

result.value.name 값이 string인 것도 정상적으로 추론된다.

<br />

---

### 객체에서 Generic 사용하기

객체 타입의 특정한 필드에 다양한 값이 올 수 있다고 가정해보자.

```
interface Item<T>{
    id: number;
    data: T;
}

interface Person{
    name: string;
}

interface Place{
    location: string;
}

const personItem: Item<Person> = {
    id: 1,
    data: {
        name : 'john',
    },
};

const placeItem: Item<Place> = {
    id: 1,
    data: {
        location : 'Korea',
    },
};
```

만약 Type Alias에서 제네릭을 사용한다면,

```
type Item<T> = {id: number, data: T};
```

<br />

---

### js와 ts의 장단점

```
js는 웹의 표준 언어이자 동적 타입 언어로 유연하게 사용 가능하다. 따라서 배우기 쉽고 빠르게 개발할 수 있다.

하지만 런타임에 변수 타입이 정해지므로 코드를 실행하는 도중 오류가 뜰 수도 있고 프로젝트 크기가 커질수록 실수할 가능성이 높아진다.

ts는 js의 상위 집합으로 정적 타입 언어이다. 컴파일 타임에 변수 타입이 정해지기 때문에 코드가 실행하기 전에 오류를 발견할 수 있기 때문에 코드의 안정성을 높일 수 있다.

하지만 학습 곡선이 있으며 설정과 컴파일이 필요한 단점이 있다.

프로젝트의 크기와 요구사항, 팀의 선호도 등을 고려하여 js와 ts 중 적합한 것을 선택하는 것이 좋다.
```

### 출처

https://velog.io/@theon2/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%99%80-%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98-%EC%B0%A8%EC%9D%B4-%EC%9E%A5%EB%8B%A8%EC%A0%90%EC%97%90-%EB%8C%80%ED%95%B4-%EC%84%A4%EB%AA%85%ED%95%B4%EC%A3%BC%EC%84%B8%EC%9A%94
