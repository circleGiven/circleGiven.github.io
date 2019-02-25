---
layout: post
comments: true
title: "유용한 every 와 some 함수"
date: 2019-02-22 07:32:23
description: "Array.prototype.*"
main-class: 'js'
tags: 
- "javascript"
---
# Introdution
보통 웹에서 api통신을 할 때, JSON형태의 배열을 많이 받게된다.<br/>
받은 배열을 가지고 **특정 조건에 맞는 데이터가 있는지 없는지 확인**을 할 때 자주 쓰이는 함수가 `some`과 `every`가 있다.

예제에 사용될 데이터 배열이다.
```javascript
// data object list
var fields = [
    {
      "id": 10038414,
      "name": "id",
      "alias": "id",
      "type": "LONG",
      "logicalType": "INTEGER",
      "role": "MEASURE",
      "aggrType": "NONE",
      "seq": 0,
      "biType": "MEASURE"
    },
    {
      "id": 10038415,
      "name": "activity_action",
      "alias": "activity_action",
      "type": "STRING",
      "logicalType": "STRING",
      "role": "DIMENSION",
      "aggrType": "NONE",
      "seq": 1,
      "biType": "DIMENSION"
    },
    {
      "id": 10038416,
      "name": "activity_actor",
      "alias": "activity_actor",
      "type": "STRING",
      "logicalType": "STRING",
      "role": "DIMENSION",
      "aggrType": "NONE",
      "seq": 2,
      "biType": "DIMENSION"
    },
];
```
<br/><br/>
# some
받은 데이터 중 **조건에 일치하는 데이터가 하나라도 있는지 확인**한다면 `some` 함수를 쓰면 간단하다.
일치하는 데이터가 하나라도 있다면 **true**를 반환한다.

### > syntax
```javascript
// Array.prototype.some()
array.some(function(currentValue, index, arr), thisArg)
```
<br/>
### > example
```javascript
// fields 내부에 logicalType이 INTEGER인 object가 하나라도 존재한다면
if (fields.some(field => 'INTEGER' === field.logicalType)) {
    console.log('fields에 logcialType이 INTEGER인 데이터가 존재');
}
```
<br/>

`some`함수를 사용하면서 아래와 같이 매개변수를 통해 특정 조건의 값을 찾는것도 가능하다.
```javascript
fields.some((field, index, arr) => {
    console.log(arr[index]);
    return 'INTEGER' === field.logicalType;
});
```
<br/>
### > 주의사항
`some`은 callback 함수에서 **return**이 **true**가 나오는 순간 연산이 종료되므로 주의해야한다.
```javascript
fields.some((field, index, arr) => {
    console.log(arr[index]);
    return 'INTEGER' === field.logicalType; // true가 나오면 some함수 종료
});
```
<br/>
만약 데이터가 **empty**인 상태라면 **return**은 항상 **false**가 된다.
```javascript
if ([].some(field => 'INTEGER' === field.logicalType)) {
    console.log('항상 동작하지 않는다');
}
```

<br/><br/>
# every
만약 받은 데이터 중 **조건에 일치하는 데이터가 모두 있는지 확인**한다면 `every` 함수를 쓰면 간단하다.
일치하는 데이터가 모두 해당하는 경우에만 **true**를 반환한다.

### > syntax
```javascript
// Array.prototype.every()
array.every(function(currentValue, index, arr), thisArg)
```
<br/>
### > example
```javascript
// fields 내부에 logicalType이 INTEGER인 object가 모두 존재한다면
if (fields.every(field => 'INTEGER' === field.logicalType)) {
    console.log('fields에 logcialType이 INTEGER인 데이터가 모두 존재');
}
``` 
<br/>

`every`함수를 사용하면서 아래와 같이 매개변수를 통해 특정 조건의 값을 찾는것도 가능하다.
```javascript
fields.every((field, index, arr) => {
    console.log(arr[index]);
    return 'INTEGER' === field.logicalType;
});
```
<br/>

### > 주의사항
`every`는 callback 함수에서 **return**이 **false**가 나오는 순간 연산이 종료되므로 주의해야한다.
```javascript
fields.every((field, index, arr) => {
    console.log(arr[index]);
    return 'INTEGER' === field.logicalType; // false가 나오면 every함수 종료
});
```
<br/>
만약 데이터가 **empty**인 상태라면 **return**은 항상 **true**가 된다.
```javascript
if ([].every(field => 'INTEGER' === field.logicalType)) {
    console.log('항상 동작한다');
}
```

---
## Reference
- [some 함수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/some)
- [every 함수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/every)
