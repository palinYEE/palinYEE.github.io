---
layout: post
title:  "[ELASTICSEARCH] docker Toolbox에 elasticsearch 설치하기"
date:   2021-01-08T10:00:52-05:00
author: 윤영진
categories: elasticsearch
tags: elasticsearch 설치 docker
cover:  "/assets/instacode.png"
---
# docker Toolbox에 elasticsearch 설치하기

## docker Toolbox란?
윈도우는 리눅스와는 달리 도커를 사용하기에 좋은 환경이 아니다. 하지만 docker는 윈도우에서 사용할 수 있게 다음 두가지를 제공한다.

* docker for window
* docker Toolbox

위 두개의 차이점은 바로 가상화를 어디에서 하는가이다. docker for window는 자체 가상화 기술로 리눅스 환경을 만든 후 컨테이너를 생성하지만, docker Toolbox는 설치할때 같이 생성된 virtualbox에 리눅스 vm을 생성하고 거기에 도커를 설치하는 방식으로 진행된다. 이에 대한 그림은 다음과 같다. 

![Alt text](/assets/elasticsearch/docker.PNG "docker")

여기서 내가 docker toolbox를 사용한 이유는 내 기준에서 좀더 다루기 쉬워서이다. 

## docker Toolbox에 elasticsearch & kibana 설치하기

1. elasticsearch 와 kibana 이미지 다운받기

<pre>
<code>
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.10.1
docker pull docker.elastic.co/kibaba/kibana:7.10.1
</code>
</pre>

2. 실행

<pre>
<code>
docker run -d --name elastic -p 9200:9200 -p 9300:9300 -e 
"discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.10.1

docker run -d --name kibana --link elastic:elasticsearch -p 5601:5601 
docker.elastic.co/kibana/kibana:7.10.1
</code>
</pre>


이와 같이 실행을 했다면 다음부터는 다음 명령어를 통해서 간단하게 실행할 수 있다.

```
docker start elastic
docker start kibana
```

실행결과 : 
![Alt text](/assets/elasticsearch/dockerTool_els_success.PNG "elasticsearch success")
![Alt text](/assets/elasticsearch/dockerTool_kibana_success.PNG "kibana success")