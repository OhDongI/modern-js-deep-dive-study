# 제어문 (Control Flow Statement)

> 조건에 따라 코드 블록을 실행하거나(조건문) 반복하여 실행(반복문)할 수 있도록 흐름을 제어하는 문.
> 
- 일반적인 실행 흐름은 위 → 아래 방향.
- 제어문을 사용하면 흐름을 인위적으로 제어 가능.

---

## 1. 블록문 (Block Statement/Compound statement)

- 중괄호 `{}`로 감싸서 0개 이상의 문(statement)을 하나의 실행 단위로 묶은 것.
- **자체 종결성**을 가지며, JS는 이를 하나의 실행 단위로 처리.
- = 코드 블록, 블록

```jsx
{
  // 여기에 여러 문을 작성할 수 있음
  let a = 1;
  console.log(a);
}

```

---

## 2. 조건문 (Conditional Statement)

> 조건의 참/거짓 여부에 따라 특정 코드 블록의 실행 여부를 결정.
> 

JS의 조건문 종류:

- `if ... else`
- `switch`

---

### 2-1. if ... else 문

- 조건식이 `true`로 평가되면 해당 블록 실행
- 조건식이 `false`이면 else 블록 실행 (옵션)

```jsx
if (조건식) {
  // 조건식이 참일 때 실행
} else {
  // 조건식이 거짓일 때 실행
}

```

### else if

- 조건을 여러 단계로 분기하고 싶을 때 사용

```jsx
if (조건식1) {
  // 조건식1 참
} else if (조건식2) {
  // 조건식2 참
} else {
  // 모두 거짓일 때 실행
}

```

### 사용 가이드

- `if ... else`는 한 번만 사용 가능 (중첩은 가능하지만 가독성 저하 유의)
- `else if`는 여러 번 사용 가능

### 삼항 연산자 vs if문

| 상황 | 추천 방식 |
| --- | --- |
| 단순한 조건 분기 후 값 할당 | 삼항 연산자 |
| 복잡한 조건 분기 및 여러 문 실행 | if ... else 문 |

---

### 2-2. switch 문

> 다양한 경우(case) 중 하나에 해당하는 블록을 실행
> 

```jsx
switch (표현식) {
  case 값1:
    // 표현식 === 값1 일 때 실행
    break;
  case 값2:
    // 표현식 === 값2 일 때 실행
    break;
  default:
    // 일치하는 case가 없을 때 실행
}

```

- `break`가 없으면 **fall through** 발생: 이후 case문이 연속 실행됨
- 표현식에는 주로 문자열, 숫자 값이 사용됨
- default 문 → 선택사항

### switch문 vs if문

| 상황 | 추천 방식 |
| --- | --- |
| 다양한 상황 (case)에 따라 실행할 코드 블록 결정 | switch문 |
|  논리적 참, 거짓으로 실행할 코드 블록 결정 | if ... else 문 |

---

## 3. 반복문 (Loop Statement)

> 조건식이 참인 동안 특정 코드 블록을 반복 실행
> 

### JS의 주요 반복문

- `for`
- `while`
- `do ... while`

> 배열/객체 순회 전용:
> 
> - `forEach()` (배열)
> - `for ... in` (객체의 프로퍼티 열거)
> - `for ... of` (이터러블, ES6)

---

### 3-1. for 문

> 반복 횟수가 명확할 때 주로 사용
> 

```jsx
for (변수 선언문 또는 할당문; 조건식; 증감식) {
  조건식이 참인 경우 반복 실행될 문;
}

```

```jsx
for (var i = 0; i < 2; i++) {
  console.log(i); // 0, 1
}

```

- `초기화`, `조건식`, `증감식`은 생략 가능하지만 모두 생략 시 무한 루프 발생

---

### 3-2. while 문

> 반복 횟수가 불명확할 때 사용
> 

```jsx
while (조건식) {
  // 조건식이 참인 동안 반복
}

```

```jsx
var count = 0;

while (count < 3) {
  console.log(count); // 0, 1, 2
  count++;
}

```

### 무한 루프와 탈출

```jsx
while (true) {
  // 무한 반복
  if (조건) break; // 조건 만족 시 탈출
}

```

---

### 3-3. do ... while 문

> 코드 블록을 최소 1회 실행한 후 조건식 평가
> 

```jsx
do {
  // 최소 한 번 실행
} while (조건식);

```

```jsx
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행
do {
  console.log(count); // 0, 1, 2
  count++;
} while (count < 3);

```

---

## 4. break 문

> 레이블문, 반복문 또는 switch 문에서 코드 블록을 즉시 탈출
> 

```jsx
for (var i = 0; i < 3; i++) {
  if (i === 2) break;
  console.log(i); // 0, 1
}

```

### 레이블 문(Label Statement)

- 식별자가 붙은 문
- 중첩 반복문 탈출 시 유용 (프로그램의 실행 순서를 제어)
- 사용은 최소화 권장

```jsx
// outer라는 식별자가 붙은 레이블 for문
outer: for (var i = 0; i < 3; i++) {
  for (var j = 0; j < 3; j++) {
    // i + j === 3 이면 outer라는 식별자가 붙은 레이블 for문을 탈출
    if (i + j === 3) break outer;
    console.log(`inner [${i}, ${j}]`);
  }
}

```

---

## 5. continue 문

> 반복문의 현재 루프를 중단하고 다음 반복으로 이동(**증감식으로** 실행 흐름 이동)
> 

```jsx
for (var i = 0; i < 5; i++) {
  if (i % 2 === 0) continue;
  console.log(i); // 1, 3
}

```

### 예: 특정 문자 개수 세기

```jsx
var string = 'Hello World.';
var search = 'l';
var count = 0;

// 문자열은 유사 배열이므로 for문으로 순회 가능
for (var i = 0; i < string.length; i++) {
  // 'l'이 아니면 현 지점에서 실행을 중단하고 반복문의 증감식으로 이동
  if (string[i] !== search) continue;
  count++; // continue 문이 실행되면 이 문은 실행되지 X
}

console.log(count); // 3

```

### 참고!

- String.prototype.match 메서드 사용해도 똑같이 동작

```jsx
const result = string.match(new RegExp(search, 'g'));
console.log(result.length); // 3

```

---

## 참고 요약

| 문 | 주요 특징 |
| --- | --- |
| `if ... else` | 참/거짓에 따라 블록 실행 |
| `switch` | 다양한 값에 따라 분기 |
| `for` | 반복 횟수 명확할 때 |
| `while` | 조건에 따라 반복 (횟수 불명확) |
| `do ... while` | 코드 최소 1회 실행 후 조건 확인 |
| `break` | 블록 탈출 |
| `continue` | 다음 반복으로 이동 |

---