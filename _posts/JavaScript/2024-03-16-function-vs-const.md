---
title: "함수 컴포넌트, 선언문 vs 표현식"
date: 2024-03-16 23:21:00 +0900
categories: [JavaScript]
tags: [javascript, const, function]
---

```javascript
// 함수 선언문
function fn() {}

// 함수 표현식
const fn = () => {}
```

# **선언문 vs 표현식**

- 호이스팅 여부
- export default를 선언과 동시에 할 수 있는가?

이 두가지 차이는 모두 좀 더 깔끔한 코드를 지향할 때 문제가 될 수 있다.  

## **호이스팅**

- **호이스팅**이란, 함수 안에 있는 선언들을 모두 끌어올려서 해당 함수 유효 범위의 최상단에 선언하는 것을 말한다.

```javascript
/* 
* 위에서 언급했던 것과 같이, const 형태의 표현식을 선언하면 호이스팅을 지원하지 않기 떄문에
* 선언을 위해서는 맨 하단에 선언해야 한다.
*/

const tryDoTheThing = () => {
  console.log(`This is me trying to be awesome ${getAwesome()}`);
}

// "getAwesome() is not defined" because it is referenced too early
tryDoTheThing(); 

const getAwesome = () => (+((Math.random() * 10000).toString().split('.')[0]));

const doTheThing = () => {
  console.log(`This is awesome! ${getAwesome()}`);
}

doTheThing(); // print
```

<br>

```javascript
/* 
* 위와는 다르게 function을 이용하면, 호이스팅이 적용되어 코드의 위치와는 상관없이 선언이 가능하다
*/

doTheThing();

function doTheThing() {
  console.log(`This is awesome number ${getAwesome()}`);
}

function getAwesome() {
  return (+((Math.random() * 10000).toString().split('.')[0]));
}

```

- **호이스팅 대상**
  - `var` 변수 선언과 함수 선언문(`function`)에서만 호이스팅이 일어난다.
    - var 변수/함수 선언만 위로 끌어올려지며, 할당은 끌어올려지지 않는다.
    - let/const는 호이스팅이 발생하기는 하지만, TDZ 문제가 발생한다.

  > **TDZ(Temporal Dead Zone)란?**  
    TDZ는 변수 선언(호이스팅에 의해 스코프 상단으로 끌어올려진 부분) 후, 변수가 할당되기 전 부분이다. 선언은 되어 있지만, 할당이 되어 있지 않으므로 임시적으로 죽어있는 구간이라고 이해하면 된다.  
    초기화되기 전에 변수에 접근하려고 한다면, TDZ에 의해서 에러가 발생하게 된다.
  {: .prompt-info }

  <br>

  ```javascript
  /*
  * var 변수 vs let/const 변수
  */

  var myname = 'HEEE'; // var 변수
  let myname2 = 'HEEE2'; // let 변수
  ```

  ```javascript
  /*
  * 함수 선언문 vs 함수 표현식
  */

  foo();
  foo2();

  function foo() { // 함수 선언문
    console.log('Hello');
  }

  var foo2 = function() { // 함수 표현식
    console.log('Hello2');
  }

  ```

  - 함수 선언문일 경우, 함수 호이스팅이 가능해 선언부를 모두 모듈 하단에 내려놓고, 메인 로직만 상단에 배치함으로써 가독성을 높일 수 있다.
  - **TDZ**는 표현식에서 항상 존재할 수 있는 이슈이다.

<br>

## **export default를 선언과 동시에 할 수 있는가?**

```javascript
// ✅ 선언문은 함수 선언과 export default를 동시에 할 수 있다.
export default function Fn() {}

// ⛔️ 표현식은 불가능하다.
export default const Fn = () => {}

// ✅ named export는 가능하다.
export const Fn = () => {}
```

- 함수 선언과 export default를 동시에 한다는 것은, default로 내보내는 함수는 그 모듈의 메인 로직일 것이고, 이는 코드를 보는 사람으로 하여금 가장 중요한 로직이 무엇인지 인지시킬 수 있다.
- 표현식을 지지하는 사람의 경우 *"가장 중요한 메인 로직을 맨 위에 두면 똑같은 거 아니냐"*고 할 수 있다. 이는 먼저 언급한 호이스팅 이슈 (TDZ)가 발생한다면 문제의 여지가 있다.

<br>

## 결과적으로 호이스팅을 지원하는 **function**을 더 선호한다고 한다.

<br>

# **참고자료**
> <https://developer0809.tistory.com/102>  
> 
> <https://softwareengineering.stackexchange.com/questions/364086/why-use-const-foo-instead-of-function-foo>
> 
> <https://velog.io/@jjunyjjuny/React-%ED%95%A8%EC%88%98-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-%EC%84%A0%EC%96%B8%EB%AC%B8-vs-%ED%91%9C%ED%98%84%EC%8B%9D%EC%9D%80-%EC%B7%A8%ED%96%A5-%EC%B0%A8%EC%9D%B4%EC%9D%BC%EA%B9%8C>   
> 
> <https://gmlwjd9405.github.io/2019/04/22/javascript-hoisting.html>  
> 
> <https://kimbangg.tistory.com/107>  
> 