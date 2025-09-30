## 1. 객체란?

- 자바스크립트는 객체(object) 기반 프로그래밍 언어.
- **모든 값은 객체** (단, 원시 값을 제외한 모든 값).
- 함수, 배열, 정규표현식 등도 객체.

### 🔹 원시 타입

- 단 하나의 값만 표현
- **변경 불가능한 값 (immutable)**

### 🔹 객체 타입

- 다양한 값을 하나의 단위로 구성한 복합 자료구조
- **변경 가능한 값 (mutable)**

---

## 2. 객체의 구성

```jsx
var person = {
  name: 'Oh',  // key: value
  age: 22
};

```

- **객체 = 프로퍼티(속성) + 메서드(동작)**
- 프로퍼티: 객체의 상태 (key: value)
- 메서드: 프로퍼티를 참조하거나 조작하는 함수
    - 프로퍼티: 객체의 상태를 나타내는 값 (**data**)
    - 메서드: 프로퍼티를 참조하고 조작할 수 있는 동작 (**behavior**)

```jsx
var counter = {
  num: 0,                    // 프로퍼티
  increase: function() {     // 메서드
    this.num++;
  }
};

```

---

## 3. 객체 생성 방법

| 분류 | 클래스 기반 | 프로토타입 기반 |
| --- | --- | --- |
| 언어 | C++, Java | JavaScript |
| 방식 | 클래스 정의 → 인스턴스 생성 | 다양한 방식 가능 (아래 참고) |

### 자바스크립트의 객체 생성 방법

1. 객체 리터럴 (가장 일반적)
2. `Object` 생성자 함수
3. 생성자 함수
4. `Object.create()` 메서드
5. 클래스 (ES6)

### 객체 리터럴 예시

- 중괄호({…}) 내에 0개 이상의 프로퍼티 정의
- **변수 할당되는 시점에** 자바스크립트 엔진은 객체 리터럴 해석 후 **객체 생성**
- 객체 리터럴 = 객체를 생성하기 위한 표기법
    - 리터럴 = 사람이 이해할 수 있는 문자 또는 약속된 기호를 사용하여 값을 생성하는 표기법

```jsx
// 중괄호 내에 프로퍼티 정의 x -> 빈 객체 생성
var empty = {}; // 빈 객체 
console.log(typeof empty); // "object"

```

---

## 4. 프로퍼티

- **프로퍼티 = 키(key) + 값(value)**
- 키: 문자열 또는 심벌 (식별자 네이밍 규칙 준수 권장)
- 값: 자바스크립트의 모든 값 사용 가능

```jsx
var person = {
  firstName: 'Ung-mo',   // 식별자 네이밍 규칙 O
  'last-name': 'Lee'     // 규칙 X → 따옴표 필요
};

```

### 동적 프로퍼티 생성

```jsx
var obj = {};
var key = 'hello';
obj[key] = 'world';

console.log(obj); // { hello: "world" }

```

- 계산된 프로퍼티 이름 (computed property): `[key]` 사용

---

## 5. 메서드

- 객체의 프로퍼티 중 값이 함수인 것
- 함수도 값이기 때문에 프로퍼티에 할당 가능

```jsx
var obj = {
  sayHi: function() {
    console.log('Hi');
  }
};

```

---

## 6. 프로퍼티 접근 방법

### 1. 마침표 표기법 (`.`) - (dot notation)

```jsx
var person = {
  name: 'Oh'
};

// 마침표 표기법에 의한 프로퍼티 접근
console.log(person.name); // Oh

```

### 2. 대괄호 표기법 (`[ ]`) - (bracket notation)

- 반드시 따옴표로 감싸기 → 그렇지 않으면 식별자로 인식
    - 단, 프로퍼티 키가 숫자로 이뤄진 문자열 → 따옴표 생략 가능

```jsx
person['name'] // "Oh"

```

**대괄호 표기법 사용해야 하는 경우**

- 프로퍼티 키가 네이밍 규칙을 따르지 않을 때
- 프로퍼티 키가 변수로 동적일 때

```jsx
person['last-name'] // 가능
person.last-name // 오류 or 의도치 않은 결과

```

**주의:**

```jsx
person[1]     // 숫자 → 문자열로 변환되어 "1" 키로 접근
person['1']   // 동일 결과

```

