---
layout: post
title: "Tac.photos를 개발이야기 - 배운게 많다"
subscript: "SPA와 serverless-http 그리고 s3"
tags: ['Node.js','S3','Lambda','vue.js']
categories: "커리어"
comments: false
permalink: /career/:title
date: 2018/04/23
---
## 시작하기 앞서
올해에 들어 SPA를 접하고 여러가지 개발을 하면서 꼭 개인프로젝트 하나를 해야겠다는 생각을 했다. 시작은 정말 거대 했다.

애초에 계획은
- 로그인 
    - Token을 활용
- Serverless
    - 모든 부분에 Serverless 적용
    - S3에 업로드 하며 당연히 썸네일도 필요할것이라 예측
- 태그 검색
- 비밀 이미지
- 등등..

등 상당히 많은 계획과 방대한 양의 기획이 있었다. 실제로 로그인도 구현했으며 이메일 인증은 AWS의 SES를 통한 메읿 발송과 Nodemailer를 활용해 나름 멋스럽게 Table단위의 폼도 적용해서 보내기 까지 만들었다..

그러나 결과적으로 모든걸 다 없애고 그냥 이미지 업로드만 냅두고 출시하게 되었다는 것이다... 상당히 애통하지만 몇가지 큰 이유들이 있었다.

