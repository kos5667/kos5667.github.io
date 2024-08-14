---
layout: post
title: "Javascript의 비동기 처리에 대한 이론"
date: 2024-08-14 11:44:00 +0900
excerpt_image: "../assets/images/excerpt-2024-08-14-theory-of-async-processing-of-javascript.png"
categories: javascript
tags: [nodejs, javascript, async, await, cs]
---

![](/assets/images/2024-08-14-theory-of-async-processing-of-javascript1.png)
Javascript의 비동기 처리에서 핵심적인 역할을 하는 **Event Loop**는 Javascript의 동시성(concurrency)을 관리하는 메커니즘입니다. Event Loop는 Javascript가 Single-Threaded 언어임에도 불구하고, 비동기 작업을 효율적으로 처리할 수 있도록 도와줍니다.

## 비동기(Asynchronous) 란?

비동기란 둘 이상의 객체 또는 이벤트가 동시에 존재하지 않거나 발생하지 않는 경우(또는 이전 객체 또는 이벤트가 완료될 때까지 기다리지 않고 발생하는 여러 관련 작업)라고 정의합니다.

**동기(Synchronous: 동시에 일어나는)**

- **정의**: 작업이 순차적으로 진행되며, 하나의 작업이 끝나야 다음 작업이 시작되는 방식입니다.
- **예시**: 전화할 때, 한 사람이 말을 끝내야 다른 사람이 말할 수 있는 상황.

**비동기(Asynchronous: 동시에 일어나지 않는)**

- **정의**: 작업이 독립적으로 진행되며, 어떤 작업이 완료될 때까지 기다리지 않고 다음 작업을 바로 시작하는 방식입니다.
- **예시**: 이메일을 보내는 것처럼, 메일을 보내놓고 답장을 기다리면서 다른 일을 할 수 있는 상황.

**블록킹(Blocking)**

- **정의**: 어떤 작업이 완료될 때까지 프로그램의 실행이 멈추는 상태를 의미합니다. 다음 작업은 현재 작업이 끝나야만 진행됩니다.
- **예시**: 파일을 읽을 때, 파일이 모두 읽혀야 다음 줄의 코드가 실행되는 상황.

**논-블록킹(Non-Blocking)**

- **정의**: 작업이 완료되지 않아도 프로그램의 실행이 멈추지 않고, 다른 작업을 계속해서 진행할 수 있는 상태를 의미합니다.
- **예시**: 파일을 읽으면서도 다른 작업을 동시에 수행할 수 있는 상황, 파일 읽기가 완료되면 그때 결과를 처리함.

### Javascript가 비동기 작업을 처리하는 방법(feat. Web API)

Javascript는 비동기 작업을 처리할 때 사용하는 브라우저의 API는 Web API라고 불리며, Web API는 다양한 API들의 집합입니다. Web API는 브라우저에서 제공하는 기능으로, Javascript가 비동기적으로 처리해야 하는 작업을 수행할 수 있도록 도와줍니다.

### Web API의 종류

1. **타이머 API**
    - **`setTimeout`**: 특정 시간(밀리초) 후에 콜백 함수를 실행합니다. 비동기적으로 코드를 실행할 때 가장 흔히 사용하는 방법입니다.
    - **`setInterval`**: 지정된 시간 간격으로 반복적으로 콜백 함수를 실행합니다. 이 역시 비동기적으로 동작합니다.

   ```javascript
   setTimeout(() => {
       console.log('This runs after 1 second');
   }, 1000);
   ```

2. **XHR (XMLHttpRequest) 및 Fetch API**
    - **`XMLHttpRequest (XHR)`**: 서버와 상호작용할 때 사용하는 API로, 비동기적으로 데이터를 주고받을 수 있습니다. 주로 Ajax 요청을 보낼 때 사용됩니다.
    - **`Fetch API**:` XHR의 대안으로, 프로미스(Promise)를 기반으로 한 API입니다. 네트워크 요청을 보내고, 서버로부터 응답을 비동기적으로 받을 수 있습니다.

   ```javascript
   fetch('https://api.example.com/data')
       .then(response => response.json())
       .then(data => console.log(data));
   ```

3. **DOM 이벤트**
    - **`addEventListener`**: DOM 요소에 이벤트 리스너를 추가하여 사용자의 상호작용(클릭, 키보드 입력 등)에 반응할 수 있습니다. 이 역시 비동기적으로 동작합니다.

   ```javascript
   document.getElementById('myButton').addEventListener('click', () => {
       console.log('Button clicked');
   });
   ```

4. **Promise 및 Async/Await**
    - **`Promise`**: 비동기 작업의 완료 또는 실패를 나타내는 객체입니다. `then`, `catch`, `finally` 메서드를 사용하여 비동기 작업을 처리할 수 있습니다.
    - **`Async/Await`**: Promise를 좀 더 읽기 쉬운 방식으로 사용할 수 있도록 도와주는 문법입니다.

   ```javascript
   async function fetchData() {
       const response = await fetch('https://api.example.com/data');
       const data = await response.json();
       console.log(data);
   }
   ```

5. **Web Workers**
    - **`Web Workers`**: 자바스크립트에서 백그라운드 스레드를 사용하여 비동기 작업을 수행할 수 있도록 하는 API입니다. CPU 집약적인 작업을 메인 스레드에서 분리하여 UI가 중단되지 않도록 할 수 있습니다.

   ```javascript
   const worker = new Worker('worker.js');
   worker.postMessage('Start task');
   worker.onmessage = function(event) {
       console.log('Worker said: ', event.data);
   };
   ```

