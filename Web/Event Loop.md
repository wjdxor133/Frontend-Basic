## 들어가기에 앞서,

### 자바스크립트 도입 Before / After

- 자바스크립트 도입 이전의 웹 사이트는 일반적으로 \*\*\*\*`HTML`, `CSS` 그리고 `정적 데이터`로만 이루어졌었다.
- 시간이 지나 **자바스크립트 도입** 이후 현재 웹 사이트는 사용자의 경험을 향상 시키고, 보다 역동적이고 인터랙티브한 웹 사이트로 발전하게 되었다.
- 그리고 더이상 정적 데이터를 가지고 화면에 보여주는 것이 아니라, 외부 네트워크(API)를 호출하고 반환된 데이터를 가지고 화면에 보여주게 되었다.
- 하지만 사용자와 데이터가 점점 많아지고 데이터 통신도 복잡해지면서 웹 사이트의 성능에 대한 이슈에 대해 많은 고민을 해야하는 시기이기도 하다.
- 즉, 자바스크립트를 가지고 웹을 만드는 개발자들은 필수적으로 브라우저의 동작 원리에 대해 이해하려고 노력해야 한다.

## 그렇다면 자바스크립트는 어떻게 동작하는 것인가?

- 자바스크립트는 `싱글 스레드` 혹은 `동기 프로그래밍 모델`이다.
- 즉 이말은 `한 번에 하나의 작업만을 수행할 수 있다는 뜻`이다.

```jsx
console.log(1);
console.log(2);
console.log(hello());
console.log(4);

function hello() {
  console.log(3);
}
```

- 예제를 보면 코드는 첫번째 줄부터 순서대로 실행할 것이다.
- 더 자세히 실행되는 과정을 살펴보면,
- 자바스크립트에는 call stack이라는 곳이 존재하는데, 그 곳에 실행문들이 순차적으로 쌓인다.

