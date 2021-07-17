# **var, let, const 차이, 호이스팅, TDZ(Temporal Dead Zone)**

## **var**

`함수 레벨 스코프`이며, `변수의 중복 선언을 허용`한다.

다시 말해 var는 한번 선언된 변수를 다시 선언할 수 있다.

```jsx
var name = "Mike";
console.log(name); // Mike

var name = "Jane";
console.log(name); // Jane

// 전혀 문제되지 않는 모습을 확인할 수 있다.
```

또, var는 선언하기 전에 사용할 수 있다.

```jsx
// 에러를 일으키지 않는다.(신기...)
console.log(name); // undefined

var name = "Mike";
```

<br />

🤔 **그 이유는?**

- var로 선언된 모든 변수는 최상의로 끌어 올려진 것 처럼 동작한다.
- 이를 `호이스팅`이라 부른다.
- 그렇다고 실제 코드에서 이동하거나 변경되지 않는다.


```jsx
var name; // 선언

console.log(name); // undefined

name = "Mike"; // 할당
```

다만, 선언에서는 호이스팅이 되지만 할당에서는 호이스팅이 되지 않는다.

즉 이말은, name이라는 변수만 올려지는 것이고 'Mike'라는 값은 올려지지 않고 그 자리에 있게 된다.

<br />

## **let, const**

`블록 레벨 스코프`이며, `var와 달리 중복 선언이 불가능`하다.

```jsx
let name = "Mike";
console.log(name); // Mike

let name = "Jane";
console.log(name); // SyntaxError: Identifier 'name' has already been declared

// 이처럼 에러가 발생한다.
```

반면 let은 var와 달리 선언하기 전에 사용할 수 없다.

```jsx
console.log(name); // ReferenceError

let name = "Mike";
```
<br />

🤔 **그렇다면 let은 호이스팅이 발생하지 않는 것인가?**

- 정답은 아니다! 이다.
- let과 const 또한 호이스팅은 발생한다.

<br />

**⁉️ 그런데 왜 var처럼 동작하지 않고 에러를 내는 것인가?**

그것은 바로 `Temporal Dead Zone` 때문이다.

줄여서 `TDZ` 라고도 부른다.

<br />


**Temporal Dead Zone 이란?**

- const나 let 선언에서 초기화가 되지 않은 상태에서 변수에 값 사용할때 메모리에 할당되지 않은 상태를 의미한다.

```jsx
console.log(name); // Temporal Dead Zone

const name = "Mike"; // 함수 선언 및 할당

console.log(name); // 사용 가능
```

let과 const는 TDZ의 영향을 받는다.

그렇기 때문에 절대로 할당하기 전에는 사용할 수 없다.

이로 인해 var 대신 let과 const를 사용하게 되면 코드 예측을 가능하게 하고 잠재적인 버그를 줄일 수 있다고 한다.

<br />

### 그렇다면 **호이스팅은 무엇인가?**

`호이스팅`은 스코프 내부 어디에서든 변수나 함수 선언이 최상위로 선언한 것처럼 행동하는 것을 뜻한다.

<br />

**변수의 생성과정**

변수는 총 `3단계의 생성 과정`을 거친다.

1. 선언 단계
2. 초기화 단계
3. 할당 단계

<br />


**var**

`var`는 `선언과 초기화가 동시`에 일어난다.

그렇기 때문에 할당 전에 호출하면 에러를 내지 않고 `undefiend를 반환`한다.

**let**

`let`은 `선언 단계와 초기화 단계가 분리되어서 진행`된다.

호이스팅이 되면서 선언 단계가 진행되지만, 초기화 단계는 실제 초기화되는 코드에 도달했을 때만 초기화되고 할당되기 때문에 `레퍼런스 에러가 발생`한다.

**const**

`const`는 `선언 + 초기화 + 할당` 동시에 이루어져야 한다.

let과 var는 선언만 해두고 나중에 할당하는 것을 허용한다.

어떻게 보면 let과 var는 값을 바꿀 수 있기 때문에 당연한 것 같다.

```jsx
let name;
name = "Mike";

var age;
age = 30;

const gender;
gender = "male"; // SyntaxError 발생!
```

<br />

### 호이스팅은 스코프 단위로 일어난다.

**var**

`var`는 `함수 스코프(function-scoped)`이다.

함수 스코프는 함수 내에서 선언된 변수만 그 지역 변수가 되는 것을 말한다.

예를 들어서 if문 안에서 var로 선언한 변수는 밖에서도 사용이 가능하다.

```jsx
const age = 30;

if (age > 19) {
  // 하지만 let과 const는 이렇게 사용할 수 없다.
  var txt = "성인";
}

console.log(txt); // 성인
```

반면에,

```jsx
function add(num1, num2) {
  var result = num1 + num2;
}

add(2, 3);

console.log(result); // ReferenceError: result is not defined
```

이렇게 var는 함수 스코프이기 때문에 이렇게 함수 내에서 선언되면 함수 밖에서 사용할 수 없다.

var는 유일하게 벗어날 수 없는 스코프는 함수 스코프라고 생각하면 된다.

**let, const**

`let`, `const`는 `블록 스코프(block-scoped)`이다.

블록 스코프는 모든 코드 블록 내에서 선언된 변수는 코드 불록 내에서만 유효하며, 외부에서는 접근할 수 없다.

ex) 함수, if 문, for 문, while 문, try/catch 문 등

그리고 보통 `let, const는 호이스팅이 발생하지 않는다`라고 착각한다.

하지만 예제에서 let, const는 블록 스코프이며, 호이스팅이 발생하는 것을 확인할 수 있다.

```jsx
let age = 30;

// 여기서 스코프는 showAge함수 내부
function showAge() {
  console.log(age); // Temporal Dead Zone

  // 호이스팅 발생
  let age = 20; // Error!
}

showAge();
```

만약 호이스팅이 발생하지 않았다면, 함수 밖에서 선언한 age = 30이 정상적으로 출력될 것 이다.

🔎 **let, const** **공통점과 차이점?**

**공통점**

- let과 const는 블록 레벨 스코프이며, var와 달리 중복 선언이 불가능하다.

**차이점**

- let은 데이터 재활당할 때만 쓰이고, const 는 고정된 값을 선언할 때 사용한다.

<br />

## 👨🏻‍💻 간단하기 설명하자면?

- var는 함수 레벨 스코프이고 중복 선언이 가능하다.
- 반면에 const, let은 블록 레벨의 스코프이며 중복 선언이 불가능하다.

**그런데 여기서 const와 let의 차이는?**

- const는 고정된 값 즉, 상수값을 선언할 때 사용하는데, let은 고정되지 않는 값 즉, 재할당이 가능한 값을 선언할때 사용한다.

<br />

