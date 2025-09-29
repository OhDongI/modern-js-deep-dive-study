# 자바스크립트의 타입 변환 (Type Conversion)

## 1. 기본 개념

- 자바스크립트의 **모든 값**은 **타입**을 가짐
- **원시값(primitive value)**: 변경 불가능한 값 (immutable)
- **타입 변환**은 기존 원시 값을 변경하는 것이 아니라, **새로운 원시 값을 생성**
- 변환 방식은 두 가지:
    - **암묵적 타입 변환 (Implicit Coercion)**
    - **명시적 타입 변환 (Explicit Coercion)**

---

## 2. 암묵적 타입 변환 (Implicit Coercion)

> = 타입 강제 변환 (type coercion )
> 

### 개념

- **자바스크립트 엔진**이 **개발자의 의도와 무관하게** 자동으로 타입을 변환
- 변환 대상: 문자열, 숫자, 불리언 (원시 타입 중 하나)

---

### 2-1. 문자열 타입으로 변환

- **`+` 연산자** 사용 시, 하나라도 문자열이면 문자열로 변환됨
    - 문자열 연결 연산자의 모든 피연산자는 코드의 문맥상 모두 문자열 타입 → so 문자열 타입으로 암묵적 타입 변환

```jsx
1 + '2' // "12"

```

### 예시

```jsx
// 심벌 타입
(Symbol()) + ''         // TypeError: Cannot convert a Symbol value to a string

// 객체 타입
({}) + ''               // "[object Object]"
Math + ''               // "[object Math]"
[] + ''                 // ""
[10, 20] + ''           // "10,20"
(function(){}) + ''     // "function(){}"
Array + ''              // "function Array() { [native code] }"

```

---

### 2-2. 숫자로 변환

- 산술 연산자 사용 시 숫자로 변환
- 비교 연산자의 피연산자도 숫자 타입
- 숫자로 변환할 수 없으면 `NaN`

### 예시

```jsx
// 문자열 타입
+'string' // NaN

// 불리언 타입
+true // 1
+false // 0

// null 타입
+null // 0

// undefined 타입
+undefined // NaN

// 심벌 타입
+Symbol() // TypeError

// 객체 타입
// 객체와 빈 배열이 아닌 배열, undefined는 변환 x NaN
+{} // NaN
+[] // 0
+[10, 20] // NaN
+(function(){}) // NaN
```

---

### 2-3. 불리언으로 변환

- 조건문(`if`, `for`, 삼항 연산자 등)에서 자동 변환
- 자바스크립트 엔진은 조건식의 평과 결과를 불리언 타입으로 암묵적 변환
- **Falsy 값**만 false로 평가됨

### Falsy 값 목록

- `false`
- `undefined`
- `null`
- `0`, `-0`
- `NaN`
- `''` (빈 문자열)

> 나머지 값은 모두 Truthy 값 → true로 평가
> 

---

## 3. 명시적 타입 변환 (Explicit Coercion / Type Casting)

- 개발자가 **의도적으로** 타입을 바꾸는 것
- 주요 방법:
    1. **생성자 함수** (`String`, `Number`, `Boolean`) 사용
        - 표준 빌트인 생성자 함수를 new 연산자 없이 호출 방법
    2. **메서드 사용**
        - 빌트인 메서드 사용 방법
    3. **연산자 활용**
        - 암묵적 타입 변환

---

### 3-1. 문자열로 변환

### 방법 1: `String()` 함수

```jsx
// 1. String 생성자 함수를 new 연산자 없이 호출하는 방법
// 숫자 타입 => 문자열 타입
String(1);       // "1"
String(NaN);     // "NaN"
String(Infinity);// "Infinity"

//불리언 타입 => 문자열 타입
String(true);    // "true"
String(false);   // "false"
```

### 방법 2: `toString()` 메서드

```jsx
// 2. Object.prototype.toString 메서드 사용 방법
// 숫자 타입 => 문자열 타입
(1).toString();  
(NaN).toString();
(Infinity).toString();

// 불리언 타입 => 문자열 타입
(true).toString();
(false).toString();

```