![이벤트루프 1](https://user-images.githubusercontent.com/47416686/126345926-3be57447-6f62-497b-ab14-6a7e3fc07a92.gif)

### 여기서 Call Stack이란?

- 현재 실행중인 명령문에 대한 어떤 순서로 작업을 수행하는지 기록하는 데이터 구조를 말한다.
- Call Stack은 "Last In, First Out" `LIFO` 구조로, push된 마지막 요소가 가장 먼저 pop을 한다.

```jsx
function fun1() {
  console.log("inside 1");
}

function fun2() {
  fun1();
}

function fun3() {
  fun2();
}

fun3();
```

![이벤트루프 2](https://user-images.githubusercontent.com/47416686/126345932-b3f1e602-84e1-4e18-8dc7-361adf234fa9.gif)

- 자바스크립트는 이렇게 싱글 스레드 언어이기 때문에 함수를 실행하면 함수 호출이 스택에 순차적으로 쌓이고 스택의 맨 위에서부터 차례대로 한 번에 하나의 함수만 처리할 수 있다.

- 순차적으로 잘 실행하다가 세번째 줄에서 함수 호출이 일어나면서 네번째 줄의 작업이 함수가 반환 될 때까지 실행되지 않는 것을 볼수 있다.
- 이러한 현상을 `블로킹(Blocking`이라고도 한다.
- 블로킹의 의미는 `어떠한 작업이 완료될때까지 기다려야하는 상황`이라고 보면 된다.
- 이렇게, 자바스크립트는 `싱글 스레드 언어(Single Threaded language)`이기 때문에 예제 코드가 순서대로 실행되고 있는 것을 확인할 수 있다.

## 그렇다면 웹에서도 자바스크립트는 순서대로 실행하는가?

- 여기에 대한 답변은 **Yes!**
- 우선 자바스크립트는 싱글 스레드 언어이기 때문에 순서대로 작업을 실행할 것이다.
- 극단적인 예시로 웹 사이트에서 어떠한 동작(Event) 하나가 30초 이상이 걸린다고 상상해보자.
- 사용자들은 아무도 그 사이트를 이용하지 않을 것이다.
- 하지만 실제로 우리가 이용하는 웹 사이트에서는 순서대로 작업을 수행하는 것이 아닌 동시에 여러 작업을 수행하는 것을 볼수 있다.
- 자바스크립트를 쓰면서 동시에 작업을 처리할 수 있었던 이유는 바로 **브라우저** 때문이다.
- 즉, 자바스크립트 언어 자체에서 비동기 동작을 지원하는 것이 아니라 브라우저에서 동시에 동작을 할수 있게 비동기 처리를 해주는 것이다.

### 브라우저는 어떻게 비동기 처리를 해주는가?

우선 브라우저는 `Web APIs`, `Callback Queue` , `Event Loop` 등으로 구성되어 있다.

![이벤트 루프 3](https://user-images.githubusercontent.com/47416686/126345907-6ca80eff-9f88-45ee-b290-bc6e35e8f04e.png)

---

스터리 올릴 부분

## 이벤트 루프란?

- `**Call Stack**`에 작업이 비어있는지 확인하고, `**Callback Queue**`에 쌓여있는 작업들을 순서대로 `**Call Stack**`에 옮겨주는 아이라고 생각하면 된다.
- 하지만 이벤트 루프를 이해하기 위해서는 먼저 자바스크립트가 브라우저에서 어떻게 동작하는지 알아야한다.

### 자바스크립트는 어떻게 동작하는가?

- 자바스크립트는 `**싱글 스레드 언어**` 혹은 `**동기 프로그래밍 모델**`이다.
- 즉 이말은 자바스크립트는 `**한 번에 하나의 작업만을 수행할 수 있다는 뜻**`이다.

```jsx
// 자바스크립트 동작 예제
console.log(1);
console.log(2);
console.log(hello());
console.log(4);

function hello() {
  console.log(3);
}
```

- 예제를 보면 코드에서 첫번째 줄부터 순서대로 `**Call Stack**`에 쌓여 실행할 것이다.
- 여기서 Call Stack은 `**현재 실행중인 명령문에 대한 어떤 순서로 작업을 수행하는지 기록하는 데이터 구조**`를 말한다.

![이벤트 루프 4](https://user-images.githubusercontent.com/47416686/126345911-3e77437f-1ff4-4cb6-8b24-eaab411b0336.gif)

- 하지만 순차적으로 잘 실행하다가 세번째 줄에서 함수 호출이 일어나면서 네번째 줄의 작업이 함수가 반환 될 때까지 실행되지 않는 것을 볼수 있다.
- 이것은 하나의 한 작업만을 수행하는 동기 프로그래밍이 가지고 있는 가장 큰 특징이며, 이러한 현상을 `**블로킹(Blocking)**`이라고도 한다.
- 블로킹을 간단하게 말하면 `**어떠한 작업이 완료될때까지 기다려야하는 상황**`이라고 보면 된다.
- 예를 들어, 이커머스 웹 사이트에서 결제하기 버튼 동작 하나 처리하는데 1분 이상이 걸린다고 상상해보자.
- 로딩창이 1분 동안 뜨면서 다른 작업을 할 수 없게 된다.
- 블로킹은 마치 이러한 현상과 같다고 보면 된다.

### 그렇다면 블로킹 현상 어떻게 해결?

- 자바스크립트는 분명 싱글 스레드 언어이기 때문에 모든 작업이 순차적으로 진행하여 블로킹 현상을 피할 수 없다.
- 하지만 기존의 자바스크립트로 만들어진 웹 사이트를 보면 순서대로 작업을 수행하는 것이 아닌 동시에 여러 작업을 수행하는 것을 볼수 있다.
- 그 이유는 바로 `**브라우저**` 때문이다.
- 즉, 자바스크립트 언어 자체에서 비동기 동작을 지원하는 것이 아니라 브라우저에서 동시에 동작을 할수 있게 `**비동기 처리**`를 해주는 것이다.

### 브라우저는 어떻게 비동기 처리를 해주는가?

- 우선 브라우저에는 `**Web APIs**`, `**Callback Queue**`, `**Event Loop**` 등으로 구성되어 있

![이벤트 루프 5](https://user-images.githubusercontent.com/47416686/126345919-e7568b88-f094-4b06-8863-d0a1567f01d8.png)

```jsx
console.log("first");

setTimeout(function cb() {
  console.log("second");
}, 1000); // 1초 뒤 실행

console.log("third");
```

**위 코드가** **브라우저에서** **동작하는 원리**

1. console.log('first'); `**Call Stack**`에 push되고 'first'가 출력된 후 pop된다.
2. setTimeout은 브라우저에 의해 제공된 API이기 때문에 자바스크립트 엔진에서 처리하지 않는다.
3. setTimeout 함수가 `**Call Stack**`에 쌓이자마자 그 안에 있던 콜백 함수 cd()가 바로 `**web Apis**`로 넘겨진다.
4. 그러고 바로 console.log('third'); `**Call Stack**`에 push되고 'third'가 출력된 후 pop된다.
5. 이제 코드가 모두 실행되었으므로 `**Call Stack**`은 비어지게 되고, `**web Apis**`에 있던 cd()는 1초 뒤에 `**Callback Queue**`로 옮겨진다.
6. 이때 바로 `**Event Loop**`가 `**Call Stack**`이 비어지는지와 `**Callback Queue**`에 쌓여있는 작업들을 확인해서 순차적으로 스택에 작업물을 push한다.
7. 현재 스택이 비어있고, `**Callback Queue**`에 cd()가 있기 때문에 `**Event Loop**`가 `**Call Stack**`에 cd()를 push하고 console.log('second');가 실행하고 'second'가 출력된 후 pop된다.

![이벤트 루프 6](https://user-images.githubusercontent.com/47416686/126345921-6f782d68-ab40-43e2-8781-fd2a468bf9b7.gif)

- 즉, 브라우저에서 자바스크립트는 이렇게 작동한다.
- 함수를 동기 호출하면 `**Call Stack**`에 차곡차곡 쌓여 순차적으로 실행된다.
- 이때 만약에 AJAX나 setTimeout() 혹은 DOM Event 함수를 실행하면, 자바스크립트 엔진은 `**Call Stack**`에서 `**web Apis**`로 보내고 정해진 시간 혹은 이벤트가 발생한 순간에 순차적으로 `**Callback Queue**`에 적재된다.
- `**Callback Queue**` 에 줄을 선 작업들은 `**Call Stack**` 에 쌓여있는 작업들이 모두 실행되어 없어지면, 이때 `**Event Loop**`가 확인해서 `**Call Stack**`에 순서대로 보내진다.
- 차례대로 `**Call Stack**`에 쌓여서 실행된다.

## 📌 **Event Loop 정의**

Event Loop의 역할은 간단합니다.

1. **`Call Stack`**과 **`Callback Queue`**를 감시합니다.

2. Call Stack이 `**비어있을 경우**`, Callback queue에서 함수를 꺼내 Call Stack에 추가 합니다.

## ✔️ 참고

[](http://latentflip.com/loupe/?code=dmFyIGEgPSAxMDsKdmFyIGIgPSAxMDsKdmFyIGMgPSAyMDsKY29uc29sZS5sb2coc3VtKGEsYikpOwpjb25zb2xlLmxvZyhjKTsKCmZ1bmN0aW9uIHN1bShhLGIpIHsKICAgIHJldHVybiBhICsgYjsKfQ%3D%3D!!!PGJ1dHRvbj5DbGljayBtZSE8L2J1dHRvbj4%3D)

[[JS/Event Loop] 자바스크립트, 이벤트 루프(Event Loop)와 동시성(concurrency)에 대하여](https://im-developer.tistory.com/113)

[JavaScript 비동기 핵심 Event Loop 정리](https://medium.com/sjk5766/javascript-%EB%B9%84%EB%8F%99%EA%B8%B0-%ED%95%B5%EC%8B%AC-event-loop-%EC%A0%95%EB%A6%AC-422eb29231a8)

[Everything You Need to Know About Event Loop in JavaScript](https://blog.usejournal.com/everything-you-need-to-know-about-event-loop-in-javascript-1f14f94e5ab6)
