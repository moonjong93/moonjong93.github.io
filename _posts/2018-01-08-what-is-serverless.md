---
layout: post
title: "서버리스에 관하여"
subscript: "firebase는 갓갓베이스입니다"
tags: ["server", "pass", "google colud", "firebase"]
categories: "개발"
comments: true
permalink: /develop/tech/:title
date: 2018/01/08
---

나는 최근에 firebase에 관한 얘기를 개발자들의 세미나에서 얘기한 경험이 있다,

> 서버리스의 대표적 선두주자이면서 상당히 관리하기 편리하기에 서버에 지식이 없는 사람도 쉽게 입문해서 자신이 원하는 앱을 만들어 낼 수 있기에 지금처럼 변화가 빠른 세상에서 빠르게 개발하기에는 정말 최고의 서비스

의견은 다소 나뉘었는데, 그 중에서 이해가 안되는 부분이 있는데 느려터져먹었으며 그딴걸 누가 사용하냐는 다소 과격한 언행이 나오기 시작했다.
나는 파이어베이스를 사용은 해봤냐고 묻고싶다 그리고 firebase가 과연 어떤 서비스를 제공하는지 대충이라도 알고 나의 얘기에 토를 달았으면 좋겠다.

## 1. 파이어베이스가 제공하는 것

우선 파이어베이스가 무엇을 제공하느냐를 알아야 할 필요가 있다 파이어베이스하면 단순히 리얼타임 데이터베이스만 생각하는 사람도 많을 것이다 나도 처음엔 그랬으니까

그러나 파이어베이스는 단순히 데이터베이스만 제공하는 서비스가 절대로 아니다 일단 데이터베이스부터 언급하자면 데이터베이스는 실시간으로 조회되며 연결된 데이터베이스가 변경될시 observer패턴을 사용한 데이터베이스 이기에 바로바로 변경점을 해당 노드에 연결된 사용자에게 알려주는 그런 서비스다.

즉 요즘 유행하는 가상화폐에서 사용한다면 생각보다 큰 부하없이도 데이터베이스를 가져올 수 있다

그 밖에도 Authentication 서비스는 클릭 몇번과 폼데이터 입력 한번으로 google로그인과 이메일 로그인을 연동 시킬 수 있으며

Storage 서비스는 말그대로 파일을 서버에서 호스팅할 수 있으며

Hosting 서비스는 firebase deploy 한번으로 vue나 react로 작성된 앱을 별다른 설정없이도 호스팅 할 수 있고

마지막으로 **functions** 서비스는 node.js로 작성된 코드를 업로드시켜두면 어디서나 사용할 수 있는 node.js 서버로 활용이 가능하다, 간단하게 말하자면 Nodemailer라는 모듈을 임포트 시켜 굳이 서버를 가지고 있지않아도 메일을 보낼 수 있다는 얘기다(ajax)

이 밖에도 보안과 유저 분석을 제공한다.

## 2. 파이어베이스로 할 수 있는것

사실 파이어베이스 자체를 가지고 커뮤니티를 만들겠다고 한다면 조금은 반대하고 싶다 NoSql기반의 데이터베이스는 제목 검색도 하기 힘들기 때문이다, 여기에서 누군가는 얘기한다 "그딴 쓰레기 서버 누가쓰냐고" 아니 대체 왜 제대로 알지도 않고..크흠..

파이어베이스 자체로서 쓴다면 사실 사용처가 제약적인건 사실이다 그러나 [Google Cloud Platform](https://console.cloud.google.com/)에 들어가보자 Mysql부터 많은 서비스가 제공되고있다.

파이어베이스 functions로 Mysql 연결후 커뮤니티를 만든다면 한글 제목도 검색되며 괜찮은 커뮤니티를 제공 할 수 있을것이다.

## 3. 사용해보고 욕합시다

대부분 파이어베이스가 어떤 서비스도 제공하는지도 모르며 느려터진 서비스라고 욕을하던데.. 대체 어떤 서비스가 느리다는 건지 잘모르겠다 리얼타임 데이터베이스를 정말 제자리에서 사용하고 있는건가? 리얼타임 데이터베이스가 느리다고 느꼇다면 아마도 처음부터 해당앱이 어떤 기능을 제공해야하고 어떤 데이터베이스를 사용하는지 이해하는것이 필요하다.

## 4. 서버리스에 대해서

서버는 말 그대로 서버가 존재하지 않는 서비스를 의미한다 서버가 존재하지 않는다고 서버가 없지는 않은 그러니까 말 장난인 셈인데 위에서 언급했던것과 마찬가지로 필요한 상황이 있으면 paas(platform as a service)를 사용해서 서버를 잠깐 빌려서 쓴다고 보면될것 같다.

대표적으로 firebase, google colud platform, aws lamda 등이 있다.

서버리스는 모든걸 다할 수 있는 개발자에게는 어울리지 않는 개념이다, 분명 우리들의 서버는 어제까지 잘 동작하다가 다음날 안되는 경우가 있었다. 분명 어제 까지는 구글로그인이 정말 잘되었는데 여행 출발 당일 알 수 없는 오류를 내뿜으며 로그인이 안되던 나의 앱은 여행을 포기하게 만들었다.

나는 분명 언급했다시피 개인개발자이다 풀스텍 개발자가 되기로 마음먹고부터는 Node.js 그리고 리눅스의 우분투부터 센토스 등등 정말 중요한것은 내가만든 앱의 재미고 설계지 언제까지 서버 때문에 포기하고 서버의 볼륨을 계산하지 못해서 서버가 끊겨 유저이탈을 경험 할 수 없었다.

서버리스는 스타트업 그리고 개인개발자라면 분명히 염두해 두어야한다 내가 아무리 코드를 잘짜도 사실 사용자는 별로 관심도 없다 어떤 서버를 어떻게 만들어서 잘 만들어도 그냥 앱이 정말 재미있고 좋은 앱이어야 성공한다

나는 상당히 많은 시간을 서버에 대한 고민을 하며 개발을 했다 그러나 개인개발자에겐 하루빨리 출시해서 결과를 보는게 중요하다고 생각한다 그러나 서버에 대한 고민 그리고 스토리지에대한 고민까지 그 모든걸 혼자서 풀어내기엔 부담스럽기 그지없다.

그래서 나는 paas(Platform as a Service)를 사용하고 있다
