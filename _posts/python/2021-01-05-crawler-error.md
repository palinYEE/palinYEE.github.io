---
layout: post
title:  "[PYTHON] 크롤링 시 나타나는 에러에 대한 고찰 "
date:   2021-01-05T18:09:52-05:00
author: 윤영진
categories: python
tags: python crawling network
cover:  "/assets/instacode.png"
---
# 크롤링 시 나타나는 에러에 대한 고찰

크롤링 코드를 비동기를 이용하여 돌렸더니 자주보이는 에러들이 발생하였다. 처음에는 불안정한 네트워크라는 생각을 했지만 지금 보니 이에 대한 에러 내용은 확실하게 알고 가야 할 것 같다. 

## 1. ProxyError : Host unreachable

뜻 자체는 호스트를 검색할 수 없다는 이야기이다. 

## 2. ProxyTimeoutError : Proxy connection timed out: 60

socks5를 이용해서 커넥션을 맺을 때 timeout 시간을 지정할 수 있다. 내가 지정한 시간은 60초인데, 커넥션 맺는 60초 동안 성공을 못해서 이러한 에러가 발생한다. 

하지만 이 에러의 문제점은 브라우저를 통해서 url에 접근 하는 것은 가능한 것이 있다. 

------------

ps. 아직 이러한 원인을 정확하게 밝혀내지 못하였으며 해결되는 즉시 업로드 할 예정이다.