```jsx
var person = {
  'last-name': 'Lee',
  1: 10
};

person.'last-name';  // SyntaxError: Unexpected string
person.last-name;    // 브라우저 환경: NaN
                     // Node.js 환경: ReferenceError: name is not defined
person[last-name];   // ReferenceError: last is not defined
person['last-name']; // Lee

// 프로퍼티 키가 숫자로 이뤄진 문자열인 경우 따옴표를 생략할 수 있다.
person.1    // SyntaxError: Unexpected number
person.'1'; // SyntaxError: Unexpected string
person[1];  // 10 : person[1] -> person['1']
person['1'] // 10
```

<aside>
💁🏻‍♂️

`person.last-name;` 표현식의 실행 결과가 **Node.js**와 **브라우저 환경**에서 다른 이유는 자바스크립트의 평가 방식과 전역 객체의 차이 때문이다. 이 표현식은 자바스크립트 엔진에 의해 `(person.last) - (name)`으로 해석되며, 먼저 `person.last`를 평가한다. 만약 `person` 객체에 `last`라는 프로퍼티가 없다면 이는 `undefined`로 평가된다. 이후 `name`이라는 식별자를 찾는데, Node.js 환경에서는 `name`이 어디에도 선언되어 있지 않기 때문에 `ReferenceError: name is not defined`가 발생한다. 반면 브라우저 환경에서는 `name`이 전역 객체인 `window`의 기본 프로퍼티로 존재하며, 이는 보통 빈 문자열 `""`로 설정되어 있다. 따라서 브라우저에서는 `person.last - name`이 `undefined - ""`로 평가되고, 이 결과는 `NaN`이 된다.

</aside>

---

## 7. 프로퍼티 값 갱신

- 존재하는 프로퍼티에 새로운 값을 할당하면 갱신됨

```jsx
var person = { name: 'Lee' };
person.name = 'Oh';

console.log(person); // {name: "Oh"}

```

---

## 8. 프로퍼티 동적 생성

- 존재하지 않는 프로퍼티에 값을 할당하면 새로 생성됨

```jsx
var person = {
  name: 'Lee'
};

person.age = 20;

console.log(person); // {name: "Lee", age: 20}

```

---

## 9. 프로퍼티 삭제

- `delete` 연산자 사용

```jsx
delete person.age;

```

- 존재하지 않는 프로퍼티를 삭제해도 에러 없음

---

## 10. ES6 객체 리터럴 확장 기능

### 10-1. **프로퍼티 축약 표현**

변수명 = 프로퍼티 키로 사용할 경우 축약 가능

```jsx
// ES5
var x = 1, y = 2;
 
var obj = {
  x: x,
  y: y
};

console.log(obj); // {x: 1,  y: 2}
```

```jsx
// ES6
let x = 1, y = 2;

// 프로퍼티 축약 표현
const obj = { x, y };

console.log(obj); // {x: 1, y: 2}

```

### 10-2. **계산된 프로퍼티 이름** (computed property name)

> 문자열 또는 문자열로 변환할 수 있는 값으로 평가되는 표현식을 사용해 프로퍼티 키를 동적으로 생성하는 것
> 

객체 리터럴 내부에서 대괄호를 사용하여 키를 동적으로 생성

```jsx
// ES5
var prefix = 'prop';
var i = 0;

var obj = {};

// 계산된 프로퍼티 이름으로 프로퍼티 키 동적 생성
obj[prefix + '-' + ++i] = i;
obj[prefix + '-' + ++i] = i;
obj[prefix + '-' + ++i] = I;

console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
```

```jsx
// ES6
const prefix = 'prop';
let i = 0;

// 객체 리터럴 내부에서 계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성
const obj = {
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i
};

console.log(obj); // { prop-1: 1, prop-2: 2, prop-3: 3 }

```

### 10-3. **메서드 축약 표현**

```jsx
const obj = {
  name: 'Oh',
  // 메서드 축약 표현
  sayHi() {
    console.log('Hi ' + this.name);
  }
};

obj.sayHi(); // Hi! Oh
```

- `function` 키워드 생략 가능
- 일반 함수와는 동작 차이 있음 (26장 “메서드”에서 살펴볼 것)

---

## 11. 요약

| 항목 | 설명 |
| --- | --- |
| 객체 | 상태(프로퍼티)와 동작(메서드)의 집합 |
| 프로퍼티 | 키와 값의 쌍 |
| 메서드 | 프로퍼티 값이 함수인 것 |
| 생성 방식 | 객체 리터럴, 생성자 함수, 클래스 등 다양 |
| 접근 방식 | `.` 또는 `[]` 사용 |
| 동적 생성/삭제 | 가능 |
| ES6 확장 | 축약 표현, 계산된 프로퍼티, 메서드 축약 등 제공 |

