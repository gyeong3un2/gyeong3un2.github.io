---
title: "toString() vs String() 형변환의 차이"
date: 2024-03-21 14:51:00 +0900
categories: [Frontend]
tags: [Frontend, TypeScript]
---

**String()**은 `null`, `undefined`에 대해서도 잘 동작하는 반면, `.toString()`은 에러가 발생하는 것을 알 수 있다.

- **String()**: 어떤 형태이든 문자로 형변환
- **.toString()**: `null`, `undefined` 형변환 시 오류

확실히 값이 명시된 경우에는 둘 다 상관없지만, `null`, `undefined`와 같이 예외인 경우가 있을 수 있으므로 **String()**을 사용하는 것이 좋다.

<br>

## **toString()**

**자바스크립트의 내장 메서드**로, **원시 데이터 타입**에만 사용할 수 있다. 즉, `숫자`, `문자열`, `불리언`, `null`, `undefined`, `Symbol`과 같은 원시 타입에만 사용 가능하다.

객체(배열, 함수, 객체 리터럴 등)에 대해서는 **toString() 메서드**를 바로 사용할 수 없다.

```typescript
const num = 3;
const strToNum = num.toString(); // '3'

const booleanValue = true;
const strToBoolean = booleanValue.toString(); // 'true'
```

<br>

## **String()**

String()은 전역 함수(global function)로서 원시 데이터 타입 뿐만 아니라 객체를 포함한 모든 데이터 타입에 사용할 수 있다. String() 함수는 주어진 값의 문자열 표현을 반환하며, 값이 이미 문자열인 경우에도 해당 값을 그대로 반환한다.

```typescript
const num = 3;
const numToStr = num.toString(); // '3'

const booleanValue = true;
const booleanToStr = booleanValue.toString(); // 'true'

const arr = [1, 2, 3];
const arrToStr = String(arr); // '1,2,3'
```

<br>

# **참고자료**

> <https://velog.io/@kimkyeonghye/JS-String-%EA%B3%BC-.toString-%EC%B0%A8%EC%9D%B4%EC%A0%90>
>
> <https://hoontinparis.tistory.com/178>
>
> <https://velog.io/@kyjeong/Javascript-toString-vs-String>
