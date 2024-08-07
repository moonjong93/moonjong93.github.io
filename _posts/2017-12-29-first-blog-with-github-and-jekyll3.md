---
layout: post
title: "Jekyll로 시작하는 블로그 - 에필로그"
subscript: "블로그 입문기 마지막 이야기"
tags: ["Jekyll", "Blog"]
categories: "개발"
comments: true
permalink: /develop/blog/:title
date: 2017/12/26
---

## 한것도 없이 마지막

그렇다 마지막이다 너무 두서 없이 쓴거같고 그냥 휘겨 갈겨 쓴것 같아서 빨리 마무리를 지어야겠다

## 1. Jekyll의 Liquid 시스템을 대충 알아보자

지킬의 친절한 [안내 페이지](https://jekyllrb-ko.github.io/docs/variables/)를 보면 알 수있지만 Liquid 템플릿 시스템(이는 대부분 블로그 플랫폼이 지원하는 언어)이 적용되어있는데 예를들면 \_config.yml파일에 name : "Moonjong93"이라고 적용 해두면 어느 페이지에서건

```
site.name
```

과 같은 변수로 접근이 가능하다 아주 편리한 시스템인데 이 블로그의 레이아웃을 잠깐 보자면

```html
<div class="main-container">
  include top.html content include copy.html include analytics.html
</div>
```

이런식으로 이루어진 코드가 상당히 많다

> include는 data안에 넣어둔 파일을 넣을 경우 사용

필요할때마다 코드를 불러와서 쓰는건 상당히 불편한데 위와같은 템플릿도 지원하기 때문에 상당히 쉽게 만들 수 있었다.

예를들면 위에서 top.html을 include하였는데 모든 페이지에서 상단에 있는 'Moonjong93과 Abuout'에 접근할 수 있게끔 하나만 만들어두고 어느 레이아웃에도 추가해두었다.

## 2. 레이아웃이란?

```html
---
layout: index
title: Welcome
---

<div class="container">
  <div calss="posts">
    for post in paginator.posts
    <div class="post">
      <a href=" post.url "><h3 class="post-title">post.title</h3></a>
      <p class="post-subscript">post.subscript</p>
      <p class="post-date">post.date | date: '%Y-%m-%d'</p>
    </div>
    endfor
  </div>
</div>
```

위는 이 페이지에 index즉 제일 첫 페이지 코드의 일부분인데 보면 알다시피 레이아웃은 index 레이아웃을 통한다 index 레이아웃은 모든 전체적인 폼만을 만든다 분리를 하게되면 효율적이게 코드관리가 가능하다

예를들면 모든 페이지에서 필요한 공통부분은 레이아웃에 미리 저장해둔다 그리고 head태그 역시 레이아웃에 정의해둔다 **변경 되는 부분은 reqiurd 템플릿 문법으로 정의한다**
페이지 별로 보여지는 title이 다를경우

```
---
layout: index
title : "hello" // 이 부분을 수정해서 가능해진다
---
```

이런식으로 편리한 템플릿을 제공하기에 기본 문서만 본다면 누구나 블로그를 만들 수 있다.

## 3. 검색엔진 최적화는?

처음 이 블로그를 올리고 1주일은 아무글도 구글에 검색되지 않았다 그래서 우선은 네이버 웹마스터를 통해 부족한 부분을 보완했다.
![네이버 웹마스터 결과 값](/assets/img/postsImg/naver-web-master.png)

가장 중요했던 부분은 RSS나 sitemap의 제출인데 이것은 \_config.yml파일에

```
plugins:
  - jekyll-feed
  - jekyll-sitemap
```

구문만 있으면 알아서 생성해주기에 상당히 편했다 바로 어제 저렇게 해서 네이버 웹마스터 최적화 이후 구글에서도 웹마스터 등록후 최적화를 진행했는데 현재 구글 검색결과에 잘 표시되는 것을 확인 할 수 있다

검색은 Moonjong93으로 하였다.

![최근 구글 검색결과 Moonjong93으로](/assets/img/postsImg/google-serach-after.png)

몇줄의 코드만으로도 검색엔진 친화적 블로그가 완성되었다

## 4. 기타 플러그인

댓글은 disqus를 사용하고 있다. 커스터 마이징이 사실 거의 불가능하다 싶은데 최근 댓글 목록같은 경우엔 데이터를 조회해서 가져온뒤 css파일로 수정했다.

댓글에 어느 페이지에서 작성했는지 까지 나오기 때문에 보기가 조금 지저분하다고 느껴서 아예 dispaly: none을 해두고 a태그만 가져온뒤 다시 위에 덮어씌워서 처리했다

```javascript
document.querySelectorAll("li.dsq-widget-item").forEach(function (me) {
  var atag = document.createElement("a");
  atag.innerHTML = me.innerHTML;
  atag.setAttribute("class", "dsq-coment");
  atag.setAttribute("href", me.childNodes[5].childNodes[2].href);
  me.parentNode.insertBefore(atag, me);
  me.remove();
});
```

물론 jquery를 사용하면 상당히 편하게 되겟지만 이번 블로그에서는 jquery를 아예 사용하지 않고 만들고 있다.

그리고 구글의 애널리틱스는 마찬가지로 include폴더에 다운로드 해서 모든 페이지에 inlcude 시켜주었다.

## 5. 마무리 하며

사실 마크업도 모르는 놈이 마크업으로 된 블로그를 만들기까지 굳이 필요없는 짓거리를 이것저것 했다(firebase with vue.js를 하면서)그러나 분명한건 완전히 헛짓거리는 아닌게 이번 경험을 통해 검색엔진을 신경쓰기 위해서 포기해야할 일이라던지(아무도 안보는 블로그가 대체 무슨 쓸모가..) 사용자 친화적 이라기보다 검색봇 친화적인 태그 사용등을 경험하며 사람들이 많이 쓰는 블로그 ex)티스토리, 워드프레스에는 그럴만한 이유가 있다는 생각이 들었다.

! 감사합니다 !
