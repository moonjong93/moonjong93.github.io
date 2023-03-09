---
layout: post
title: "jekyll action"
subscript: "과연 이게 잘 되나"
tags: ['jekyll', 'github action']
categories: ""
comments: false
permalink: /life/:title
date: 2020/09/03
---

빌드가 잘 된다면 블로그 글을 이어서 작성
---

# jekyll action

jekyll을 구성하는데 있어서 많은 불편함이 있다.

일단 gem 자체가 많은 permission을 요구하는것도 사실이고 설치하다가 중간에 잘못되면 그냥 블로그 안하게 되고

이게 한 2년은 된것 같다.

테스트가 잘 되는지.. 어떻게 되는지?


---

내가 사용한 yml은 아래와 같다

```yml
name: Jekyll site CI

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Build the site in the jekyll/builder container
      run: |
        docker run \
        -v ${{ github.workspace }}:/srv/jekyll -v ${{ github.workspace }}/_site:/srv/jekyll/_site \
        jekyll/builder:latest /bin/bash -c "chmod 777 /srv/jekyll && jekyll build --future"
```

이렇게 놓고 푸시를 하면 알아서 당겨 간다.

위의 구문은 별도의 공부 없이고 대충 이해할 수 있는 수준이라서 별도의 설명은 안해도 될것 같다.

아무튼 블로그는 그냥 계속 깃헙에 작성 하는걸로 해야겠다.
