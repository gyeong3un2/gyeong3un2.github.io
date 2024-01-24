---
title: "자바스크립트 객체 기초: 프로퍼티와 메서드 이해하기"
date: 2023-12-29 23:05:00 +0900
categories: [JavaScript]
tags: [Javascript, Object, Method, Property, ES6]
---

자바스크립트는 객체(Object) 기반의 프로그래밍 언어이다.  

- **원시타입**
  - 단 하나의 값
  - 변경 불가능한 값(immutable value)

- **객체 타입**
  - 다양한 타입의 값(원시 값 또는 다른 객체)을 하나의 단위로 구성한 복합적인 자료구조(data structure)
  - 변경 가능한 값(mutable value)

<br>

객체는 0개 이상의 프로퍼티로 구성된 집합이며, 프로퍼티는 키(key)와 값(value)으로 구성된다.  
```javascript
var person = {
  name: 'Lee', // 하나의 프로퍼티, name: 프로퍼티 키, 'Lee': 프로퍼티 값
  age: '20', // 하나의 프로퍼티, age: 프로퍼티 키, 20: 프로퍼티 값
}
```

<br>

프로퍼티 값이 함수일 경우, 일반 함수와 구분하기 위해 메서드(method)라 부른다.  
```javascript
var counter = {
  num: 0, // 프로퍼티
  increase: function() { // 메서드
    this.num++;
  }
}
```

- **프로퍼티**: 객체의 상태를 나타내는 **값(data)**
- **메서드**: 프로퍼티(상태 데이터)를 참조하고 조작할 수 있는 **동작(behavior)**

<br>

### **객체 리터럴에 의한 객체 생성**
C++이나 자바 같은 클래스 기반 객체 지향 언어는 **클래스를 사전에 정의**하고 **필요한 시점에 new 연산자와 함께 생성자(constructor)를 호출**하여 **인스턴스를 생성하는 방식으로 객체를 생성**한다.  
** 인스턴스: 클래스에 의해 생성되어 메모리에 저장된 실체  

**객체 리터럴**은 중괄호(`{...}`) 내에 0개 이상의 프로퍼티를 정의한다. 만약 프로퍼티가 0개라면 빈 객체가 생성된다.  

객체 리터럴은 값으로 평가되는 표현식이다. 그래서 객체 리터럴의 중괄호는 **코드블록을 의미하지 않기 때문에** 객체 리터럴의 닫는 **중괄호 뒤에는 세미콜론을 붙인다.  **

<br>

### **프로퍼티**  
**객체는 프로퍼티의 집합**이며, 프로퍼티는 키와 값으로 구성된다. 프로퍼티를 나열할 때는 쉽표(`,`)로 구분한다.  

- **프로퍼티 키**: 빈 문자열을 포함하는 모든 문자열 또는 심벌 값  
→ 프로퍼티 값에 접근할 수 있는 **식별자 역할**  
→ 식별자 네이밍을 따라야 하는 것은 아니지만, **따르지 않을 시 반드시 따옴표를 사용해야 한다.**  
`var`, `function`과 같은 예약어를 프로퍼티 키로 사용해도 에러가 발생하지 않지만, 예상치 못한 에러가 발생할 여지가 있으므로 권장하지 않는다.  

- **프로퍼티 값**: 자바스크립트에서 사용할 수 있는 모든 값

```javascript
var person = {
  firstName: 'Ung-mo', // 식별자 네이밍 규칙을 준수하는 프로퍼티 키
  'last-name': 'Lee' // 식별자 네이밍 규칙을 준수하지 않는 프로퍼티 키
};
```

<br>

### **메서드**
**프로퍼티 값이 함수**일 경우, 일반 함수와 구분하기 위해 **메서드(method)**라 부른다. 즉, 메서드는 객체에 묶여 있는 함수를 의미한다.  
```javascript
var circle = {
  radius: 5, // 프로퍼티
  
  // 원의 지름
  getDiameter: function() { // 메서드
    return 2 * this.radius;
  }
};
console.log(circle.getDiameter()); // 10
```
메서드 내부에서 사용한 **this 키워드**는 객체 자신(위 예제에서는 `circle` 객체)을 가리키는 **참조변수**다.  

<br>

### **프로퍼티 접근**
프로퍼티에 접근하는 방법은 다음과 같은 두 가지이다.  

