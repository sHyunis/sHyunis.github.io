---
title: "JavaScript 객체,배열,비동기,동기"
excerpt: "JavaScript 객체,배열,비동기,동기"

categories:
  - Categories2
tags:
  - [tag1, tag2]

permalink: /categories2/JavaScript4/

toc: true
toc_sticky: true

date: 2024-07-29
last_modified_at: 2024-07-29
---

# 객체 배열 메서드, 얕은복사, DOM, 깊은복사, 비동기 동기

## 참조형타입

참조형타입은 값을 직접 가지지 않고 해당 값이 저장된 메모리 주소를 가리킴.

## 얕은복사, 깊은복사

1. 얕은복사(shallow Copy)
   : 얕은 복사는 배열의 참조를 복사하는 것으로 원본 배열과 복사된 배열이 동일한 객체를 참조한다. 따라서 한 배열을 수정하면 다른 배열에도 영향을 미침

```js
let original = ["Apple", "Banana", "Cherry"];
let shallowCopy = original;

shallowCopy[1] = "Blueberry";
console.log(original); // ['Apple', 'Blueberry', 'Cherry']
console.log(shallowCopy); // ['Apple', 'Blueberry', 'Cherry']
```

깊은복사(Deep Copy)
: 깊은 복사는 배열의 모든 요소를 새로운 배열에 복사하여 원본배열과 복사된 배열이 다른 객체를 참조하여 한 배열을 수정해도 다른 배열에 영향을 미치지 않음

- 재귀적 복제

```js
function deepCopy(o) {
  var result = {};
  if (typeof o === "object" && o !== null)
    for (i in o) result[i] = deepCopy(o[i]);
  else result = o;
  return result;
}

const obj1 = {
  a: 1,
  b: [1, 2, 3],
};

var obj2 = deepCopy(obj1);

console.log(obj1 === obj2);
console.log(obj1);
console.log(obj2);
```

- JSON.parse,JSON.stringfy복사
- 깊은 복사가 가능하나 getter/setter 등 JSON으로 변경 불가한 프로퍼티는 무시한다. 배열도 깊은 복사가 가능하지만 배열 관련 함수는 사용 불가능하다.

```js
let original = ["Apple", "Banana", "Cherry"];
let deepCopy = JSON.parse(JSON.stringify(original));

deepCopy[1] = "Blueberry";
console.log(original); // ['Apple', 'Banana', 'Cherry']
console.log(deepCopy); // ['Apple', 'Blueberry', 'Cherry']
```

## 배열 메서드

1. 변경 메서드
   : 배열 자체를 변경하는 메서드, 원본 배열을 수정한다.

- push() : 배열의 끝에 하나 이상의 요소를 추가, 배열의 새로운 길이를 반환
- pop() : 배열의 마지막 요소를 제거, 요소를 반환
- shift() : 배열의 첫 번쨰 요소를 제거, 요소를 반환
- unshift() : 배열의 앞에 하나 이상의 요소를 추가, 배열의 새로운 길이를 반환
- splice() : 배열의 기존 요소를 삭제 또는 교체 새 요소를 추가 배열의 내용을 변경함

```js
let fruits = ["Apple", "Banana", "Cherry"];
fruits.splice(1, 1, "Blueberry");
console.log(fruits); // ['Apple', 'Blueberry', 'Cherry']
```

- sort() : 배열의 요소를 정렬.
  ㅁ a - b 오름차순
  ㅁ b - a 내림차순

2. 비변경 메서드
   : 비변경 메서드는 배열을 변경하지 않고, 새로운 배열을 반환하거나 값을 반환하는 메서드

- concat() : 두 개 이상의 배열을 결합하여 새로운 배열을 반환

```js
let fruits = ["Apple", "Banana"];
let moreFruits = ["Cherry", "Date"];
let allFruits = fruits.concat(moreFruits);
console.log(allFruits); // ['Apple', 'Banana', 'Cherry', 'Date']
```

- slice() : 배열의 일부를 복사하여 새로운 배열을 반환
- join() : 배열의 모든 요소를 문자열로 결합
- includes() : 배열에 특정 요소가 포함되어 있는지 확인, 불리언 값을 반환
- indexof() : 배열에서 특정 요소를 찾고 그 요소의 첫 번쨰 인덱스를 반환
- map() : 배열의 각 요소에 대해 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환
- filter() : 배열의 각 요소에 대한 주어진 함수를 호출한 결과가 참인 요소만 모아 새로운 배열을 반환

