---
layout: post
title: "AWS의 S3에 CNAME을 연결하기"
subscript: "S3에 도메인 지정이 필요하다"
tags: ["AWS", "S3", "DNS"]
categories: "개발"
comments: true
permalink: /AWS/:title
date: 2018/03/29
---

## 왜?

버킷을 처음 생성해 그 도메인 그대로 사용하면 상당히 긴 도메인이 나온다. 내가 만들고 있는 프로젝트에 이미지를 공유하는게 주된 목적인데 EX)https://s3.amazonaws.com/test.tac.photos/DASNKFDSANf134ia9s90fd.jpeg 이렇게나 긴 도메인은 보기도 힘들고 복사해서도 길이가 너무 길어서 편하자고 사용한 내 웹사이트에서 오히려

> 왜 이따구로 주소가 길어??

라는 불편함을 느낄것 같았다.

## 준비

우선 버킷의 생성이 필요하다.

1. 내가 원하는 도메인을 구매한다.
   - [GoDaddy](https://kr.godaddy.com/)를 추천한다.
   - 참고로 나는 GoDaddy에서 구매후 네임서버를 ROUTE53으로 이전해서 사용중이다.
2. 버킷은 내가 사용하려고 하는 도메인의 주소와 일치하게 해서 생성
   - 예) 버킷을 test.domain.com으로 생성한다.

이렇게 구매와 생성이 끝났다면 거의 모든일을 해냈다.

## 어떻게?

1. 버킷에 접속한다. (AWS 관리페이지를 통해서)
2. 내가 만든 버킷에 들어간다.
3. 버킷의 속성을 클릭한다.
4. '정적 웹 사이트 호스팅'을 클릭한다.
5. '이 버킷을 사용하여 웹 사이트를 호스팅합니다'를 체크
   - 인덱스 문서에는 index.html
   - 오류 문서에는 error.html을 입력
   - (실제 파일이 존재하지 않아도 된다)
6. 저장
7. 다시 '정적 웹 사이트 호스팅'을 클릭
8. 상단에 엔드포인트를 복사
9. 현재 가지고있는 도메인의 관리 서비스로 이동
10. CNAME으로 등록
    - 예) test.domain.com이라는 이름으로 CNAME이 가르키는 주소를 아까 복사한 엔드포인트 'test.test.com.s3-website-us-east-1.amazonaws.com'와 같은 URL을 입력해준다.
11. 5분 정도 기다리면 내가 새로 업로드하는 어떤 이미지도 test.domain.com/test.jpg로 접근이 가능하다.

## 마치며

물론 요청을 리다이렉션해서 2개의 버킷을 생성후 하나는 오로지 리다이렉션 정보만 담게도 설정이 가능하다.

> 만약 기존에 사용중인 S3 버킷이 있다면.

그러나 제일 처음부터 한다면 위에 나와있는 대로 하는게 좋을것 같다.
