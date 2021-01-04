---
layout: post
title:  "[ELASTICSEARCH] 서버에 elasticsearch 설치하기"
# date:   2020-12-28T11:52:52-05:00
date:   2021-01-04T18:09:52-05:00
author: 윤영진
categories: elasticsearch
tags: elasticsearch 설치
cover:  "/assets/instacode.png"
---
# 서버에 elasticsearch를 설치해보자.

지금까지 나는 elasticsearch를 docker와 vmware에 있는 우분투에 설치를 해보았다. 이는 매우 간단했다. 하지만 서버 우분투에 설치할 경우 elasticsearch 와 kibana에 여러 셋팅을 변경해주어야 한다. 본 포스트 에서는 기본적인 elasticsearch 설치 및 여러 셋팅에 대해서 살펴보자. ( 본 포스터는 elasticsearch 7.1.1 버전을 기준으로 설명한다. )

## 1. elasticsearch와 kibana 설치

기본적인 설치는 매우 간단하다. 먼저 다음 두개의 파일을 준비한다. 

*  [elasticsearch7.1.1](https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.1.1-linux-x86_64.tar.gz)

* [kibana7.1.1](https://artifacts.elastic.co/downloads/kibana/kibana-7.1.1-linux-x86_64.tar.gz)

그리고 다음 명령어를 입력하여 압축을 풀어준다. 

```
tar -xvf elasticsearch-7.1.1-linux-x86_64.tar.gz

tar -xvf kibana-7.1.1-linux-x86_64.tar.gz
```
여기까지는 vmware 또는 virtualbox에 설치된 우분투에서 설치하는 것과 동일하다. 

## 2. 외부 접속 허용하기

우리가 서버에 있는 elasticsearch와 kibana를 외부에서 접속 하기 위해서 몇가지 셋팅이 필요하다. 

## 3. 에러 발생 시 나오는 문구

하지만 서버 우분투에서 `./bin/elasticsearch`를 한다면 다음과 같은 에러가 발생한다. 

<center>[1] bootstrap checks failed</center>

이 에러 덕분에 나는 3시간을 낭비했다.. 하지만 이 블로그를 보는 사람은 그러지 않

## 4. 셋팅 방법

----------
# Reference
* <https://msyu1207.tistory.com/entry/Elasticsearch-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EC%99%B8%EB%B6%80-%ED%97%88%EC%9A%A9>
* <https://antdev.tistory.com/63>