## 객체 메서드(ObjectMethods)

: 객체 메서드는 객체의 속성에 접근하거나 객체를 조작함

- Object.keys() : 객체의 속성들을 배열로 반환
- Object.values() : 속성 값들을 배열로 반환
- Object.entries() : 속성[key, value]의 쌍을 배열로 반환
- Object.assign() : 하나 이상의 출처 객체로부터 대상 객체에 속성을 복사한다.

```js
let target = { name: "John" };
let source = { age: 30, city: "New York" };
let returnedTarget = Object.assign(target, source);
console.log(target); // { name: 'John', age: 30, city: 'New York' }
console.log(returnedTarget); // { name: 'John', age: 30, city: 'New York' }
```

- Object.freeze() : 객체를 동결 시켜 더 이상 수정할 수 없게 만듬
- Object.seal() : 객체를 밀봉하여 새로운 속성을 추가하거나 기존 속성을 삭제할 수 없음 속성값은 변경 가능

---

## DOM(Document Object Model)

: HTML 문서를 구조화 해놓은 객체

### DOM API

#### 1. 문서 탐색 및 선택

- document.getElementById(id)
  : 지정된 id속성을 가진 요소를 반환
- document.getElementsByClassName(className)
  : 지정된 클래스 이름을 가진 모든 요소를 반환
- document.getElementsByTagName(tagName)
  : 지정된 태그 이름을 가진 모든 요소를 HTMLCollection으로 반환
- document.querySelector(selector)
  : CSS선택자를 사용하여 일치하는 첫번쨰 요소를 반환
- document.querySelectorAll(selector)
  : CSS선택자를 사용하여 일치하는 모든 요소를 NodeList로 변환

#### 2. 요소 생성 및 조작

- document.createElement(tagName)
  : 지정된 태그 이름의 새로운 요소를 생성
- element.appendChild(child)
  : 지정된 자식을 요소의 끝에 추가
- element.insertBefore(newNode, referenceNode)
  : 새로운 노드를 지정된 참조 노드 앞에 삽임

```js
const parent = document.getElementById("parent");
const newNode = document.createElement("div");
const referenceNode = document.getElementById("child");
parent.insertBefore(newNode, referenceNode);
```

- element.removeChild(child)
  : 지정된 자식 노드를 제거
- element.replaceChild(newChild, oldChild)
  : 지정된 자식 노드를 다른 노드로 교체

```js
const parent = document.getElementById("parent");
const newChild = document.createElement("div");
const oldChild = document.getElementById("child");
parent.replaceChild(newChild, oldChild);
```

#### 3. 속성 조작

- element.setAttribute(name,value)
  : 요소에 지정된 속성을 추가하거나 변경함

```js
const element = document.getElementById("myElement");
element.setAttribute("class", "newClass");
```

- element.getAttribute(name)
  : 요소에서 지정된 속성 값을 반환
- element.removeAttribute(name)
  : 요소에서 지정된 속성을 제거

#### 4. 스타일 조작

- element.style.propertyName = value
  : 요소의 인라인 스타일 속성을 설정
- eleement.classList
  : 요소의 클래스 리스트에 대한 접근을 제공

#### 5. 이벤트 처리

- element.addEventListener(type, listener)
  : 요소에 이벤트 리스너를 추가
- element.removeEventListener(type, listener)
  : 요소에서 이벤트 리스너를 제거

---

## 동기, 비동기

1. 동기 (Synchronous : 동시에 일어나는)
   : 요청과 결과가 요청을 한 자리에서 결과가 반환됨
2. 비동기 (Asynchoronous : 동시에 일어나지 않는)
   : 요청과 결과가 동시에 일어나지 않고 요청이 대기하는 동안 다른 요청에 대해 처리 가능한 방식이다. 여러 개의 요청을 동시에 처리 가능

## Promise, async/await

### 1. promise

: 약속을 의미하고 Javascript에서 비동기 작업의 완료 또는 실패를 나타내는 객체

- 세가지 상태
  ㅁ 대기 중 (Pending) : 아직 결과를 받지 못한 상태
  ㅁ 이행됨 (Fulfilled) : 작업이 성공적으로 완료된 상태
  ㅁ 거부됨(Rejected) : 작업이 실패한 상태

1. 프로미스 생성
   new Promise를 통해 생성, 생성자 함수는 두 가지 콜백 함수를 받음
   resolve(성공) reject(실패)