### 누가 쓰겠어?
처음 계획은 이미지를 누구나 쉽게 공유하고 업로드 이후에 간단한 링크를 만들어 [imguar](https://imguar.com)과 같은 사이트 이지만 약간 한국의 느낌과 맞추고 싶었고 실제로 그게 정말 잘 될것 같다고 생각했다.

그러나 몇가지 문제에 부딪혔다.

1. 비용
2. 디자인
3. 홍보
4. 쓰고자 하는 동기

이 어느것도 충족할 수 없었다. 비용에 따른 문제를 고민하면서 서버도 고민하고 거기다가 가끔 뿜어져나오는 Serverless-http 와 그외 데이터베이스 등 많은 연동에서의 오류는 어느순간 나에게 이 프로젝트를 포기하라고 소리쳤다.

## 무엇을 개발도중에 없앴나?

![없애버린 것들 중 하나](http://i.tac.photos/p/rJmAmJj3M.png)
그렇게 없애버린것에는 많은 것이 있었다. 대표적으로 로그인이 그렇다 소셜로그인은 Hello.js를 통해 서버에는 오로지 유저의 Email과 어떤 종류의 소셜로 로그인 했는지만 반영해서 혹시 가입되어 있지 않는 유저라면 닉네임 설정으로 넘어가게 되었고

이메일 회원가입은 가입 요청과 동시에 AWS SES를 통해 이메일을 발송해서 허락이 나야만 로그인 할 수 있었다.

그 외에도 이미지 태깅 검색부터 상당히 많이 부분을 아니 사실 다 날렸다고 보면된다..

> 빠르게 버리는것도 도움이 된다고 생각한다.

## 그래서 무엇을 했나?
하지만 이 프로젝트를 중간에 포기했더래도(물론 그러지 않았지만) 상당히 배운게 많았다 우선 SPA앱이 가지는 한계와 이것을 극복하기 위한 노력들.. 예를들면 Cloudfront에서는 Vue Router를 403즉 없는 페이지로 인식하는데 그런 페이지의 처리 부터 시작해서 ssl의 적용 그리고 서비스워커 템플릿을 이용했을때의 단점 등... 사실 배운것만 생각하면 최고의 프로젝트였다.

### 무엇을 배웠을까?

1. SPA
    - 라우터에 이동전 파라미터를 주고 받을때의 일
    - SPA앱을 구축하는데 특히 Head 태그를 관리하는 일
    - 데이터를 변경하고 가져올때 제대로 된 구조화를 하지 않으면 오히려 내가 힘들다는 것
2. AWS
    - Route 53
        - Api gateWay의 Custom doamin을 위해서.
        - S3의 버킷 접근을 좀더 용이하게 만들기 위해서.
    - S3
        - S3에서 버킷 URL을 짧게하기
    - CloudFront
         - SPA앱은 존재하지 않는 파일을 요청하니 무조건 403을 내뿜기에 여러가지 세팅이 필요했다.
    - Lambda
        - serverless-http를 사용할거면 람다에서 세팅을 하는 경우는 거의 없으며 대부분은 Serverelss.yml을 통해서 해결해야한다 (버킷 억세스 권한 등등)
3. 그외
    - Token 인증
        - 토큰 인증은 앞으로 대다수의 Session 방식을 사용하고 있는 웹에서 앞으로 지향해야할 방향이라고 생각한다.
    - Vuex
        - MVC패턴을 벗어나 Redux패턴 즉 Store 기반의 웹은 처음 도입하기에 조금 꺼려졌지만 특히 User의 정보를 담아 다양한 컴포넌트에서 활용을 하면서 사용하니까 너무나도 필요한 존재라는 것을 알게되었다.

지금 생각나는 것만 손에 꼽아도 상당히 많은 것들을 배울 수 있었다.

![고민의 흔적들](http://i.tac.photos/p/Skx0M1o3f.png)
상당히 많은 고민의 흔적들...

## 다음프로젝트는?
무조건 Firebase를 쓸 생각이다. 데이터베이스를 관리하며 SPA앱을 만들고 거기다가 서버사이드의 RESTful API를 만들며 작업하는건 상당히 많은 시간이 걸린다는 것을 다시 한번 깨우쳤다.

물론 graphQL을 한번 써서 프로젝트를 해보고 싶긴하지만 다음 프로젝트는 절대로 아니다. 앞으로의 개인프로젝트는 단순히 나의 포트폴리오 용도로 만드는것이 아니라 진짜 수익이 나는 괜찮은 앱을 만들어보고 싶기에 우선은 보여지는 프론트엔드 부분에 많은 고민을 할애하고 싶고 또 기획에 많은 고민을 하고 싶다.

## 마치며
서버리스 프로젝트는 너무나도 정말 최고였다. EC2서버를 운영할땐 스케쥴도 상당히 많이 체크해야 했고 동시접속을 얼마나 견딜 수 있을지 동일 요청을 얼마나 버틸지 등 많은 부분을 고민 해야 했다.

앞으로의 웹은 RESTful이 대세가 이룰것이라고 확신한다 아니 100%다. 물론 과거에는 Node.js개발자나 PHP등 서버사이드 개발자가 해야할 일이 서버관리와 유연한 데이터베이스를 설계하는 일 이었다면

이제는 분명히 프론트엔드와 백엔드의 무게가 동등 해지고 있다고 생각이 들었다.

웹을 만든다, 라는 생각을 하면 나는 정말 무조건 드는 생각이 있는데 바로 어떻게 하면 내 서버자원을 유저가 최대한 적게 사용할까?? 라는 고민이었다. 이 고민은 나의 첫 프로젝트였던 Overdoc - 오버워치 데이터 제공 웹을 개발할때도 했던 생각이었는데 

나는 죽어도 내 서버를 호락호락하게...크흠 아무튼 최대한 서버 요청은 적을수록 좋다고 생각한다. 지금까지도 그렇게 생각해왔지만 이번 프로젝트를 하고 나서는 정말 그런 생각이 더욱 커졌다.

앞으로의 RESTful기반 웹사이트는 당연히 서버리스가 좋다고 생각하고 이런 서버로의 요청을 조금이라고 덜 하기 위해서는 무조건적으로 프론트사이드에서 요청을 최소화 하기 위한 작업들을 많이 해줘야한다고 생각한다.

그리고 아무래도 이 프로젝트는 그동안 블로그에 글을 작성하며 이미지 업로드 하기가 귀찮았는데.. 그 용도로 쓰면 될것같다.

혹시라도 이 글을 읽는 분이 계신다면 [Tac.phtoos](http://tac.photos)한번 접속해주는 것도...

> 이번 프로젝트로 정말 많은걸 배웠다.