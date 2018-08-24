---
layout: post
title: "나는 graphql을 이해했다"
subscript: "graphql을 만능 라이브러리라고 잘못 이해했던 개발자"
tags: ['graphql', 'mysql']
categories: ""
comments: true
permalink: /study/:title
date: 2018/08/16
---

## Graphql은 무엇일까?
대다수의 블로그를 보면 마치 정말 전지전능한 실제 기술같았다. 왜냐면 꼭 파이어베이스와 같이 서버리스 플랫폼에서 제공하는 플랫폼의 '라이벌'이라고 얘길 해서 나는 Firebase('이하' 파이어베이스) 같이 별다른 설정 없이 사용할 수 있는줄 알았다.

> 잘못된 이해였다

실제로 Graphql과 RESTfullAPI의 설계는 많은 차이를 보이지만 결국엔 내가 컨트롤 한다는 점에선 변화가 없고 대신 라우터의 관리 파라미터의 관리가 엄청 쉬워진다는 장점이 있다.

기존에 JWT토큰을 발행하기 위해서 /login/createjwttoken이라는 라우터에서 파라미터를 받아서 컨트롤 하기 위해서 Node.js에 새로운 라우터를 만들고........

이런 행위를 하지 않고 모든 라우터를 graphql에 묶어서 관리해주면된다.

## 그럼 무엇을 잘못 이해했을까?

나는 Graphql을 접하기전에 파이어베이스를 먼저 접했다. 파이어베이스는 별다른 설정없이 데이터를 설계하고 스키마 설계를 필요하지도 않고 단지 그냥 그저 쓸 뿐이었다.

난 Graphql이 그런건줄 알았다. 대다수의 블로그 글들은 Query와 Mutaion과 같은 데이터를 불러오는 예제만 기록되어있었다.

Node.js에서 별다른 설치없이 데이터베이스와 연결만하면 Sequlize라는 ORM 기반 모듈처럼 데이터베이스도 알아서 만들어주고 테이블도 알아서 관리해주는줄 알았다.

> 그러나 완전히 반대였다.

## 그러면 내가 이해한 Graphql은?

이번 개인프로젝트에 적극적으로 도입해서 모든 요청은 Graphql로 처리하고있다,

가장 이해하기 힘든 부분은 '로그인'에 대한 처리였는데 이걸 이해하고선 Graphql을 빨리 이해할 수 있었다.

우선 Graphql은 데이터베이스를 직접적으로 만들어주지 않는다. Resolver라는 부분을 통해서 요청이 들어오면 해당 요청을 검토하고 데이터를 컨트롤 해야한다.
~~~javascript
export default {
    // 로그인 -> JWT토큰 만들어서 token을 리턴해줌 
Query: { 
        login: (_, {email, password}, ctx) => {
            console.log(ctx)
            return models.User.findByEmail({email, password})
            .then( (user) => {
                if(user.password == createHash(password)){
                    return createJWTToken(user.id, user.displayName)
                    .then((token) => {
                        return { token }
                    })
                }else{
                    return new Error('not matched password')
                }
            })
            .catch((err) => {
                return new Error('not found user')
            })
        },
    },
}
~~~

위와 같이 결국 데이터를 직접 조회해서 해당 데이터를 비교후에 리턴값으로 Token이라는 기존에 저작되어있는 타입을 리턴해준다 Token의 값은 단순 String에 속한다.

~~~javascript
type User {
        id: ID!
        email: String! @isUnique
        password: String!
        displayName: String!
    }

type Token {
    token: String!
}

type Query {
    login(email: String!, password: String!): Token
}

type Mutation {
    register(email: String!, password: String!, displayName: String!): User
}
~~~

결국엔 Json으로 들어온 객체를 통해 받아온 데이터를 활용해서 알맞는 리턴값을 구해서 만들어줘야한다는 점이다.

결국에 내가 생각했던 '연결만 하고 타입설정만 하면 끝'이라는 것과는 너무 큰 차이가 있었다.

## Graphql을 사용하면서의 이점
아무리 그래도 직접 Router를 통해서 하나하나 Post부터 시작해서 Get등 다양한 메서드를 갖는 라우터를 설계하는것보단 훨씬 작업 속도가 빨랐다.

## Graphql을 앞으로도 계속 사용할건지?
> 네!

당장 스텍오버플로우만 봐도 그렇듯 상당히 많은 수요가있다. 그리고 막상 사용해보니 처음 이해할때만 조금 어려웠고 막상 이해하고 나니 파일관리도 편하고 기본적으로 Apollo 라는 모듈을 사용할땐 서버를 별다른 설정을 하지 않아도 테스트할 수 있게 서버를 만들어줘서 상당히 편리했다.
