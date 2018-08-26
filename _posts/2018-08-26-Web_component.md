---
layout: post
title: '[javascript] new Map()'
date: 2018-08-25
author: Uzihoon
comments: true
#cover: '/assets/img/hero.jpg'
tags: es6, javascript
---

##new Map()
===========

ES6에서부터 새로 도입된 데이터 구조로서 *맵(map)* 과 *셋(set)*이 있다.  

`Map`은 객체처럼 key-value 로 저장된다. 기존에 Object에는 몇가지 단점인 부분이 있었는데,  

1. Object는 프로토타입을 가지고 있음으로 프로토타입 체인으로 인해 의도치 않은 연결이 생길 수가 있다. 
2. 객체 안에 연결된 키와 값의 개수를 파악할 수 없어 계속 추적해야만 파악이 가능 하다.
3. Object의 키는 `String과` `Symbols` 밖에 될 수가 없다.
4. 객체는 순서를 보장 하지 않는다.

특히 4번인 순서를 보장 하지 않는 다는 점에서 순서를 보장시키기 위해 이전에는 id 나 key를 통해 다시 정렬을 해 주거나 배열을 쓸 수 밖에 없었다.

`Map`은 기존 `Object`의 단점인 부분들을 대부분 보완을 하고 있다.

무조건적으로 Object 대신 Map을 쓰라고 권장 하지는 않으며, 상황에 맞게 사용할것은 [MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Map) 에서는 권고하고 있다.

* 실행시 까지 키(key)를 알수 없고, 모든 키가 동일한 type이며 모든 값들이 동일한 type일 경우
* 문자열이 아닌 키가 필요한 경우
* 키-값이 변경이 자주 일어나는 경우

위의 경우는 `Map`을 사용할 것을 권하고 있으며 아래의 경우에는 Object 사용을 권장한다.

* 각 개별 요소에 대해 적용해야 하는 로직이 있는 경우

맵은 `new Map()`을 통해 생성한다.

```javascript
const a = {name: 'apple'};
const b = {name: 'blue'};

const myMap = new Map();
```

맵에 값을 저장할때는 `set`을 사용한다.

```javascript
myMap.set(a, 'fruit');
myMap.set(b, 'color');

//체인으로 연결할 수도 있다.
myMap
    .set(a, 'fruit');
    .set(b, 'color');
```

값을 불러올 때는 `get`을 사용한다.

```javascript
myMap.get(a);   //'fruit'
myMap.get(b);   //'color'
```

맵에 존재하지 않는 키에 `get`을 호출 하면 `undefined`를 반환한다.

```javascript
myMap.get(c);   //undefined
```

맵에 키가 존재하는지 확인을 하고 싶은 경우 `has()`를 사용하면 된다.

```javascript
myMap.has(a);    //true
myMap.has(c);    //false
```

맵에 이미 존재하는 키에 `set()`을 호출하면 값이 교체된다.

```javascript
myMap.set(a, 'color');
myMap.get(a)    //'color'
```

크기를 알고 싶은 경우 `size`를 통해 알 수 있다.

```javascript
myMap.size; //2
```

또한 `Map`은 이터러블 객체이므로 `for...of` 루프를 쓸 수 있다.
`keys()`는 맵의 키, `values()`는 맵의 값, `entries()`는 키와 값인 배열을 반환한다.

```javascript
const myMap = new Map();
const a = {name: 'uzi'};
const b = {name: 'hoon'};

myMap.set(a, 'firstName');
myMap.set(b, 'lastName');
for(let u of myMap.keys()) {
    console.log(u.name) //uzi hoon
}

for(let r of myMap.values()) {
    console.log(r); //firstName lastName
}

for(let ur of myMap.entries()) {
    console.log(`${ur[0]}.name: ${ur[1]}`);
}

for(let [key, value] of myMap) {
    console.log(`${key.name} : ${value}`);
}

//배열이 필요한 경우 확산 연산자를 사용하면 된다.
console.log([...myMap.values()]) //[ 'firstName', 'lastName' ]

```

또한 `Map`은 `forEach()`메소드로 순회 할 수 있다.

```javascript
myMap.forEach(function(value, key) {
    console.log(`${key.name} : ${value})
})
```