- 마침표 프로퍼티 접근 연산자(`.`)를 사용하는 **마침표 표기법(dot notation)**
- 대괄호 프로퍼티 접근 연산자(`[...]`)를 사용하는 **대괄호 표기법(bracket notation)**
  → 대괄호 표기법을 사용하는 경우, 대괄호 프로퍼티 접근 연산자 내부에 지정하는 **프로퍼티 키는 반드시 따옴표로 감싼 문자열**이어야 한다.

```javascript
var person = {
  name: 'Lee',
};

console.log(person.name); // 올바른 표기법
console.log(person['name']); // 올바른 표기법
console.log(person[name]); // 올바르지 않는 표기법, ReferenceError: name is not defined
```

<br>

에러가 발생한 이유는 대괄호 연산자 내의 따옴표로 감싸지 않은 이름, 즉 식별자 name을 평가하기 위해 선언된 name을 찾으려고 했지만 찾지 못했기 때문이다.  

**객체에 존재하지 않는 프로퍼티에 접근하면 undefined를 반환한다. 이때 에러가 발생하지 않으니 주의하자!**

```javascript
var person = {
  name: 'Lee'
};

console.log(person.age); // undefined
```

```javascript
var person = {
  'last-name': 'Lee',
  1: 10
};

person.'last-name'; // SyntaxError: Unexpected string
person.last-name; // 브라우저 환경: NaN, Node.js 환경: ReferenceError: name is not defined

person[last-name]; // ReferenceError: last is not defined
person['last-name']; // -> Lee
```


이유는 `person.last-name`을 실행할 때, 자바스크립트 엔진은 먼저 `person.last`를 펴악한다. `person` 객체에는 `last`라는 프로퍼티가 없기 때문에 `person.last`는 `undefined`로 평가된다.  
따라서 `person.last-name`은 `undefined-name`과 같다.  

그리고 `name`이라는 식별자를 찾는다. 이때 `name`은 프로퍼티 키가 아닌 **식별자로 해석**된다.  
<br>

그리고 나서 **Node.js 환경**에서 생각해보자.  
이는 현재 어디에서 `name`이라는 식별자 선언이 없으므로 `ReferenceError: last is not defined`이라는 에러가 발생한다.  

그 다음 **브라우저 환경**에서 생각해보자.  
`name`이라는 전역 변수(전역 객체 window의 프로퍼티)가 **암묵적으로 존재**한다. 전역 변수 `name`은 창(window)의 이름을 가리키며, **기본값은 빈 문자열**이다.  
따라서 `person.last-name`은 `undefined-‘ ’` 과 같으므로 NaN이 된다.  

<br>

### **프로퍼티 값 갱신 / 동적 생성 / 삭제**

```javascript
var person = {
  name: 'Lee'
};

person.name = 'Kim'; // 객체에 이미 name 프로퍼티가 존재하므로 값이 갱신
console.log(person); // { name: 'Kim' }

---

person.age = 20; // 객체에 age 프로퍼티가 존재하지 않는다. 따라서 동적 생성 후, 값이 할당
console.log(person); // { name: 'Lee', age: 20 }

---

person.age = 20;

delete person.age; // 객체에 age 프로퍼티가 존재하므로, 삭제 가능하다.
delete person.address; // 객체에 address 프로퍼티가 존재하므로, 삭제 불가능하다. 이때 에러 발생하지 않는다.

console.log(person); // { name: 'Lee' }
```

<br>

### **ES6에서 추가된 객체 리터럴의 확장 기능**

#### **프로퍼티 축약 표현**

```javascript
// ES5
var x = 1, y = 2;
var obj = {
  x: x,
  y: y
};

// ES6
var  x = 1, y = 2;
var obj = {x, y};

console.log(obj); // { x: 1, y: 2 }
```
<br>

#### **메서드 축약 표현**

```javascript
// ES5
var obj = {
  name: 'Lee',
  sayHi: function() {
    console.log('Hi! ' + this.name);
  }
};

// ES6
const obj = {
  name: 'Lee',
  sayHi() { // 메서드 축약 표현
    console.log('Hi! ' + this.name);
  }
};

obj.sayHi(); // Hi! Lee
```

ES6의 메서드 축약 표현으로 정의한 메서드는 프로퍼티에 할당한 함수와 다르게 동작한다.