---
title: Javascript 이벤트루프(Event Loop)
date: "2021-06-10T22:40:32.169Z"
template: "post"
draft: false
slug: "Javascript Event Loop"
category: "Javascript"
tags:
  - "Javascript"
  - "core"
description: "자바스크립트 이벤트 루프에 대해 알아보고 크롬의 V8 엔진이 비동기에 대해 어떻게 처리하는지 알 수 있습니다."
socialImage: "/media/javascript-image.png"
---

## 이벤트 루프를 잘 설명한 유튜브 영상

[![Watch the video](/media/eventloop-youtube.png)](https://www.youtube.com/watch?v=8aGhZQkoFbQ&t=147s)

자바스크립트는 단일 스레드 기반 언어 지만 **동시성(Concurrentcy) 를 지원**한다. 여기서 단일스레드는 자바스크립트엔진이 단일 호출스택을 사용한다라는 관점이다. 브라우저에서는 여러 스레드가 사용되며 이 자바스크립트 엔진과 상호 연동하기 위해 사용하는 장치가 이벤트 루프이다.

이벤트 루프 기반의 비동기 방식으로 Non-blocking IO 를 지원한다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ea03d1bf-f1b4-4af7-a410-f34b069d403b/Untitled.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ea03d1bf-f1b4-4af7-a410-f34b069d403b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210615%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210615T153851Z&X-Amz-Expires=86400&X-Amz-Signature=6eea485d4e83971cab596365e410b23e0a59b53ed83a4e288e0ed005aeb37504&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

비동기를 호출하기 위해서는 Wep API 영역에 따로 정의되어 있다.

이벤트 루프와 태스크 큐와 같은 장치도 자바스크립트 엔진 외부에 구현되어 있음

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/673d163a-78f9-4836-aebb-6042f6ecd592/Untitled.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/673d163a-78f9-4836-aebb-6042f6ecd592/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210615%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210615T153922Z&X-Amz-Expires=86400&X-Amz-Signature=c18beb0dd58a730cf185740efc351531d865c0e2ab8cbfde8ece9fb2638d4e4b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

노드 JS 에 LIBUS라는 라이브러리를 사용하여 이벤트 루프를 제공하고 있다.

### 테스크 큐와 이벤트 루프

태스크 큐는 말 그대로 콜백 함수들이 대기하는 큐(FIFO) 형태의 배열, 이벤트 루프는 호출 스택이 비워질 때마다 큐에서 골배함수를 꺼내와서 실행하는 역할을 해준다.

이벤트 루프는 현재 **실행중인 태스크가 없는지**와 **태스크 큐에 태스크**가 있는지를 반복적으로 확인

- 모든 비동기 API들은 작업이 완료되면 **콜백 함수를 태스크 큐에 추가**한다.
- 이벤트 루프는 '현재 실행중인 태스크가 없을 때'(주로 호출 스택이 비워졌을 때) 태스크 큐의 첫 번째 태스크를 꺼내와 실행한다.

### 마이크로 태스크

일반 태스크 보다 더 높은 우선순위를 갖는 태스크

태스크 큐에 대기중인 태스크가 있더라도 마이크로 태스크가 먼저 실행된다.

### Event Queue 와 Job Queue

Event Queue는 테스크 큐와 동일한 역할을 한다

Job Queue 는 Microtask queue 와 동일한 역할 가지고 있다.

### Render Queue란

- Render Queue는 브라우저에서 사용자에게 래스터 이미지를 보여주기 위해HTML, CSS, Javascirpt 코드를 변환하는 과정을 의미한다.(rendering path 혹은 critical rendering path 라고도 한다.)
- DOM Tree -> CSS Tree -> CSSOM -> Render Tree -> Layouting> Layer Tree -> Paint -> GPU Syne -> Composition 순으로 이뤄지는데,Composition은 스크린에 그려진 Final Frame이다.

## 추가 참고

https://im-developer.tistory.com/113
