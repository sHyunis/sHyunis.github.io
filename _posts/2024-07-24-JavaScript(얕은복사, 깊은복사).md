---
title: "JavaScript(얕은복사, 깊은복사, 실행컨텍스트)"
excerpt: "JavaScript, 얕은복사, 깊은복사, 실행컨텍스트"

categories:
  - Categories2
tags:
  - [tag1, tag2]

permalink: /categories2/JavaScript3/

toc: true
toc_sticky: true

date: 2024-07-24
last_modified_at: 2024-07-24
---

> ## 🌟 값의 Type , 얕은복사, 깊은 복사, 실행컨테스트

---

## ⭐️ 자바스크림트 값의 Type

- 기본형(Primitive Type)
- 참조형
  : 값의 저장방식, 불변성 여부에 따라 나뉨

1. 복제의 방식
   a. 기본형 : 값이 담긴 주소값을 바로 복제
   b. 참조형 : 값이 담긴 주소값들로 이루어진 묶음을 가리키는 주소값을 복제
2. 불변성의 여부
   a. 기본형 : 불변성을 띔
   b. 참조형 : 불변성을 띄지 않음

메모리구성 단위

- bit(0,1)
  : 가장 작은 단위
- byte
  : 모든 데이터는 byte 단위의 식별자인 메모리 주소값을 통해서 메모리에 저장

식별자, 변수
var testValue = 3
변수 = 데이터
식별자 = 변수명

---

# ⭐️ 변수 선언과 데이터 할당

## 값을 바로 변수에 대입하지 않는 이유

1. 자유로운 데이터 변환
2. 메모리를 효율적으로 관리하기 위해서

## 변수와 상수를 구분하는 방법

- 변수 : 변수영역에 메모리를 변경할 수 있음
- 상수 : 변수영역에 메모리를 변경할 수 있음

## 불변하다와 불변하지 않다

- 불변하다 : 데이터 영역 메모리를 변경할 수 없음
- 불변하지 않다 : 데이터 영역 메모리를 변경할 수 있음

(쓸모없어진 데이터들은 js의 가비지 컬렉터가 정리해서 메모리를 관리함)

# 참조카운트

> 객체를 참조하는 변수나 다른 객체의 수

# 참조형 가변성 주의점

객체를 만들면 변수, 데이터, 객체데이터공간이 만들어진다.
데이터의 주소값들을 저장하는 것이기 때문에
객체를 복사하여 데이터의 정보를 바꾸면 데이터가 바뀐다.
따라서 처음 만든 객체의 데이터도 변경이 된다.

```js
// user 객체를 생성
var user = {
  name: "wonjang",
  gender: "male",
};

// 이름을 변경하는 함수, 'changeName'을 정의
// 입력값 : 변경대상 user 객체, 변경하고자 하는 이름
// 출력값 : 새로운 user 객체
// 특징 : 객체의 프로퍼티(속성)에 접근해서 이름을 변경 => 가변

var changeName = function (user, newName) {
  var newUser = user;
  newUser.name = newName;
  return newUser;
};
// 변경한 user정보를 user2 변수에 할당
// 가변이기 때문에 user1도 영향을 받음
var user2 = changeName(user, "twojang");
//결국 아래 로직은 skip하게 됨
if (user !== user2) {
  console.log("유저 정보가 변경되었습니다.");
}

console.log(user.name, user2.name);
console.log(user === user2);
```

## ⭐️ 얕은 복사 (for ~in , copyObject)

얕은 복사 : 바로 아래 단계의 값만 복사(객체안의 객체 여전히 주소복사해옴)
문제점 : 중첩된 객체의 경우 참조형 데이터가 저장된 프로퍼티를 복사할 때, 주소값만 복사

### for ~in 구문을 이용

:객체의 모든 프로퍼티에 접근 가능

<복사>

```js
var copyObject = function (target) {
  var result = {};
  for (var prop in target) {
    result[prop] = target[prop];
  }
  return result;
};
```

얕은 복사 예제

```js
 var user = {
    name : "wonjang"
    gender : "male"
  }
  var user2 = copyObject(user)
  user2.name = "twojang"

  if(user !== user){
    console.log('유저 정보가 변경되었습니다.')
  }
  console.log(user.name,user2.name)
```

## ⭐️ 깊은 복사

: 내부의 모든 값들을 하나하나 다 찾아서 복사하는 방법

// 2차 카피까지 (어디까지나 임시방편)

```js
var user2 = copyObject(user);

//2차 copy(임시방편)

user2.urls = copyObject(user.urls);
```

=> 재귀적으로 수행해줘야 한다.

### 재귀적 수행 (recursive)

> 함수나 알고리즘이 자기 자신을 호출하여 반복적으로 실행되는 것
> 가장 깊은 곳까지 다 수행하고 나옴

### 완벽한 깊은 복사

: 모든 요소 하나하나를 다 불변성을 유지하도록 바꿔주는 것

```js
var copyObjectDeep = function (target) {
  var result = {};
  if (typeof target === "object" && target !== null) {
    for (var prop in target) {
      result[prop] = copyObjectDeep(target[prop]);
    }
  } else {
    result = target;
  }
  return result;
};
```

# undefined과 null

1. undefined : 값이 있어야할 것 같은데 없는 경우

   - 변수에 값이 지정되지 않은 경우, 데이터 영역의 메모리 주소를 지정하지 않은 식별자에 접근할 떄
   - .이나 [] 로 접근하려 할 때, 해당 데이터가 존재하지 않는 경우
   - return문이 없거나 호출되지 않은 함수의 실행결과

2. null : 개발자가 의도적으로 지정해준 경우
   - typeof null이 object로 나오는 것은 javascript 자체 버그!

## 동등연산자(equality operator), 일치연산자(identity operator)

동등연산자는 type까지 일치하지 않아도 true를 반환하는 반면 일치연산자는 type까지 확인한다.

---

# ⭐️ 실행컨텍스트

: 실행할 코드에 제공할 환경 정보들을 모아놓은 객체

1. 선언된 변수를 위로 끌어올림 = 호이스팅
2. 외부 환경 정보를 구성
3. this를 설정

## 실행컨텍스트 구성 순서(콜스택)

코드실행 - 전역(in)-전역(중단)-outer(in)-outer(중단)-inner(in)-inner(out)-outer(재개)-outer(out)+전역(재개)-전역(out)-코드종료

### 콜 스택

: 컴퓨터 프로그램에서 현재 실행 중인 서브루틴에 관한 정보를 저장하는 스택 자료구조

---

## 어려웠던 내용🥲 & 한번 더 생각하자 🙏

1. 객체의 가변성 때문에 이루어지는 얕은 복사와 깊은 복사에 대해서 알게 되었다. 개념은 이해가 되었는데 실제로 for~in문을 사용하고 활용할 때 어려움을 많이 겪게 될 것 같다...!
2. 메모리할당에 대해서 알게 되었다. 변수와 데이터 객체를 저장하는 곳 이렇게 주소값이 따로 생기는 것을 알게되었고 객체는 데이터 값을 같이 공유할 수 있기 때문에 내가 의도했던 바와 다르게 객체가 변경될 수 있다는 것을 항상 조심해야 할 것 같다

## 🙏 오늘의 정리

이번주는 혼자서 프로젝트를 만들어보고 있다.
혼자서 하다보니 신경쓸 것도 더 많고 가끔 막힐 때도 있지만 어려움을 겪을 수록 실력은 늘고있지 않을까....? 오늘도 열심히!!!✨
