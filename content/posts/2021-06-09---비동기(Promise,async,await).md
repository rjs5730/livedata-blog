---
title: 비동기(Promise,async,await)
date: "2021-06-09T22:40:32.169Z"
template: "post"
draft: false
slug: "Javascript Promise"
category: "Javascript"
tags:
  - "Javascript"
  - "function"
description: "자바스크립트 비동기를 알아보고 Promise, async와 await 사용법을 공부해봅시다."
socialImage: "/media/javascript-image.png"
---

## Promise

- 자바스크립트 비동기 오브젝트
- state: pending 에서 fulfilled of rejected 상태 변화가 있다.
  - pending : 대기
  - fulfiled : 이행
  - rejected : 거부
- 비동기는 Producer와 Consumer로 구분된다.

### 1. producer

새로운 프로미스 객체가 생성하면 자동적으로 안에 있는 함수가 호출된다.

```jsx
const promise = new Promise((resolve, reject) => {
  // 네트워크를 통하는건 비동기적으로
  console.log("doing something");
});
```

## Promise.all(프로미스 배열)

- 여러가지 작업을 동시에 병렬로 처리하고 싶다면 Promise.all 사용한다.

```jsx
function multiply5 (number) {
	return new Promise((resolve, reject) => {
		setTimeout(() => {
			let result = number * 5;
			console.log(result);
			resolve(result);
		}, 1000);
	});
}
Promise.all([
	multiply5(5),
	multiply5(10),
	multiply5(20)
]).then(result => {
console.log('result', result);
});

### 결과값 1초후 5,10,20
```

## Promise.race(프로미스 배열)

- Promise.all() 이 실행한 모든 프로미스들의 결과값을 배열로 받는 것과 달리 Promise.race()는 가장 빨리 응답을 받는 결과값만 resolve한다.

```jsx
function multiply2(number) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      let result = number * 2;
      resolve(result);
      console.log("result", result);
    }, 1000 * number);
  });
}
Promise.race([multiply2(3), multiply2(2), multiply2(1)]).then((result) => {
  console.log("final result", result);
});
```

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/db124af6-7799-411f-9a21-609c88487ba2/Untitled.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/db124af6-7799-411f-9a21-609c88487ba2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210615%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210615T151502Z&X-Amz-Expires=86400&X-Amz-Signature=1669c94c168ee6e790c3009904f92507888bc18ebb7db930ae3f4b95acc85b8e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

2가 가장먼저 출력후 순서대로 4 6이 출력된다.

## Async & Await

- 비동기를 동기적프로그래밍으로 만들 수 있다
- 함수 앞에 async 를 붙히면 Promise 가 리턴된다

```jsx
function delay(time) {
  return new Promise((resolve) => {
    setTimeout(resolve, time);
  });
}

async function getApple() {
  await delay(1000);
  return "사과";
}

async function getBanana() {
  await delay(1000);
  return "바나나";
}

// 동시 다발적으로 호출할 경우, 병렬 수행 (이렇게 하지는 않음)
async function pickFruits() {
  // 프로미스를 만들면 프로미스가 바로 호출된다.
  const applePromise = getApple();
  const bananaPromise = getBanana();
  const apple = await applePromise;
  const banana = await bananaPromise;
  return `${apple} + ${banana}`;
}

// 모든 함수가 호출될때까지 기다린다.
async function pickAllFruits() {
  // 프로미스를 만들면 프로미스가 바로 호출된다.
  const fruits = await Promise.all([getApple(), getBanana()]);
  console.log(fruits);
}

async function pickOnlyOneFruits() {
  // 프로미스를 만들면 프로미스가 바로 호출된다.
  return Promise.race([getApple(), getBanana()]).then((fruits) =>
    fruits.join(" + ")
  );
}
```
