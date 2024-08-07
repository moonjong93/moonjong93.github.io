---
layout: post
title: "자바스크립트의 재귀함수 어떻게 이해하면 좋을까?"
subscript: "예제를 통해 이해해보기"
tags: ["Javascript", "Recursion"]
categories: "개발"
comments: true
permalink: /study/:title
date: 2018/08/24
---

## 재귀함수 (Recursion function)

재귀함수는 말 그대로 함수 내에서 자기 자신을 다시 또 호출하면서 로직을 수행하는 함수를 말한다. 재귀함수를 응용하는데 있어서 많은 글들을 읽어봤지만 사실 그렇게 크게 와닿는 글은 없었던것 같다.

## 예제 보기

[MSDN](<https://msdn.microsoft.com/ko-kr/library/wwbyhkx4(v=vs.94).aspx>)의 예제를 살펴보자

팩토리얼에 재귀함수를 활용하는 예제인데

```javascript
function factorial(num) {
  // If the number is less than 0, reject it.
  if (num < 0) {
    return -1;
  }
  // If the number is 0, its factorial is 1.
  else if (num == 0) {
    return 1;
  }
  var tmp = num;
  while (num-- > 2) {
    tmp *= num;
  }
  return tmp;
}

var result = factorial(8);
document.write(result);

// Output: 40320
```

위와같은 팩토리얼 함수를 재귀함수로 아래와같이 만들수 있다는 내용이다.

```javascript
function factorial(num) {
  // If the number is less than 0, reject it.
  if (num < 0) {
    return -1;
  }
  // If the number is 0, its factorial is 1.
  else if (num == 0) {
    return 1;
  }
  // Otherwise, call this recursive procedure again.
  else {
    return num * factorial(num - 1);
  }
}

var result = factorial(8);
document.write(result);

// Output: 40320
```

## 간단한 예제 그러나 사용처는?

본인도 그랬다 물론 이해는 되지만 '재귀함수'를 사용하면서 얻는 이점이 무엇이 있는지 사실 이해가 잘 가지 않았다.

왜냐면 후자의 예제 역시 동작이 되며 모두다 같은 결과 값을 가져다 주기 때문이다.

그러던 도중 타인에게 문제를 받아 해결하는 과정에서 재귀함수를 사용해 꽤 간단하게 문제를 풀어냈기에 이 예제를 본다면 다른 사람도 어느정도 도움이 될것 같아서 작성하게 되었다.

## 다차원 배열을 1차원 배열로 만드는 예제

다차원 배열이란 배열이 한개의 차원이 아닌 여러개의 차원이 되는 그런 배열을 뜻한다. 다차원 배열이 된 이상 배열의 크기는 그렇게 중요하지 않고 어느 부분이라도 확장될수 있다.

1차원 배열이란 [0,1,2,3,4,5]와 같은 배열을 말하며
2차원 배열은 [ [1,2,3], [4,5,6] ]과 같은 배열을 말한다.

그러나 다 차원 배열은 저것을 넘어선 어느 부분에서건 증가가 가능해지는데 아래와 같은 배열도 다차원 배열에 속한다

[ 0, [1,2, [3,2,3,1], [0,1,2,3,] ],2,3,4 [1,2,3, [4, [6] ] ] ] 과 같이 보기도 힘든 배열...도 역시 다차원 배열에 속한다.

그러나 이런 배열들을 1차원 배열로 바꾸기 위해서는 어떻게 해야할까?

말 그대로 위의 배열을 [ 0, 1, 2, 3, 3, 1 ...]와 같이 말이다.

## 일반적인 For문을 이용해서 푼다면?

그러니까 나쁜 방법부터 생각해보자 일반적인 for문을 이용한다면 어떻게 풀 수 있을까?

```javascript
function Solution(target){

    var result = []

    // 만약 배열이 아니라면 이 함수를 종료
    if(!Array.isArray(target))
        return null

    // 타갯의 길이 만큼 반복
    for(var i = 0; i < target.legnth; i ++){
        // 타갯의 i가 배열인지 확인
        if( !Array.isArray(  target[i] ) ){
            // 배열이 아니라면 1차원 배열에 삽입
            result.push(target[i])
        }else{
            for(var j = 0; j < target[i].length; j ++){
                if( !Array.isArray(  target[i][j] ) ){
                    result.push(target[i][j])
                }
            }else{
                .
                .
                .
            }
        }
    }
}
```

와 같이 depth에 관한 정보를 모른다면 어디까지 코딩해야하는지 알 수 없다. 즉 거의 불가능에 가깝다.

그렇다면 어떻게 하면 효율적으로 해결할 수 있을까?

```javascript
function Solution(target) {
  // 결과를 담을 변수
  var result = [];

  for (var i = 0; i < target.length; i++) {
    // 어레이가 아니라면 push해주고
    if (!Array.isArray(target[i])) result.push(target[i]);
    else {
      result = result.concat(Solution(target[i]));
    }
  }

  return result;
}
```

위 처럼 해결할 수 있다.
