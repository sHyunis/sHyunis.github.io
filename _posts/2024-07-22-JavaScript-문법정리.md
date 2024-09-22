---
title: "JavaScript기본문법정리"
excerpt: "JavaScript"

categories:
  - Categories2
tags:
  - [tag1, tag2]

permalink: /categories2/JavaScript1/

toc: true
toc_sticky: true

date: 2024-07-22
last_modified_at: 2024-07-22
---

> # 🌟 기본 문법 정리
>
> : Data type, Operator(연산자), 함수(function), 조건문, 객체(Object), 배열(Array), 반복문, break, continue

# 👀 JavaScript란?

# 브라우저 동작 스크립트 언어

UX(User Experience)= 사용자 경험

JS 언어의 특징

1. 객체 지향 프로그래밍 지원
2. 객체 지향 프로그램(데이터와 함수를 객체라는 그룹으로 묶어서 처리)
   동적타이핑(런타임 시점에 변수에 할당되는 값에 따라 자동으로 데이터 타입이 결정)

3. 함수형 프로그래밍 지원
4. 비동기 처리(작업을 순차적으로 기다리지 않고 병렬로 처리할 수 있도록 하는 방식)
5. 클라이언트 측 및 서버 측 모두에서 사용 가능(Nods.js를 이용하여 서버 측에서도 사용, 이를 통해 웹 개발 전반에 걸쳐 자바스크립트를 화용가능)

---

## ☘️ ☘️ ☘️ ☘️ ☘️ ☘️ ☘️ ☘️ ☘️ ☘️ ☘️ ☘️ ☘️ ☘️ ☘️ ☘️ ☘️ ☘️ ☘️

