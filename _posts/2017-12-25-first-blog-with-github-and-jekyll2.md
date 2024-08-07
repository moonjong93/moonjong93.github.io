---
layout: post
title: "Jekyll로 시작하는 블로그 - 중간"
subscript: "블로그 입문기 두 번째 이야기"
tags: ["Jekyll", "Blog"]
categories: "개발"
comments: true
permalink: /develop/blog/:title
date: 2017/12/26
---

## 1. 웹 개발은 디자인 부터

어느정도 프로토타입은 정해두었다. 사실 처음과 지금의 결과물은 상당히 다르다 처음엔 노트형식의 디자인을 기획하게 되었다.

![이 블로그의 프로토타입](/assets/img/postsImg/jekyll-blog-with-github-prototype.png)

정말 자주 사용하는 시스템이 있는데 바로 [Evernote](https://www.evernote.com)이다 지금도 아이디어를 정리할때 사용하고 있는데 벌써 노트의 수가 70개에 육박한다 상당히 좋은 시스템이고 편리하기 때문에 내가 만약 블로그를 만들때 이렇게 보기 편하면 좋다고 생각햇다.

> 그러나 에버노트 형식의 블로그의 단점은 분명했다

일단은 검색 최적화가 힘들었다 노트를 클릭하면 내가 작성한 글들을 모아놓은 데이터를 보고 싶었는데 Jekyll의 시스템상 썸네일 그리고 짧은 글 요약 등을 저장하기가 상당히 귀찮기 때문에 노트 형식의 블로그는 포기하게 되었다.

## 2. 컬러를 정하자

예전엔 레이아웃부터 생각햇다면 지금은 컬러부터 정하게 되는것 같다, 메인이 되는 색상인 연분홍 느낌의 #fe9f9f 컬러부터 시작으로 색을 정하게 되었다, 대부분의 글들은 완전한 블랙보다는 #333 ~ 777을 오고가며 만들었다 내 기준에서는 그렇게 하는 부분이 눈이 편하다고 느꼇기 때문이다.

그렇게 만들어진 블로그의 색상표는 대략적으로

- 강조 - 이 블로그의 메인 색상 그리고 강조에 사용
  - 컬러표 : #fe9f9f
  - 사용처 : 아이덴티티
  - 느낌 : 소프트 핑크 (크흠)
- 본문 글자색 - 눈이 편한 색상을 사용
  - 컬러표 : #1b1f29
  - 사용처 : 본문
  - 느낌 : 그나마 눈이 편한 색 조금 빠진 검정
- H 태그 색상 - 눈이 편한 검정, 두께는 700정도
  - 컬러표 : #4a4a4a
  - 사용처 : H 태그
  - 느낌 : 눈이 조금 편한, 조금 색 빠진 검정

이런식으로 컬러표를 정해서 디자인에 나섰다

## 3. 레이아웃을 정하자

index.html 즉 메인이 되는 레이아웃을 먼저 짜야 했다, 레이아웃은 상당 부분 evernote의 영향을 많이 받았다, 기존에는 좌측에서 열리는 notes의 목록으로 선택해서 해당 포스트에 들어가는 정말 나의 노트를 훔처보는 느낌으로 디자인 하고 싶었다.

그러나 글씨의 미리보기나 위에서 내려오는 무엇을 사용하더래도 굳이 써야할 이유를 느끼지 못했다 왜냐면 글의 미리보기가 너무 많으면 검색결과에 노출이 안되기 때문에 그리고 썸네일등 힘든게 많기 때문에 목록에서 선택하는 부분을 조금 바꿔서 만들게 되었다.

> 그러나 글이 많아지면 아무런 의미가 없을것 같다

## 4. 처음 만나는 Ruby?

그러나 아예 Ruby언어를 모르는 나에게는 조금 어렵게 다가왔다 그러나 대부분의 문법은 ejs에서 사용해본 것들과 비슷했다 물론 Vue.js와도 말이다

지킬 공식 가이드북을 가면 자세히 나와있다 가령 - page.title 이라는 간단한 코드로도 타이틀을 가져올 수 있다 이미 내부적으로 그런 모든것들이 다 구현되어있기 때문인데 이런 점들이 지킬에 블로그를 올리는데 정말 많은 도움이 된다.

[깃허브](https://github.com/moonjong93/moonjong93.github.io) 이곳에 방문하면 모든 코드가 보관 중이니... 굳이 보고 싶으시다면 보시는것도 추천한다

---

다음 글은 이제 코드를 보면서 마지막으로 어떻게 만들었는지 알아보겠다.