### 방법 3: 문자열 연결 연산자

```jsx
// 3. 문자열 연결 연산자 이용 방법
// 숫자 타입 => 문자열 타입
1 + ''; 
NaN + '';
Infinity + '';

// 불리언 타입 => 문자열 타입
true + '';
false + '';
```

---

### 3-2. 숫자로 변환

### 방법 1: `Number()` 함수

```jsx
// 1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
// 문자열 타입 => 숫자 타입
Number('0');     // 0 
Number('-1');    // -1
Number('10.53'); // 10.53
// 불리언 타입 => 숫자 타입
Number(true);  // 1
Number(false); // 0
```

### 방법 2: `parseInt`, `parseFloat`

```jsx
// 2. parseInt, parseFloat 함수를 사용하는 방법 (문자열만 변환 가능)
// 문자열 타입 => 숫자 타입
parseInt('0'); 
parseInt('-1');
parseFloat('10.53');

```

### 방법 3: 단항 `+` 연산자

```jsx
// 3. + 단항 산술 연산자를 이용하는 방법
// 문자열 타입 => 숫자 타입
+'0';
+'-1';
+'10.53';
// 불리언 타입 => 숫자 타입
+true; 
+false;

```

### 방법 4: 곱셈  연산자

```jsx
// 4. * 산술 연산자를 이용하는 방법
// 문자열 타입 => 숫자 타입
'0' * 1;
'-1' * 1;
'10.53' * 1;
// 불리언 타입 => 숫자 타입
true * 1;
false * 1;

```

---

### 3-3. 불리언으로 변환

### 방법 1: `Boolean()` 함수

```jsx
// 1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
// 문자열 타입 => 불리언 타입 
Boolean(''); // false

// 숫자 타입 => 불리언 타입
Boolean(NaN);      // false
Boolean(Infinity); // true

// null 타입 => 불리언 타입
Boolean(null); // false

// undefined 타입 => 불리언 타입
Boolean(undefined); // false

// 객체 타입 => 불리언 타입
Boolean({}); // true
Boolean([]); // true
```

### 방법 2: `!!` 연산자 (두 번 부정)

```jsx
// 2. ! 부정 논리 연산자를 두 번 사용하는 방법
// 문자열 타입 => 불리언 타입 
!!'';

// 숫자 타입 => 불리언 타입
!!NaN;
!!Infinity

// null 타입 => 불리언 타입
!!null; 

// undefined 타입 => 불리언 타입
!!undefined;

// 객체 타입 => 불리언 타입
!!{};
!![];

```

(2번 추가 설명)

| 표현식 | 동작 설명 |
| --- | --- |
| `!value` | `value`를 먼저 **불리언으로 변환**한 뒤, **논리 부정** (즉, `true` → `false`, `false` → `true`) |
| `!!value` | 첫 번째 `!`로 부정된 값을 **다시 부정**, 즉 원래 의미의 불리언 값으로 돌려옴 |

---

## 4. 단축 평가 (Short-circuit Evaluation)

### 개념

- 논리 연산자(`&&`, `||`)는 **불리언** 값이 아닌 **원래 피연산자**를 그대로 반환
- 평가 중 결과가 결정되면 **나머지 평가 생략**

> 논리합 or 논리곱 연산자 표현식의 평가 결과는 불리언 값이 아닐 수도 있다.
논리합 or 논리곱 연산자 표현식은 언제나 2개의 피연산자 중 어느 한쪽으로 평가된다.
> 

---

### 논리곱 `&&`

- 좌항이 Falsy → 좌항 반환
- 좌항이 Truthy → 우항 반환
    - (좌항 → 우항 평가 진행)

```jsx
'Cat' && 'Dog'    // "Dog"
false && 'Dog'    // false
'Cat' && false    // false

```

---

### 논리합 `||`

- 좌항이 Truthy → 좌항 반환
- 좌항이 Falsy → 우항 반환

```jsx
'Cat' || 'Dog'    // "Cat"
false || 'Dog'    // "Dog"
'Cat' || false    // "Cat"

```

---

