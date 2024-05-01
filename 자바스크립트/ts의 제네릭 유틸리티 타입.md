## ts의 제네릭 유틸리티 타입

`제네릭` => 함수, 객체, 클래스 타입에서 사전에 정의하지않은 다양한 타입을 다룰때 사용한다.

`제네릭의 유틸리티 타입` => **이미 정의한 타입을 변환**할 때 사용하는 타입 문법이다.

- Partial< T >

  **특정 타입의 부분집합**을 나타내는 타입이다.

  ```
  interface User {
      name: string;
      email: string;
      age: number;
  }

  function updateUser(user: User, fieldUpdate: Partial<User>) {
      return { ...user, ...fieldUpdate };
  }

  const user2 = updateUser(user, {
      email: 'dev-yujin@google.com',
  });
  ```

- Readonly< T >

  T의 모든 프로퍼티를 **읽기 전용**으로 설정하며, 재할당할 수 없다.

  ```
  interface User {
      name: string;
      email: string;
      age: number;
  }

  const user: Readonly<User> = {
      name: 'yujin'
      email: 'yujin@google.com',
      age: 29,
  };

  user.name = 'mimi'; // Cannot assign to 'name' because it is a read-only property.
  ```

- Record <K,T>

  <Key, Type>으로 Key(key):Type(value) 형태의 타입이다.

  ```
  interface Person {
    age: number
  }

  type Member = 'mimi' | 'yujin' | 'youngji';

  const example: Record<Member, Person> = {
      'mimi': {age: 25},
      'yujin': {age: 27},
      'youngji': {age: 29},
  }
  ```

- Pick< T >

  특정 타입에서 몇 개의 속성을 선택한 타입이다.

  ```
  interface User {
      name: string;
      email: string;
      age: number;
  }

  type AnonymousUserType = Pick<User, 'email' | 'phone'>;

  const user: AnonymousUserType = {
      email: 'dev-yujin@google.com',
      age: 29,
  };
  ```

- Omit<T,K>

  T에 대한 K의 차집합을 나타내는 타입이다.

  예를들어 User 타입 중 game은 제외하고 email과 password만 필요하다고 가정해보자.

  ```
  interface User {
      email: string;
      password: string;
      game: {
          kill: number;
          death: number;
          assist: number;
      }
  }

  const userOne: Omit<User, 'game'> = {
      email: 'game123@google.com',
      password: '1234',
  };
  ```

### 출처

https://velog.io/@ongddree/TIL-Typescript-%EC%A0%9C%EB%84%A4%EB%A6%AD-%EB%B0%8F-%EC%9C%A0%ED%8B%B8%EB%A6%AC%ED%8B%B0-%ED%83%80%EC%9E%85
