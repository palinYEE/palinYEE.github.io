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
tar xvzf elasticsearch-7.1.1-linux-x86_64.tar.gz

tar xvzf kibana-7.1.1-linux-x86_64.tar.gz
```
여기까지는 vmware 또는 virtualbox에 설치된 우분투에서 설치하는 것과 동일하다. 

## 2. 외부 접속 허용하기

우리가 서버에 있는 elasticsearch와 kibana를 외부에서 접속 하기 위해서 몇가지 셋팅이 필요하다. 

1. `elasticsearch/config/elasticsearch.yml` 파일을 수정해야 한다. 수정 해야할 것들은 다음과 같다.   

```
cluster.name: cluster 이름 설정
node.name: 노드 이름 설정
bootstrap.memory_lock: true
network.host: 0.0.0.0
discovery.seed_hosts: ["서버 ip 입력"]
cluster.initial_master_nodes: ["node.name 입력"]
```

2. `kibana/config/kibana.yml` 파일을 수정해야 한다. 수정 해야 할 것들은 다음과 같다. 

```
server.host: "서버 ip"
elasticsearch.hosts: ["1에서 설정한 elasticsearch host"]
```

3. `firewall-cmd`를 이용하여 포트를 열어준다.

```
firewall-cmd --permanent --zone=public --add-port=9200/tcp
firewall-cmd --reload
firewall-cmd --list-ports
```

## 3. 에러 발생 시 나오는 문구

위와 같은 셋팅을 모두 끝났다면 일반 docker나 우분투에서는 `./bin/elasticsearch`를 한다면 정상적으로 실행될 것이다. 하지만  서버 우분투에서는 다음과 같은 에러가 발생한다.

<center>[1] bootstrap checks failed</center>

이 에러 덕분에 나는 3시간을 낭비했다.. 하지만 이 블로그를 보는 사람은 그러지 않기를 바란다...

## 4. 셋팅 방법
서버에서 사용하기 위해서는 추가적으로 다음을 셋팅해주어야 한다. 

1. `/etc/security/limit.conf` 파일에 다음을 추가한다.

```
es_name hard nofile 65536 
# es_name는 하드세팅(해당 쉘 최대값) 으로 한 번 접속할때 65536번의 파일을 열어 볼 수 있음

es_name hard nofile 65536 
# es_name는 소프트세팅(해당 설정 값) 으로 한 번 접속할때 65536번의 파일을 열어 볼 수 있음

es_name hard nproc 65536 
# es_name는 하드세팅으로 한 번 접속할때 65536번의 프로시저를 실행 할 수 있음

es_name sort nproc 65536 
# es_name는 소프트세팅으로 한 번 접속할때 65536번의 프로시저를 실행 할 수 있음
```

2. `elasticsearch/config/jvm.options` 에 다음을 수정한다.

```
bootstrap.memory_lock: true
```

3. `sysctl -w vm.max_map_count=262144` 명령어를 입력한다.

이러한 과정을 거치고 다시 실행 한다면 정상적으로 작동하는 것을 볼 수 있다. 


----------
# Reference
* <https://msyu1207.tistory.com/entry/Elasticsearch-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EC%99%B8%EB%B6%80-%ED%97%88%EC%9A%A9>
* <https://antdev.tistory.com/63>