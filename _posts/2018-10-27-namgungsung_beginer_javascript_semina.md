---
layout: post
title: "남궁성 자바스크립트 기초 세미나 정리"
subscript: "세미나에 참가하다"
tags: ["Javascript", "beginer"]
categories: ["개발"]
comments: true
permalink: /study/:title
date: 2018/10/27
---

## 남궁성 자바스크립트에 참가하다.

예전에 '난 정말 자바를 공부한적이 없다구요'라는 책을 보고 남궁성 자바라는 카페를 가입했었는데 어쩌다보니 자바는 전혀 하지 않고 Jvacsript만 주로 하게되었는데 운 좋게 남궁성님이 운영하는 세미나가 있어서 참가하게 되었다.

물론 처음엔 늦게 신청해서 아쉽게도 참가권에서 밀려났지만 운이 좋게도 한자리 비어서 진행하게되었다.

이 글은 내가 이 세미나를 들으며 정리하며 내용을 담기로 했다.

## 목차

1. Javascript 역사
1. 개발도구의 종류와 장단점 - VS code, Webstorm, Atom 등
1. 변수의 타입과 선언
1. 입력과 출력
1. 연산자 - new, typeof, instanceof
1. 조건문과 반복문 - for each, for in
1. 배열
1. 내장객체 형변환함수, ""와 new String("")의 차이
1. 함수
   - 함수 기본
   - 매개변수
   - 변수의 스코프
   - 클로져
1. DOM과 이벤트 처리
1. 객체와 생성자
   - 생성자와 this
   - prototype
   - constructor
   - js에서의 다형성
   - 상속

## Javascript의 역사

- 1995년에 Eredan Eich가 발명, ECMA가 1997년에 표준화 했음

HTML이 원래는 하이퍼링크만 주어진 단순한 문서였는데 이를 동적으로 변화하기 위해서 Javascript로 만들어졌음

원래 개발당시에는 OOP를 고려하지 않았지만 현재는 상당히 많은 부분에서 사용중이고 현재는 이를 넘어서 함수형 언어가 되었음.

현재는 Javascirpt가 안쓰이는 곳이 없다. 보안, 출판, Indesign은 Javascript로 책을 자동화로 만들게끔 도와준다.

실무에선 Jquery를 많이 쓰이는데 탈피해서 자바스크립트 본연으로 돌아가서 JS를 사용하는 경우가 많아지고 있음

오늘 세미나에서는 JAVA와 js의 차이점에서 대해서 많이 둘거고 실습을 위주로 진행함

ECMA5와 ECMA6의 차이는 OOP를 추가했다는 점이며 오늘은 ECMA5위주로 진행을 함

Javascript에서 window 의미하는것은 브라우저를 뜻함

## 개발도구의 종류와 장단점

## 변수의 타입과 선언

### hoisting

- 변수나 함수 선언이 스코프에서 최상단으로 옮겨가는 것

```javascript
num = 5;
var num2 = 1;
console.log(num2);
var num;
console.log(num);

//여기서 num의 선언을 최상단으로 자동으로 올려줌
```

권장하지 않는 프로그래밍임

### Scope

- 함수 내부가 아니면 전부 전역 (var)
- 전역 선언에 경우 브라우저에 변수가 저장된다.
- 지역 변수는 함수 내부에 선언된 선언이 지역변수로 저장된다.
- 변수 선언을 함수든 어디서든 안하면 전역으로 선언됨

```javascript
function sum(a, b) {
  var result = 0;
  gResult = 0;

  for (var i = 0; i < arguments.length; i++) {
    gResult += arguments[i];
    console.log(i);
  }
  //var i는 호이스팅에 의해서 최상단으로 올라가게됨
}

console.log(gResult); //undefined
sum(10, 50);
// 0
// 1
console.log(gResult); // 60;
```

```javascript
// false인지 ture인지 확인하려면 그냥 타입에 !!해보면됨
console.log(!!undefined);
// false
```

## 연산자

- '==' '==='의 차이 ==는 값비교 ===는 타입까지 비교

```javascript
var num = new Number(0);
var num1 = 0;
console.log(num === num1);
// false
// 타입이 다르다 new Number는 객체이기 때문
```

- 결론 ==는 쓰지마라

```javascript
var num = new Number(0);
var num1 = 0;
console.log(num == num1);
// true
```

여기에서 num을 자동으로 형변환을 시키기 때문에 좋지 않다.

## 조건문과 반복문

## 배열

```javascript
var arr = [1, 2, 3, 4, 5];
arr[6] = 100;

console.log(arr);
//1,2,3,4,5, ,100

for (var i in arr) console.log(arr[i]);
// empty, undefined는 건너뜀 in의 특징임
```

```javascript
var arr = [1, 10, 20, 11, 12, 30];
arr.sort(); // 는 사전 정렬이라서 제대로 되지않음
// 그래서 이렇게함
arr.sort((a, b) => a - b);
```

## DOM

- DOM은 기본적으로 노드로 생성된다.

## 난 정말 자바를 공부한적이 없다구요

찾아보니 남궁성님이 안쓰셨다. 잘못알고 왔다. 망했다.

## 후기

이 글을 읽은 사람이라면 누구나 왜 목차랑 인마 달라 이자식아 라는 생각을 하실 수 있다 그렇다 목차와 다르게 세미나가 진행됐다.

그리고 시간이 모자라서 DOM의 이벤트는 하지 않고 지나갔다.

> 괜히 갔나 후회 했다

솔직히 말하면 시간을 버렸고 돈을 버렸다고 생각했다. 기존에 전부 알던 내용이고 복습을 할거면 MSDN을 볼것이고 그것마저도 아니라면 많은 자바스크립트 교재를 한번 훑어보는게 좋다고 생각한다.

물론 초보자 입장에선 이 강좌가 어떻게 다가올진 모르겠다. 좋다고 생각하는 사람도 있을것이고 그럴것 같다

그러나 현재 프론트엔드나 자바스크립트 개발을 보자면 es5 기준으로 프로그래밍을 하는 경우는 전혀 없다고 확신한다.

타입스크립트, ES6(바밸을 통한)면 모를까 상당히 안타까운 시간이었고 설명 자체도 본인이 가져오신 교재를 통해 읽는 것만 반복되는 느낌이었다.

자바를 알고 있는 사람을 전제하에 세미나가 진행된다고 하셨는데 어느정도 자바를 아는 사람이라면 굳이 세미나를 참가하지 않고 변수 선언 등...을 살펴보기는게 좋지 않을까?

완전 초보자가 듣기에는 너무 급하게 지나가서 내 옆자리 분은 실제로 제대로 이해하지 못하고 지나갔고 조금 경험이 있는 개발자는 시간이 아깝다고 느끼며 지나갔다.

이도저도 아닌 세미나였어서 더 이상 쓸 말이 없다.

책을 사시는것을 추천한다.