### 단축 평가 활용 예

### 조건이 Truthy일 때 실행 (`&&`) ⇒ if문 대체 가능

```jsx
var done = true;
var message = '';

// 주어진 조건 true
if (done) message = '완료';

// if문 단축 평가로 대체 가능
// done이 true시 message에 '완료' 할당
message = done && '완료'
console.log(message); // 완료

```

### 조건이 Falsy일 때 실행 (`||`) ⇒ if문 대체 가능

```jsx
var done = false;
var message = '';

// 주어진 조건이 false일 때
if (!done) message = '미완료';

// if문 단축 평가로 대체 가능
// done이 false면 message에 '미완료' 할당
message = done || '미완료';
console.log(message); // 미완료

```

---

### 삼항 연산자

- `if...else`문을 대체 가능

```jsx
var done = true;
var message = done ? '완료' : '미완료';

```

---

### 객체 프로퍼티 접근 시 주의

- 변수의 값이  null 또는 undefined 경우 객체의 프로퍼티 참조시 → 타입 에러 발생 (프로그램 강제 종료)

```jsx
var elem = null;

// elem이 null이나 undefined 같은 falsy값 -> elem으로 평가
// elem이 Truthy 값 -> elem.value로 평가
var value = elem && elem.value; // null (타입 에러 X)

```

---

## 5. ES11 이후 도입된 연산자

### 5-1. 옵셔널 체이닝 (`?.`)

- 좌항이 `null` 또는 `undefined`면 평가 중단 후 `undefined` 반환
    - 그렇지 않으면 우항 평가(우항 프로퍼티 참조 이어나감)
- null 또는 undefined 확인 & 프로퍼티 참조에 유용

```jsx
var elem = null;

// elem이 null 또는 undefined이면 undefined를 반환하고, 그렇징 않으면 우항의 프로퍼티 참조를 이어간다.
var value = elem?.value;
console.log(value); // undefined

```

---

### 5-2. null 병합 연산자 (`??`)

- 좌항이 `null` 또는 `undefined`일 때만 우항 반환
    - 그렇지 않으면 좌항의 피연산자 반환
- null 병합 연산자 ??는 변수에 기본값 설정시 유용

```jsx
// 좌항의 피연산자가 null 또는 undefined이면 우항의 피연산자를 반환하고,
// 그렇지 않으면 좌항의 피연산자를 반환
var foo = null ?? 'default string';
console.log(foo); // "default string"

```

> ||와의 차이: 0, '' 등은 무시하지 않음
> 

---

### 예: 함수 매개변수 기본값 설정

- 함수 호출시 인수 전달  x → 매개변수에 undefined 할당. (에러)

### ES5 방식

- `str`이 **falsy한 값**(예: `undefined`, `null`, `0`, `false`, `''`, `NaN`)이면, `''` (빈 문자열)로 대체.
- `str`이 **truthy한 값**이면 그대로 사용.

```jsx
// 딘측 평가를 사용한 매개변수의 기본값 설정
function getStringLength(str){
  str = str || '';
  return str.length;
}

getStringLength();     // 0
getStringLength('hi'); // 2  
```

### ES6 방식 (기본값 설정)

위 함수에서 `str = ''`이므로,

- `str`이 생략되거나 `undefined`이면 `''`가 기본값으로 설정됨.
- `"hi"`처럼 값을 넣으면 당연히 그 값이 사용됨.

```jsx
// ES6의 매개변수의 기본값 설정
function getStringLength(str = '') {
  return str.length;
}

getStringLength();     // 0
getStringLength('hi'); // 2
```

---

## 마무리 요약

| 변환 대상 | 암묵적 | 명시적 |
| --- | --- | --- |
| 문자열 | `+` 연결 | `String()`, `.toString()` |
| 숫자 | 산술 연산 | `Number()`, `parseInt()`, `+`, `*` |
| 불리언 | 조건식 | `Boolean()`, `!!` |

> 논리 연산자, 옵셔널 체이닝, null 병합 연산자도 타입 변환이나 평가 흐름 제어에 많이 활용됨.
>