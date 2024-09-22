---
title: "JavaScript(Map, Set)"
excerpt: "JavaScript"

categories:
  - Categories2
tags:
  - [tag1, tag2]

permalink: /categories2/JavaScript2/

toc: true
toc_sticky: true

date: 2024-07-23
last_modified_at: 2024-07-23
---

> ## 🌟추가자료구조(Map,Set), 일급객체함수, es6문법

## ⭐️ Map, Set (추가자료구조)

: 데이터의 구성, 검색, 사용을 효율적으로 처리 > 기존의 객체 또는 배열보다

### Map

: key / Value

- key에 어떤 데이터타입(유형)도 다 들어올 수 있다.
- Map은 키가 정렬된 순서로 저장되기 때문이다.
- 기능
  : 검색, 삭제, 제거, 여부 확인

  > 주요 메서드

- new Map() : 맵을 만든다.
- map.set(key, value) : key를 이용해 value를 저장
- map.get(key) : key에 해당하는 값을 반환 key가 존재하지 않으면 undefined를 반환
- map.has(key) : key가 존재하면 true, 존재하지 않으면 false를 반환
- map.delete(key) : key에 해당하는 값을 삭제함
- map.clear() : 맵 안의 모든 요소를 제거
- map.size : 요소의 개수를 반환

예시

```js
const myMap = new Map();
myMap.set("key", "value");

myMap.get("key");
```

## Map의 반복

- Map에서는 keys(), values(), entries()메소드를 사용하여
  키, 값 및 키-값쌍을 반복

  > => [for ...of 반복문]

  > for of 반복문을 사용하기 위해서 객체가 Symbol.iterator속성을 가지고 있어햐 함(iterator : 반복문)

```js
const myMap = new Map();
myMap.set("one", 1);
myMap.set("two", 2);
myMap.set("three", 3);

// console.log(myMap.keys());

for (const value of myMap.values()) {
  console.log(value);
}

console.log(myMap.entries);
for (const entry of myMap.entries()) {
  console.log(entry);
}
```

- .size // map의 사이즈
- .has("") // map에 해당 key가 존재하는지 검색

## ⭐️ Set

: 고유한 값을 저장하는 자료구조,
값만 저장한다. 키를 저장하지는 않는다. 값이 중복되지 않는 유일한 요소로만 구성된다. value만 넣음(집합)

```js
const mySet = new Set();
mySet.add("value1");
mySet.add("value2");
mySet.add("value2");

console.log(mySet.size); // 2 중복된 값 x
console.log(mySet.has("value1")); // true
console.log(mySet.has("value2")); // true
console.log(mySet.has("value3")); // false
```

- Iterator. 반복
  for (const value of mySet.values()) {
  console.log(value);
  }

---

## ⭐️ 일급객체함수

: 일급객체(First-class Object)란 다른 객체들과 일반적으로 적용 가능한 연산을 모두 지원하는 객체를 가르킴

- 유연하게 사용할 수 있음!

1. 변수에 함수를 할당
2. 함수를 인자로 다른 함수에 전달할 수 있다.

- 함수가 일급객체이기 때문에 가능함
  2-1 콜백함수 : 매개변수로서 쓰이는 함수
  2-2 고차함수 : 함수를 인자로 받거나 return하는 함수

3. 함수를 반환할 수 있다.

```js
function createAdder(num) {
  return function (x) {
    return x + num;
  };
}
const addFive = function (x) {
  return x + 5;
};
console.log(addFive(10));
```

4. this

### 화살표함수는 this를 컴바인딩 하지 않는다!!

```js
// 일급객체로서의 함수(2)
const person = {
  name: "john",
  age: 31,
  isMarried: true,
  //   sayHello: function () {
  //     console.log(`Hello my name is ${this.name}`);
  //   }, // this는 자기자신을 가르킴
  sayHello: () => console.log(`Hello my name is ${this.name}`),
};
person.sayHello();
```

5. 배열의 요소로 함수를 할당

```js
const myArr = [
  function (a, b) {
    return a + b;
  }, // 0번째 요소
  function (a, b) {
    return a - b;
  },
]; // 1번쨰 요소

// 더하기
console.log(myArr[0](1, 3));
// 빼기
console.log(myArr[1](10, 7));
```

6. 리팩토링 (함수의 재사용)

---

ES6 문법

1. 2015년 이전 =>var / let(변수), const(상수) 개정
2. arrow function

```js
function add() {}
let add = function () {};
let add = (x) => {
  return 1;
};
let add = (x) => 1;
```

3. 삼항연산자
   => condition ? true인 경우 : false인 경우

## ⭐️ 구조분해할당 : destructuring(de + structure+ ing)

de = not, structure = 구조 , 배열이나, 객체의 속성

1.  배열의 경우
    : 순서가 중요!

```js
// 1.
let [value, value2] = [1, "new"];
// 2.
let arr = ["value", "value2", "value3"];
let [a, b, c] = arr;

console.log(a);
console.log(b);
console.log(c);
```

2. 객체인 경우
   : key가 중요!

```js
let { name, age } = {
  name: "mbc",
  age: 30,
};

//새로운 이름으로 할당
let { name: newName, age: newAge } = user;
console.log(newName);
console.log(newAge);
```

## 단축속성명 (property shorthand)

```js
const name = "nbc";
const age = "30";

// key - value
const obj = { name, age };
const obj1 = { name: name, age: age };
```

## 전개구문 [...] (spread Operator)

: 객체나 배열을 풀어준다.

```js
// 배열 spreadOperator사용법
let arr = [1, 2, 3];
let newArr = [...arr];
console.log(arr);
console.log(newArr);
// 객체 spreadOperator사용법
let user = {
  name: "nbc",
  age: 30,
};
let user2 = { ...user };
```

## 나머지 매개변수(rest parameter)

=> ...args
:처음에는 넣어주지 않았지만 후에 값이 들어올 수 있음을 의미

```js
function exampleFunc(a, b, c, ...args) {
  console.log(a, b, c);
}
exampleFunc(1, 2, 3);
```

## 템플릿 리터럴 (Template Literal)

=> `` (베틱)
: 베틱 안에 ${}시 변수명이나 자바스크립트 문법 사용가능
const testValue = "안녕하세요!"
console.log(`Hello World ${3+3}`)

---

# 어려웠던 내용🥲

1. 자연스럽게 쓰면서 알고는 있었지만 용어들이 쉽지 않았다 ex) template Literal
   코드를 짤 때 내가 어떤 메서드를 사용하고 있는지 생각하면서 짜면 자연스럽게 외워지지 않을까?
2. 화살표함수는 this를 컴바인딩 하지 않는다!! (몰랐던 사실이었다..)
3. 함수의 리펙토링과 배열의 요소로 할당하는 부분이 아직 많이 헷갈린다!!
4. map()은 key와 value값 모두 저장하지만 Set()은 value값만 저장한다는 것!

# 한번 더 생각하자 🙏

>

## 코드컨벤션(이름짓는방법)

한사람이 쓴 것처럼!
규칙에 의존!

- 파이썬(snake_case)
- PascalCase(컴포넌트, page파일)
- 상수 (다 대문자)
- 길더라도 약속되지 않은 줄임말 x

# 🙏 오늘의 정리

점점 알게되는 메서드가 많아지면서 각각의 특징들이 조금씩 헷갈리는 것 같다..!
무작정 외우지 말고 코테 문제들을 풀고 다른 사람들 풀이도 보면서 익히는 것이 더 빠를 것 같다
많이 풀어보고 많이 사용해보자!! 그것만큼 빨리 익히는 방법은 없다! 그리고 포기하지 말 것.✨
