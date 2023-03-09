---
layout: post
title: "어떻게 프리서버를 만드는것을 배웠는지"
subscript: "지인하고.. 즐겼습니다 ㅠㅠ"
tags: ['자랑 아님', '엄연한 불법 행위']
categories: ""
comments: true
permalink: /lie/:title
date: 2020/09/03
---

프리서버 운영은 엄연한 불법 행위 입니다.

> 저작권법 제101조의4(프로그램코드역분석) ① 정당한 권한에 의하여 프로그램을 이용하는 자 또는 그의 허락을 받은 자는 호환에 필요한 정보를 쉽게 얻을 수 없고 그 획득이 불가피한 경우에는 해당 프로그램의 호환에 필요한 부분에 한하여 프로그램의 저작재산권자의 허락을 받지 아니하고 프로그램코드역분석을 할 수 있다.

라고 [나무위키](https://namu.wiki/w/%ED%94%84%EB%A6%AC%EC%84%9C%EB%B2%84)에서 설명하고 있습니다.

## 프리서버라는 말을 접하게된 계기

초등학교 시절 거상에 흠뻑빠져 있었다. 사냥에는 흥미가 없고 하루종일 짐꾼과 돌아다니면서 벼를 팔아 시세 차익을 내거나 한양에서 장사를 하거나 하는 행위를 주로 했다.

장사를 계속 하다보니까 자연스레 친구가 많이 생겼는데 어느날 한 사람이 나에게 '프리서버'라는걸 해본적이 있냐고 물었다. 나는 당시 프리서버라는 것에 대해서 아니 프리라는 단어 자체를 영어로 쓰지 못할정도로 어린 나이 이기 때문에 그의 이야기에 흠뻑 빠졌다.

1. 레벨업은 내가 원하는대로 마음대로
2. 내가 가지고 싶은 장비도 마음대로
3. 그냥 게임 자체를 내 마음대로

## 초등학교 3학년 폭풍 검색 시작

정확히 어떤 엔진을 사용해서 검색한지는 잘 기억이 안나지만 몇개 추려 보자면

- 인포마스터? (이제는 존재하지도 않는 검색 사이트)
- 네이버 (전혀 나오지 않음)
- 다음
- 파란

등을 사용해 검색을 몇달간 계속 했다.

그러나 초등학교 3학년의 통찰력과 이해로 무엇을 할 수 있으리.. 나는 당연히 프리서버를 구현하지 못했다.

## 그렇게 2년뒤 피씨방에서 라그나로크 프리서버를 하는 형들을 발견

아직도 기억이 난다 그 형들의 레벨업소리가 타탁! 한 마리를 잡으니 레벨이 바로 40이 되는걸 보고 말았다. 나는 불현듯 이게 프리서버라는 거구나라는 생각을 했고 뒤에서 하염없이 지켜봤다.

> 야 저리가

나보고 거의 꺼지라는 수준의 말로 저리가라고 했지만 저 멀리서 계속 지켜봤다.

그리고 그현들이 오는 시간에 맞춰서 피씨방에 출근했다..

그리고 며칠 음료수를 형들의 책상에 두고 뒤에서 지켜보았다.

그렇게 한 일주일이 지나고 나도 드디어 형들의 프리서버에 들어갈 수 있는 자격이 생겼다.

그들은 프리서버를 운영하고 있었고 가끔 피씨방에 와서 둘이서 이것저것 게임을 고치면서 노는 학생이었다.

## 어떻게 구현하는지 배워야 했다

나에게는 7살 많은 형이 있었는데 내가 피씨방에서 보고 온것을 형은 믿지 못했다. 아니 게임을 참가 했다고 해도 형은 무슨 개소리냐며 비아냥대기 바뻤고 급기야 아버지에게 피씨방에 가지 못하게 하라고 얘기하기 시작했다.

오기로 이것을 배워 형하고 피씨방에 갔을대 내가 구현한것을(? 내가 구현한것은 없는데..) 보여줘야만 했다.

그로부터 피씨방에 조금 더 일찍 가기 시작했다.

옆에서 형들이 하는것을 보고 따라하고 그렇게 읿주일 나도 통파일(구현이 전부 담겨있는 팩? 같은 것)을 어떻게 구하는지와 어떻게 서버를 여는지를 배우게 되었다.

내 기억이 맞다면.

1. mysql을 통해 db서버를 연다
2. 내 서버 주소를 어떤 메모장에 옮겨 적는다.
3. 통파일 압축해제
4. 통파일에서 나온 .bat 실행 또는 cmd에서 무슨 명령어를 입력

이렇게 하면 내 서버가 열리고 실행은 또 그냥 안되고 통파일에서 나온 압축 해제된 클라이언트 폴더에 가서 세팅을 바꿔줘야 한다.

아무튼 이렇게 해서 라그나로크 프리서버를 여는 방법을 배웠고 이후에 리니지, 바람의 나라 등을 중학교때 까지 한번 한번씩 열었었다.

그런데 내가 성인이 되서도 mysql을 만질줄이야!