```js
const promise = new Promise((resolve, reject) => {
  const success = true; // 작업 성공 여부를 나타내는 예시 변수

  if (success) {
    resolve("작업 완료");
  } else {
    reject("작업 실패");
  }
});
```

2. 프로미스 사용
   then과 catch 메서드를 사용하여 결과를 처리한다.

```js
promise
	.then(result =>{
  console.log("result")
  	.catch(error =>{
    console.error(error);
  })
```

3. 프로미스 체이닝
   : 여러 비동기 작업을 순차적으로 실행할 때 프로미스 체이닝을 사용하게 만들 수 있다. 각 then 메서드는 새로운 프로미스를 반환하여 체이닝을 만들어준다.

```js
const fetchData = new Promise((resolve, reject) => {
  setTimeout(() => resolve("데이터 가져오기 완료"), 1000);
});

fetchData
  .then((result) => {
    console.log(result);
    return new Promise((resolve, reject) => {
      setTimeout(() => resolve("두 번째 작업 완료"), 1000);
    });
  })
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.error(error);
  });
```

## async/await

async 를 이용하여 비동기 함수로 만들고 await 키워드를 사용하여 프로미스가 해결될 때 까지 기다림.
가독성이 높아지는 것이 장점

### async

: 프로미스를 항상 반환한다.

```js
async function myAsyncFunction(){
  return "1차 작업";

  myAsyncFunction().then(result => {
    console.log(result);
```

### await

: await은 프로미스가 해결될 때 까지 비동기 함수를 실행 중단한다.
async안에서만 사용가능

```js
async function fetchData() {
  const response = await fetch("url주소");
  const data = await response.json();
  console.log(data);
}

fetchData();
```

### 에러 핸들링

try catch문 사용

```js
async function fetchData() {
  try {
    const response = await fetch("~");
    if (!response.ok) {
      throw new Error("네트워크 응답이 올바르지 않습니다.");
    }
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("에러 발생:", error);
  }
}

fetchData();
```

#### 비동기 작업 한번에 처리하기

: 비동기 작업을 동시에 처리하고 기다릴 때는 Promise.all 사용가능

```js
async function fetchMultipleData() {
  try {
    const [data1, data2] = await Promise.all([
      fetch("~").then((res) => res.json()),
      fetch("~").then((res) => res.json()),
    ]);
    console.log(data1, data2);
  } catch (error) {
    console.error("에러 발생:", error);
  }
}

fetchMultipleData();
```

---

## URL

1. 프로토콜 : 자원에 접근하기 위해 사용됨

- https,http https가 보안이 강화된 것

2. 도메인이름: 자원이 위치한 서버의 이름 사람이 읽는 주소 기계에는 IP주소를 뜻함
3. 경로(Path): 서버 내에서 리소스의 위치
4. 쿼리 문자열(Query String):접근하는데 필요한 추가 매개변수를 전달

### URL 예시

```
https://example.com/path/to/resource?query=string
```

- **프로토콜**: `https`
- **도메인 이름**: `example.com`
- **경로**: `/path/to/resource`
- **쿼리 문자열**: `?query=string`

---

## fetch

fetch함수 예시

```js
fetch(url)
.then(response => response.json())
.then(data =< console.log(data))
.catch((error) => console.error(error));
```

- `fetch(url)`: 지정된 URL로 네트워크 요청을 보낸다.
- `.then(response => response.json())`: 응답을 JSON 형식으로 파싱
- `.then(data => console.log(data))`: 파싱된 데이터를 처리
- `.catch(error => console.error("Error:", error))`: 요청 중 발생한 에러를 처리

### fetch의 옵션

: fetch 함수는 두 번째 인수로 옵션 객체를 받을 수 있다. 이를 통해 HTTP 메서드, 헤더, 바디 등을 설정할 수 있다.

```js
fetch("~", {
  method: "POST", // HTTP 메서드
  headers: {
    "Content-Type": "application/json", // 요청 헤더
  },
  body: JSON.stringify({
    title: "새 작업",
    completed: false,
  }), // 요청 본문
})
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));
```

- `method`: HTTP 메서드를 설정 (예: GET, POST, PUT, DELETE)
- `headers`: 요청 헤더를 설정 (예: Content-Type)
- `body`: 요청 본문을 설정 주로 POST나 PUT 요청에서 사용