![](https://velog.velcdn.com/images/alice0751/post/b86a9bef-f110-4e16-af97-b8548eac273d/image.png)

### ✨ 변수, 상수

변수 : 기억하고 싶은 값을 메모리에 저장 => 재사용

#### 변수의 개념

- 변수 이름 : 저장된 값의 고유 이름
- 변수 값 : 변수에 저장된 값
- 변수 할당 : 변수에 값을 저장하는 행위
- 변수 선언 : 변수를 사용하기 위해 컴퓨터에 알리는 행위
- 변수 참조 : 변수에 할당된 값을 읽어오는 것

#### 변수의 선언 방법

1. var
2. let
3. const

var는 재선언이 가능하지만 let과 const는 재선언이 불가하다.
var와 let은 재할당이 가능하지만 const는 재할당이 불가하다.

## ✨ Data type

Data type은 runtime에 결정된다.
runtime : 코드 작성할 때가 아닌 실제 코드가 실행될 때

(typeof 변수) Data type을 조회가능

[숫자]

- 정수
- 실수(float)
- 지수형(Exp)
- Nan(Not a number)
- Infinity, -Infinity (무한대)

[문자]
: string(문자열 = 문자의 나열)

- 문자열 길이확인(.length)
  console.log(str.length);
- 문자열 결합하기(.concat)
  let result = str1.concat(str2);
- 문자열 자르기(.substr), (.slice)
  console.log(str3.substr(7,5)); (7번째부터 5개)
  console.log(str3.slice(7, 12)); (7번째~12번째)
- 문자열 검색하기(.search)
  console.log(str4.search("World")); (몇번째에 문자열이 있는지 반환)
- 문자열 대체(.replace)
  let result01 = str5.replace("World", "Javascript");
  (World를 Javascript로 변환)
- 문자열 분할 (.split)
  let result02 = str6.split(",");

[Boolean]
true, false

[undefined]
: 정의되지 않은 것
un : not, define : 정의하다

[null]
: 개발자가 의도적으로 값이 존재하지 않음을 "명시적"으로 나타내는 방법

[object(객체)]

: key-value pair

let person = {
name: "SoHyun",
age: 20,  
}

[Array(배열)]
: 여러개의 데이터를 순서대로 저장하는 데이터 타입 (index를 가지고 있음)

---

## ✨ 형 변환

1. 암시적 형 변환

[문자]
{}, null, undefined + "1" => 문자열

```js
let result1 = 1 + "2";
console.log(result1);
console.log(typeof result1);

let result2 = "1" + true;
console.log(typeof result2);
```

[숫자]

```js
let result3 = 1 - "2";
console.log(result3);
console.log(typeof result3);

let result4 = "2" + "3";
console.log(typeof result4);
```

2. 명시적 형 변환
   [Boolean]

- false값 반환
  0, 빈문자열, null, undefined, NaN

```js
console.log(Boolean(0));
console.log(Boolean(""));
console.log(Boolean(null));
console.log(Boolean(undefined));
console.log(Boolean(NaN));
```

- true값 반환
  문자열,객체

```js
console.log(Boolean("false"));
console.log(Boolean({}));
```

[String(문자)]

```js
let result5 = String(123);
console.log(String(typeof result5));

let result6 = String(true);
console.log(String(typeof result6));

let result7 = String(false);
console.log(String(typeof result7));

let result8 = String(null);
console.log(String(typeof result8));

let result9 = String(undefined);
console.log(String(typeof result9));
```

[Number(숫자)]

```js
let result10 = Number("123");
console.log(result10);
console.log(typeof result10);
```

## ✨ 연산자

1. 더하기연산자(+)
2. 빼기 연산자(-)
3. 곱하기 연산자(\*)
4. 나누기 연산자(/)
5. 나머지 연산자(%)
6. 할당 연산자(assignment)

- 등호 연산자 (=)
- 더하기 등호 연산자(+=)
- 뺴기 등호 연산자(-=)
- 곱하기 등호 연산자

7. 비교 연산자
   : Boolean(true or false를 반환하는 연산자)

- 일치 연산자(===)
  : type까지 일치해야 true를 반환하는 연산자
- 불일치 연산자(!==)
  :type까지 일치해야 false를 반환하는 연산자
- 작다 연산자(<)
- 작거나같다 연산자(<=)

8. 논리 연산자

- 논리곱 연산자(&&)
  : 모두 true일때 true 반환
- 논리합 연산자(||)
  : 두 값 중 하나라도 true인 경우 true반환
- 논리부정 연산자(!)
  : 값을 반대로 바꿈
  (ex) (!true) => false
- 삼항 연산자(조건에 따라 값 반환)

```js
let x = 10;
let result = x > 5 ? "크다" : "작다";
console.log("------");
console.log(result);
```

- 타입 연산자(typeof)
  : 변수의 type을 반환

---

## ✨ 함수 선언문(function)

: input과 output

1. 함수 선언문
   function 함수명(매개변수){
   // 함수 내부에서 실행할 로직
   }
2. 함수 표현식
   let 함수명 = function(매개변수){
   //함수 내부에서 실행할 로직
   }

### 스코프

: 영향을 끼치는 범위

### 전역변수

: js전체에 영향을 주는 변수

### 지역변수

: 지역내에서만 영향을 주는 변수

## 화살표 함수

: ES6 신 문법

```js
function add(x, y) {
  return x + y;
}

// 1-1 기본적인 화살표 함수
let arrowFunction = (x, y) => {
  return x + y;
};

// 한 줄로(함수식이 줄이 한 줄일 때만 가능)
let arrowFunc02 = (x, y) => x + y;
```

## ✨ 조건문(if, else if, else, switch)

1. if 문

```js
if(/*true또는 false가 나올 수 있는 조건*/){
// 조건에 따라 수행할 식
}
```

2. else

```js
if (조건) {
  //main logic #1
} else {
  //main logic #2
}
```

3. if - else if - else

```js
if (조건1) {
  // main logic #1
} else if (조건2) {
  // main logic #2
} else {
  // main logic #3
}
```

4. switch
   : 변수의 값에 따라, 여러 개의 경우(case) 중 하나를 선택
   default
   (break필수)

```js
let fruit = "사과";

switch (fruit) {
  case "사과":
    console.log("사과입니다.");
    break;
  case "바나나":
    console.log("바나나입니다.");
    break;
  case "키위":
    console.log("키위입니다.");
    break;
  default:
    console.log("아무것도 아닙니다.");
    break;
}
```

## 중첩문

if(조건){
// main logic #1
if(조건){
// main logic #1
}else{}
}else{}

## 조건부 실행

: 앞의 조건이 만족하면 뒤를 실행

```js
// let x = 10;

// if(x>0){
// console.log("x는 양수입니다.")}

x > 0 && console.log("x는 양수입니다.");
```

## 삼항 연산자와 단축평가

 <!-- or 조건(||) -->

```js
let y; // y는 undefined
let z = y || 20;
```

해석: y가 undefined면 20일 넣어라

## falsy한 값, truthy한 값

: if문의 조건문 안에서 [0, "", null, undefined, NaN, false]실행 안됨(false라는 값으로 인식함)

```js
if (0) {
  // main logic
  console.log("hello");
}

if ("") {
  // main logic
  console.log("hello");
}
if (null) {
  // main logic
  console.log("hello");
}
if (undefined) {
  // main logic
  console.log("hello");
}
if (NaN) {
  // main logic
  console.log("hello");
}
if (false) {
  // main logic
  console.log("hello");
}
if (true) {
  // main logic
  console.log("hello");
}
```

---

# ✨ 객체

: 하나의 변수에 여러개의 값을 넣을 수 있다
key - value pair

## 객체 생성 방법

1. 기본적인 객체 생성 방법

```js
let person = {
    name : "홍길동",
    age : 30.
    gender : "남자",
}
```

2. 생성자 함수를 이용한 객체 생성 방법
   : this , new 변수명()

```js
function Person(name, age, gender) {
  this.name = name;
  this.age = age;
  this.gender = gender;
}

let person1 = new Person("홍길동", 30, "남자");
let person2 = new Person("홍길순", 20, "여자");
```

## 속성에 접근하는 방법

: 변수명.value

```js
console.log(person.name);
console.log(person.age);
console.log(person.gender);
```

## 객체 메소드(객체가 가진 여러가지 기능 : Object.~~~)

1. Object.key() : key를 가져오는 메소드
2. Object.values() : value를 가져오는 메소드
3. Object.entries() : entries를 가져오는 메소드
   => key와 value를 묶어서 배열로 만든 배열 (2차원 배열)
4. Object.assign(복사를 시킬 곳, 복사할 것) : 객체복사

- 복사1

```js
let newPerson = {};
Object.assign(newPerson, person);
console.log("newPerson=>", newPerson);
```

- 복사2(age를 변경하고 복사)

```js
let newPerson = {};
Object.assign(newPerson, person, { age: 31 });
console.log("newPerson=>", newPerson);
```

## 객체 비교

: 객체는 메모리에 저장할 때 별도의 공간에 저장
별도 공간에 대한 주소를 저장
객체 비교를 하면 변수와 달리 내용이 같아도 저장한 주소가 다르기 떄문에 false를 반환한다.

## 객체 병합(...)

spread Operator => ... 을 객체 앞에 붙임
{}를 풀어줌

```js
let person1 = {
  name: "홍길동",
  age: 30,
};
// person2 별도 공간에 대한 주소
let person2 = {
  gender: "남자",
};
console.log("----------");
let perfectMan = { ...person1, ...person2 };
console.log(perfectMan);
// 결과
// : {name : 홍길동, age : 30, gender : "남자"}
```

# ✨ 배열

1. 생성
   (ex)

```js
let fruits = ["사과", "바나나", "오렌지"];
```

- 크기 지정

```js
let number = new Array(5);
```

2. 요소 접근
   배열명 [[index번호]]
   (ex)

```js
console.log(fruits[0]);
```

3. 배열 메소드

- push
  : 배열명.push("안에 추가시킬 요소")
- pop
  배열의 마지막 요소가 삭제됨
  : 배열명.pop()
- shift
  배열의 첫번쨰 요소가 삭제됨
  : 배열명.shift()
- unshift
  배열의 맨 앞에 요소가 추가됨
  : 배열명.unshift("추가시킬 요소")
- splice
  : 배열명.splice(삭제하는 첫위치,삭제하는 마지막위치, 삭제하고 넣을 요소 )
- slice
  : 배열명.slice(배열을 잘라 시작할 위치, 해당 위치 앞까지 반환)
  ```js
  let fruits = ["사과", "바나나", "키위"];
  let slicedFruits = fruits.slice(1, 2);
  console.log(slicedFruits);
  // ['바나나;]
  ```

## forEach

: 배열의 반복문
콜백함수 : 매개변수자리에 함수를 넣는 것
=> 배열명.forEach(function(item){
실행문
})

```js
let numbers = [5, 2, 3, 8, 5];

// 콜백함수 : 매개변수자리에 함수를 넣는 것
numbers.forEach(function (item) {
  console.log("item입니다", +item);
});
// 출력값
// item입니다 5
// item입니다 2
// item입니다 3
// item입니다 8
// item입니다 5
```

## map

: 기존에 있었던 배열을 가공해서 새로운 배열을 생산
항상 원본 배열의 길이만큼이 return된다.(리턴이 없어도 undefined로 원본 배열의 길이만큼 출력)

=> 배열명.map(function(item){
return 변형시킬 방법;
})

(ex)

```js
let numbers = [5, 2, 3, 8, 5];
let newNumbers = numbers.map(function (item) {
  return item * 2; // return필수
});

console.log(newNumbers);
// 출력값
//[ 10, 4, 6, 16, 10 ]
```

## filter

: 배열의 값중 return의 조건에 맞는 값만 반환
=> 배열명.filter(function(item){
return item === 5;
})

```js
let filteredNumbers = numbers.filter(function (item) {
  return item === 5; // 조건
});

console.log(filteredNumbers);
```

## find

: return 조건에 맞는 첫번째 값만 반환
=> 배열명.find(function(item){
return (조건)
})

```js
let numbers = [5, 2, 3, 8, 5];
let result = numbers.find(function (item) {
  return item > 3;
});
console.log(result);
```

---

# ✨ 반복문

: 조건이 될 때까지 식을 반복

## for문

1. for 문 기본식
   => for(초기값;조건식;증감식){}

2. for ~ in문
   : 객체의 속성을 출력하는 문법
   => for(let key in 객체명){
   console.log()
   }

```js
let person = {
  name: "John",
  age: 30,
  gender: "male",
};

for (let key in person) {
  console.log(key + ":" + person[key]);
}
```

## while문

=> while(조건){
//메인로직
//증감
}

## do ~ while문

=> do{//메인로직; 증감;}while
(조건;)

## break

:break문을 만나면 for문을 탈출

```js
for (let i = 0; i < 10; i++) {
  if (i === 5) {
    break;
  }
  console.log(i);
} // 1,2,3,4,5
```

## continue

: continue를 만났을 때 다음 for문으로 넘어감

```js
for (let i = 0; i < 10; i++) {
  if (i === 5) {
    continue;
  }
  console.log(i); // 1,2,3,4,6,7,8,9
}
```

---

# 어려웠던 내용🥲

1. forEach, filter, map, find 의 사용법이 가끔 헷갈렸었는데
   오늘 한번 더 전체정리를 하며 내 것으로 만든 것 같다...!
2. 문자열 자르기 - slice(), substring(), splice() 가 비슷한 듯 조금씩 달라 헷갈렸는데 상황따라 직접 사용을 많이 해보며 익혀야 할 것 같다.
3. Object의 메소드 Object.key, Object.assign, Object.values, Object.entries 헷갈리지 않게 많이 써보기
4. 객체와 배열은 매일 조금 더 보며 익히기

# 🙏 오늘의 정리

처음 Javascript 문법을 1회독하였을때는 헷갈리는 것들도 많았고 이해가 잘 가지 않던 것들도 많았는데 몇회독씩 반복하다보니 이해도 가고 좀 더 잘 활용할 수 있을 것 같다는 확신이 든다...!
문법은 기초일 뿐이기에 응용하고 활용하는 방법을 익혀서 꼭 능력있는 개발자가 되고싶다...!
그날까지 화이팅💪💥

> ★ 항상 기술적고민을 많이 하고 생각할 것!

## 기술적 고민🤓

- 로직과 코드에 대한 의도를 생각할 것
- 구현하는 기술, 스텍의 목적과 근거 가지기
- 더 좋은 방법이 있는지 고민하기
- 객체지향을 잊지않을 것!
- 주석을 달면서 알고리즘 풀어보기
