---
title: "프로젝트SET"
excerpt: "SETUP"

categories:
  - Categories8
tags:
  - [tag1, tag2]

permalink: /categories8/TYPESCRIPT기초/

toc: true
toc_sticky: true

date: 2024-09-23
last_modified_at: 2024-09-23
---

### ☘️ 자바스크림트와 타입스크립트의 차이점

#### 1. JavaScript는 동적 타입시스템

동적 타입 언어는 프로그램을 실행한 이후에 변수, 함수의 타입이 결정된다.
타입이 고정되지 않아서 같은 변수에 여러 타입의 값을 자유롭게 할당할 수 있다.

TypeScript는 정적 타입시스템
타입시스템 중에 프로그램이 실행되기 전에 모든 변수와 표현식의 타입을 확인하고 고정하는 방식

=> 이러한 차이점으로 TypeScript는 더 안정적으로 실수 없이 개발을 할 수 있도록 도와준다.

#### TypeScript의 동작원리

: 타입스크림트는 컴파일이라는 과정안에서 문법, 타입 체크등을 수행해준다.
자바스크림트에서 타입스크립트로 변환

1. 컴파일 시작 : tsc 명령어를 사용해 타입스크립트 컴파일러를 실행한다.
2. 파일 로드 : 컴파일러가 모든 입력 파일과 import된 파일을 로드한다.
3. 코드 분석 : 코드를 읽어들여 프로그램 구조를 나타내는 AST(구문 트리)를 만든다.
4. 심볼 테이블 생성 : 코드를 분석하여 변수와 함수 등 모든 요소의 관계를 정리한 심볼 테이블을 만든다.
5. 자바스크립트 코드로 변환 : AST를 바탕으로 타입스크립트 코드를 자바스크립트 코드로 변환한다.
6. 타입 검사 : 컴파일러가 코드를 검사하여 타입 오류를 찾는다. 오류가 없다면 최종 자바스크립트 파일을 생성한다.

---

#### TypeScript를 실행

```js
yarn create vite
```

- react와 TypeScript를 선택

---

#### TypeScript의 선언

- number : 숫자
- string : 문자열
- Array : 배열
- 인터페이스 : interface (객체 형태로 key value형태로 작성)
- 타입 별칭 : type

```js
type User = {
  name: string;
  age:number;
  isValid:boolean;

  let userArr: User[] = [
    {
      name: "Neo",
      age: 10,
      isValid: true,
    },
    ]
```

- Null과 Undefined
- 모든 타입 : any
- void : return 값이 없을 때를 의미한다.
- Union(유니언) : OR연산자와 같이 A이거나 B이다.
  두 가지 type을 가져야할 때 사용한다.
- 인터섹션(Intersection) : 두 개 이상의 타입을 모두 만족해야한다.

#### 이런 타입도 있다!

readonly : 읽기 전용
Tupe : 튜플
enum : 열거형
Object : 객체
unknown : 알 수 없는 타입
Never : 아무타입도 포함하고 있지 않음

---

#### 복잡한 타입 표현

- 인터페이스 : 객체 형태의 타입을 정의하는데 주로 사용
- 타입 별칭 : 객체 형태 뿐만 아니라 유니온 타입, 튜플, 매핑된 차입등 복잡한 타입 표현에 유리하다. typeA = B | C 처럼 더 다양한 타입을 정의 가능

---

#### ☘️ 타입 어노테이션

: 사용하려고 하는 변수, 함수 등 옆에 : 기호와 함께 타입을 넣어주면 된다.
어떤 값이 어떤 타입을 참조하고 있는지 개발자가 직접 타입을 작성해서 타입스크립트에게 알려주는 행동

#### ☘️ 타입 추론

: 개발자가 타입을 명시적으로 지정하지 않아도 타입 안전성을 유지할 수 있도록 도와줌

---

### ☘️ 제네릭

: 타입을 마치 클래스나 함수 등에서 파라미터처럼 사용하는 것
타입을 변수처럼 사용하는 것을 의미한다.

```js
function pringAnything<T>(arr: T[]): void {
  for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
  }
}

pringAnything < string > ["a", "b", "c"];
pringAnything([1, 2, 3]);
```

useState 예제

```js
import { useState } from "react";

function App() {
  const [counter, setCounter] = useState < number > 0;
  const increment = () => {
    setcounter((prev) => prev++);
  };
  return <div onClick={increment}>{counter}</div>;
}
export default App;
```

---

## 유틸리티 타입

: Generic을 사용해서 타입을 efective 하게 쓸 수 있게 해줌

### Utility Type Tool

- Pick<T,K>
  : T에서 프로퍼티 K의 집합을 선택해 타입을 구성한다.

```js
interface Todo {
  title: string;
  description: string;
  completed: boolean;
}

type TodoPreview = Pick<Todo, "title" | "completed">;

const todo: TodoPreview = {
  title: "Clean room",
  completed: false,
};
```

- Omit<T,K>
  T에서 모든 프로퍼티를 선택한 다음 K를 제거한 타입을 구성한다.

```js
interface Todo {
  title: string;
  description: string;
  completed: boolenan;
}

type TodoPreview = Omit<Todo, 'description'>'

const todo: TodoPreview = {
  title: 'Clean room',
  completed: false,
};
```

- Exclude<T,U>
  : T에서 u에 할당할 수 있는 모든 속성을 제외한 타입을 구성한다.
- Partial<T>
  : T의 모든 프로퍼티를 선택적으로 만드는 타입을 구성한다.
  이 유틸리티는 주어진 타입의 모든 하위 타입 집합을 나타내는 타입을 반환한다.
  전체가 아닌 일부의 값을 사용하기 위해서 사용된다.
- ReadOnly<T>
  : T의 모든 프로퍼티를 읽기 전용으로 설정한 것
- Record<K,T>
  : 타입 T의 프로퍼티의 집합 K로 타입을 구성한다.
- Extract <T,U>
  : T에서 U에 할당 할 수 있는 모든 속성을 추출하여 타입을 구성
- ReturnType<T>
  T함수 타입의 반환 타입을 구성한다. 함수의 반환 타입을 추론하는데 유용하다.
- Parameters<T>
  : T함수 타입의 매개변수 타입을 튜플로 구성한다.