6. **WebSocket**
    - **`WebSocket API`**: 서버와의 양방향 통신을 지원하는 API입니다. 클라이언트와 서버 간의 지속적인 연결을 유지하며 실시간 데이터를 주고받을 수 있습니다

   ```javascript
   const socket = new WebSocket('wss://example.com/socket');
   socket.onmessage = (event) => {
       console.log('Message from server ', event.data);
   };
   ```

### **Node.js는 비동기 작업을 어떻게 처리할까?**

Node.js는 서버 측에서 자바스크립트를 실행하는 런타임 환경이며, 브라우저와는 다른 환경이기 때문에, Web API 대신 Node.js의 내부 모듈과 C++로 구현된 라이브러리를 사용하여 비동기 작업을 처리합니다.

<aside>
💡 <strong>Node.js가 비동기를 처리하는 방법</strong>

- **Node.js**에서는 비동기 작업을 처리하기 위해 **Node.js API**를 사용하며, **Web API**를 사용하지 않습니다.
- Node.js는 **libuv**라는 라이브러리를 통해 비동기 I/O 작업을 관리하며, 이를 통해 이벤트 루프에서 작업을 처리하고, 작업이 완료되면 콜백 함수를 실행합니다.
- Node.js의 비동기 API는 브라우저 환경에서의 Web API와 유사한 역할을 하지만, 서버 측 작업에 최적화되어 있습니다.
</aside>

## Event Loop란?

- **Single-Threaded**: Javascript는 한 번에 하나의 작업만 처리할 수 있는 Single-Threaded 언어입니다. 하지만 비동기 작업(I/O 작업, 타이머, HTTP 요청 등)을 통해 Main-Threaded가 Blocking되지 않고 다른 작업을 처리할 수 있도록 합니다.
- **Call Stack**: Javascript Engine은 함수 호출을 관리하기 위해 Call Stack을 사용합니다. 함수가 호출되면 Call Stack에 쌓이고, 함수가 완료되면 Call Stack에서 제거됩니다.
- **Event Queue**: 비동기 작업이 완료된 후 실행될 Callback 함수들은 Event Queue에 들어갑니다. Event Queue는 대기 중인 함수들의 목록을 가지고 있으며, Call Stack이 비어 있을 때 Event Queue에 있는 함수들이 실행됩니다.

### Event Loop의 동장 방식

1. **Call Stack 검사**: Event Loop는 Call Stack이 비어 있는지 확인합니다.
2. **Event Queue 검사**: Call Stack이 비어 있다면, Event Queue에서 첫 번째 Callback 함수를 Call Stack으로 가져와 실행합니다.
3. **비동기 작업 처리**: 비동기 작업이 완료되면 해당 Callback 함수가 Event Queue에 들어가게 되고, Event Loop가 이 함수를 실행하기 위해 대기합니다.
4. **반복**: 이 과정이 계속해서 반복됩니다. Call Stack이 비어 있을 때마다 Event Queue에 있는 함수들이 하나씩 실행됩니다.

### 실행 순서 예시
![](/assets/images/2024-08-14-theory-of-async-processing-of-javascript2.png)

```javascript
console.log('Start');

setTimeout(() => {
    console.log('Timeout callback');
}, 0);

console.log('End');
```

1. console.log('Start') 가 호출되고, Call Stack에 들어가 실행됩니다. 콘솔에 “Start”가 출력되고, 함수가 종료 되면서 Call Stack에서 제거됩니다.
2. ‘setTimeout’ 함수가 호출됩니다. 타이머를 설정하고, Callback 함수를 비동기적으로 처리하기 위해 브라우저의 API로 넘깁니다. 타이머가 완료되면 Callback 함수가 Event Queue로 들어갑니다.
3. console.log('End') 가 호출되고, Call Stack에 들어가 실행됩니다. 콘솔에 “End”가 출력되고, 함수가 종료되면서 Call Stack에서 제거됩니다.
4. 이제 Call Stack이 비어 있어 Event Loop는 Event Queue를 확인하고, 대기 중인 함수(setTimeout의 Callback 함수)를 Call Stack으로 가져와 실행합니다. 콘솔에 “Timeout callback”이 출력됩니다.

## 정리

- **비동기 작업의 순서**: 비동기 작업은 항상 Event Queue에 쌓이며, Main-Threaded가 다른 작업을 완료하고 나서야 실행 됩니다. 예를 들어, ‘setTimeout’ 이 0으로 설정되어도, 이 Callback 함수는 즉시 실행되지 않고 Event Queue에 대기하다가 Call Stack이 비어 있을 때 실행됩니다.
- **Event Loop와 비동기 작업의 조합**: Event Loop는 Javascript가 비동기 작업을 효과적으로 처리할 수 있게 도와주며, 동시에 Main-Threaded 가 Blocking되지 않도록 보장합니다. 이 덕분에 Javascript는 사용자 인터페이스를 매끄럽게 유지하면서도 다양한 비동기 작업을 처리할 수 있습니다.

### Reference

- https://dev-coco.tistory.com/46
- https://evan-moon.github.io/2019/09/19/sync-async-blocking-non-blocking/
- [https://inpa.tistory.com/entry/🔄-자바스크립트-이벤트-루프-구조-동작-원리](https://inpa.tistory.com/entry/%F0%9F%94%84-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84-%EA%B5%AC%EC%A1%B0-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC)
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Event_loop
