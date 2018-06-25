---
layout: post
title: "일본에서 체크인 기능을 담은 웹을 개발했다"
subscript: "Vue.js와 함께하는 PWA 웹 개발"
tags: ['Node.js','functions','firebase','vue.js']
categories: "커리어"
comments: false
permalink: /career/:title
date: 2018/01/22
---
## 일본은 왜?
문득 그냥 가고 싶었다 그래서 정말 이유 없이 왔다.

그렇게 온 일본에서 처음으로 맡은 프로젝트 체크인 기능을 4개 국어로 만들어 달라.

일본어, 중국어, 영어, 한국어까지
![완성사진](/assets/img/postsImg/language-fplus.png)

## 필요 했던 부분
- 메일 서버
- https 호스팅
    - firebase는 갓갓 호스팅
- 이미지 서버
- 관리하기 쉬운 서버...

그니까 서버는 운용되는데 서버르 관리하기 꺼려한다고 전달 받았을때 바로 서버리스가 생각났다. 거기다가 firebase의 실시간 데이터베이스까지 사용한다면 걱정할게 없었다.

## 메일
[메일건](https://www.mailgun.com/)을 이용해 메일을 발송하고 있다 처음 테스트 당시에는 google 계정으로 보냈었는데 생각보다 속도도 느리고 거디가다 찾아보니 발송 제한까지 있기에 따로 메일서버를 사용했다.

가격은 상당히 저렴하며 월 10,000건 까지는 무료이기에 테스트에는 이정도의 조건은 없는것 같다.

거기다가 딱히 어렵지 않게 적용할 수 있었고 STMP를 사용해 메일을 발송하면 끝 이었다. 

메일을 발송하는 부분은 [Nodemailer](https://nodemailer.com/about/)를 사용했다.

그러나 메일 발송에서 별도의 서버를 운용하는게 꺼려진다고 하기에 firebase의 functions를 활용해 REST 형식의 웹으로 개발을하게 되었다.

## https 적용은?
사실 나는 Nginx나 Apache서버를 사용해본 경험은 있지만 ssl을 적용하거나 했던일은 아예 없었다.

그래서 위와 같은 개발환경에선 ssl을 적용하는게 얼마나 어려울지는 모르겠지만 REST 형식의 프론트엔드만 호스팅하면되기 때문에 상당히 간단했다. 

firebase의 정적웹 호스팅을 이용했는데 그냥 배포만 하면 자동으로 ssl을 적용해서 만들어줬기 때문에 따로 신경쓸 부분은 크게 없었다.

## 언어는?
언어는 JSON 형식으로 개발해 router로 나누어서 concat해서 각 언어에 맞게 불러오게 설계했다.

제일 기본은 당연히 영어로 개발하고 해당 영어를 다른 국적의 직원들이 번역해줘서 상당히 빠르게 끝날 수 있었다.

다음에 내가 다국적 서비스를 할 기회가 생긴다면 다시 한번 적용해볼만 한것 같다.

## 그 외에
이미지 서버나 그외 부분 역시 firebase를 활용해 해결했다. 클라이언트가 특히 디자인에 많이 신경써달라고 했기 때문에 내가할 수 있는 최소한의 시간을 서버로 사용하고

나머지는 프론트엔드 개발에 사용하게 되었다. 가령 사진을 촬영시 현재 보여지는 이미지가 다르게 나와야 한다거나 하는 자잘한 요구사항이 있었기에 생각보다 시간이 꽤 걸리는 작업이었다.

## 마치며.
클라이언트가 자신이 무엇을 만들고 싶어하는지 모르는건 정말 개발자로 하여금 힘들게 한다, 자신이 무엇을 원하는지도 무엇을 만들어야 하는지도 모르는데... 더군다나 모자란 일본어로 소통하느냐고 나름 애를 먹었다.

그러나 모자란 일본어로도 이 프로젝트를 정말 잘 끝냈기에 나름 자신감도 생기고 괜찮은 클라리언트(자신이 무엇을 만들고 싶어하는지도 모르지만 사람이 괜찮았다)를 만나 다행이었다.






