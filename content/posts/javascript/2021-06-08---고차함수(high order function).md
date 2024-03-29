---
title: ES6 고차함수(high order function)
date: "2021-06-08T22:40:32.169Z"
template: "post"
draft: false
slug: "Javascript hight"
category: "Javascript"
tags:
  - "Javascript"
  - "function"
description: "자바스크립트 고차함수를 설명합니다. 기존 for를 사용하는 방식과 달리 고차함수를 사용하여 많은 장점을 가질 수 있습니다."
socialImage: "/media/javascript-icon.png"
---

### 고차함수란?

- 고차 함수는 함수를 인자로 전달 받거나, 함수를 반환 하는 함수를 의미한다.
- 고차 함수는 꼭 자바스크립트에 한정 되어있지 않고, 대부분의 언어에서 지원하고 또 비슷한 방식으로 구현 할 수 있다.

### 고차함수를 써야하는이유

- for를 사용할 경우 조건 값을 정확히 알고 있어야한다.
- for 문을 계속 돌려도 똑같은 결과 값이 나올지 예측하기 힘들다.
- **map, set, forEach, reduce 등 개발자의 의도를 파악하기 쉽다.**

### concat()

문자열 합치는 함수

```jsx
const array1 = ["a", "b", "c"];
const array2 = ["d", "e", "f"];
const array3 = array1.concat(array2);

console.log(array3);
// expected output: Array ["a", "b", "c", "d", "e", "f"]
```

### ever()

배열 안 모든 요소가 주어진 함수 통과하는지 판단

```jsx
const isBelowThreshold = (currentValue) => currentValue < 40;

const array1 = [1, 30, 39, 29, 10, 13];

console.log(array1.every(isBelowThreshold));
// expected output: true
```

### some()

한개의 요소라도 통과하면 true 반환한다.

### filter()

주어진 함수를 통과하는 요소를 모아 새로운 배열 반환

```jsx
const words = [
  "spray",
  "limit",
  "elite",
  "exuberant",
  "destruction",
  "present",
];

const result = words.filter((word) => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```

### find()

주어진 판별 함수를 만족하는 첫번째 요소의 값을 반환

```jsx
const array1 = [5, 12, 8, 130, 44];

const found = array1.find((element) => element > 10);

console.log(found);
// expected output: 12
```

### findIndex()

주어진 판별 함수를 만족하는 첫번째 요소의 인덱스 반환

### from()

유사 배열 객체(array-like object)나반복 가능한 객체(iterable object)를 얕게 복사해새로운Array 객체를 만듭니다.

```jsx
console.log(Array.from("foo"));
// expected output: Array ["f", "o", "o"]

console.log(Array.from([1, 2, 3], (x) => x + x));
// expected output: Array [2, 4, 6]
```

### includes()

배열에 특정 요소가 포함되어 있는지 판별합니다.

```jsx
const array1 = [1, 2, 3];

console.log(array1.includes(2));
// expected output: true

const pets = ["cat", "dog", "bat"];

console.log(pets.includes("cat"));
// expected output: true

console.log(pets.includes("at"));
// expected output: false
```

### indexof()

지정된 요소를 찾을 수 있는 첫번째 인덱스를 반환하고 존재하지 않으면 -1 반환

```jsx
const beasts = ["ant", "bison", "camel", "duck", "bison"];

console.log(beasts.indexOf("bison"));
// expected output: 1

// start from index 2
console.log(beasts.indexOf("bison", 2));
// expected output: 4

console.log(beasts.indexOf("giraffe"));
// expected output: -1
```

### lastIndexOf()

배열에서 주어진 값을 발견할 수 있는 마지막 인덱스 반환

### join()

배열의 모든 요소를 연결해 하나의 문자열로 만든다.

```jsx
const elements = ["Fire", "Air", "Water"];

console.log(elements.join());
// expected output: "Fire,Air,Water"

console.log(elements.join(""));
// expected output: "FireAirWater"

console.log(elements.join("-"));
// expected output: "Fire-Air-Water"
```

### map()

모든 요소 각각에 대해 주어진 함수를 호출한 결과를 모아 새로운 배열 반환

```jsx
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map((x) => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```

### Array.of()

**`Array.of()`** 메서드는 인자의 수나 유형에 관계없이 가변 인자를 갖는 새 `Array` 인스턴스를 만듭니다.

`Array.of()`와 `Array` 생성자의 차이는 정수형 인자의 처리 방법에 있습니다. `Array.of(7)`은 하나의 요소 `7`을 가진 배열을 생성하지만 `Array(7)`은 `length` 속성이 7인 빈 배열을 생성합니다.

```jsx
Array.of(7); // [7]
Array.of(1, 2, 3); // [1, 2, 3]

Array(7); // [ , , , , , , ]
Array(1, 2, 3); // [1, 2, 3]
```

### reduce()

배열의 각 요소에 대해 주어진 reducer 함수를 실행하고 하나의 결과값을 반환

```jsx
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15
```

### reverse()

배열의 순서를 반전

### shift()

배열의 첫번째 요소를 제거하고 제거된 요소 반환

```jsx
const array1 = [1, 2, 3];

const firstElement = array1.shift();

console.log(array1);
// expected output: Array [2, 3]

console.log(firstElement);
// expected output: 1
```

### unshift()

```jsx
const array1 = [1, 2, 3];

console.log(array1.unshift(4, 5));
// expected output: 5

console.log(array1);
// expected output: Array [4, 5, 1, 2, 3]
```

### slice()

어떤 배열의 begin부터 end까지(end 미포함)에 대한 얕은 복사본을 새로운 배열 객체로 반환합니다. 원본 배열은 바뀌지 않습니다.

```jsx
const animals = ["ant", "bison", "camel", "duck", "elephant"];

console.log(animals.slice(2));
// expected output: Array ["camel", "duck", "elephant"]

console.log(animals.slice(2, 4));
// expected output: Array ["camel", "duck"]

console.log(animals.slice(1, 5));
// expected output: Array ["bison", "camel", "duck", "elephant"]
```

### splice()

메서드는 배열의 기존 요소를 삭제 또는 교체하거나 새 요소를 추가

splice('추가할 위치', '삭제할 갯수', '추가할 데이터')

```jsx
const months = ["Jan", "March", "April", "June"];
months.splice(1, 0, "Feb");
// inserts at index 1
console.log(months);
// expected output: Array ["Jan", "Feb", "March", "April", "June"]

months.splice(4, 1, "May");
// replaces 1 element at index 4
console.log(months);
// expected output: Array ["Jan", "Feb", "March", "April", "May"]
```
