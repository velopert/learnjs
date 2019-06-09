# 3장. 자바스크립트에서 비동기 처리 다루기

자바스크립트의 동기적 처리와 비동기 처리에 대해서 알아봅시다.

![](https://i.imgur.com/hh3Mawr.png)

만약 작업을 동기적으로 처리한다면 작업이 끝날 때까지 기다리는 동안 중지 상태가 되기 때문에 다른 작업을 할 수 없습니다. 그리고 작업이 끝나야 비로소 그 다음 예정된 작업을 할 수 있죠. 하지만 이를 비동기적으로 처리를 한다면 흐름이 멈추지 않기 때문에 동시에 여러 가지 작업을 처리할 수도 있고, 기다리는 과정에서 다른 함수도 호출할 수 있습니다.

그러면, 한번 코드를 보고 이해해봅시다.

연산량이 많은 작업을 처리하는 함수를 만들어보겠습니다.

우선, Codesandbox 의 설정에서 sandbox.config.json 을 열어서 Infinite Loop Protection 이라는 속성을 비활성화하세요.

![](https://i.imgur.com/nejYC6f.png)

그 다음에, index.js 를 다음과 같이 수정해보세요.

```javascript
function work() {
  const start = Date.now();
  for (let i = 0; i < 1000000000; i++) {}
  const end = Date.now();
  console.log(end - start + 'ms');
}

work();
console.log('다음 작업');

```

여기서 Date.now 는 현재 시간을 숫자 형태로 가져오는 자바스크립트 내장 함수입니다. 위 work 함수는, 1,000,000,000 번 루프를 돌고, 이 작업이 얼마나 걸렸는지 알려줍니다.

![](https://i.imgur.com/jLvBqG8.png)

지금은 `work()` 함수가 호출되면, for 문이 돌아갈 때는 다른 작업은 처리하지 않고 온전히 for 문만 실행하고 있습니다.

만약 이 작업이 진행되는 동안 다른 작업도 하고 싶다면 함수를 비동기 형태로 전환을 해주어야하는데요, 그렇게 하기 위해서는 `setTimeout` 이라는 함수를 사용해주어야합니다.

코드를 다음과 같이 수정해보세요.

```javascript
function work() {
  setTimeout(() => {
    const start = Date.now();
    for (let i = 0; i < 1000000000; i++) {}
    const end = Date.now();
    console.log(end - start + 'ms');
  }, 0);
}

console.log('작업 시작!');
work();
console.log('다음 작업');
```

`setTimeout` 함수는 첫번째 파라미터에 넣는 함수를 두번째 파라미터에 넣은 시간(ms 단위)이 흐른 후 호출해줍니다. 지금은 두번째 파라미터에 0을 넣었습니다. 따라서, 이 함수는 바로 실행이 됩니다. 0ms 이후에 실행한다는 의미이지만 실제로는 4ms 이후에 실행됩니다 [(참고)](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout#Reasons_for_delays_longer_than_specified). 이렇게 `setTimeout` 을 사용하면 우리가 정한 작업이 백그라운드에서 수행되기 때문에 기존의 코드 흐름을 막지 않고 동시에 다른 작업들을 진행 할 수 있습니다.

![](https://i.imgur.com/F6wmvsg.png)

결과물을 보면, 작업이 시작 되고 나서, for 루프가 돌아가는 동안 다음 작업도 실행되고, for 루프가 끝나고 나서 몇 ms 걸렸는지 나타나고 있습니다.

그렇다면, 만약에 work 함수가 끝난 다음에 어떤 작업을 처리하고 싶다면 어떻게 해야 할까요? 이럴 땐, 콜백 함수를 파라미터로 전달해주면 됩니다. 콜백 함수란, 함수 타입의 값을 파라미터로 넘겨줘서, 파라미터로 받은 함수를 특정 작업이 끝나고 호출을 해주는 것을 의미합니다.

```javascript
function work(callback) {
  setTimeout(() => {
    const start = Date.now();
    for (let i = 0; i < 1000000000; i++) {}
    const end = Date.now();
    console.log(end - start + 'ms');
    callback();
  }, 0);
}

console.log('작업 시작!');
work(() => {
  console.log('작업이 끝났어요!')
});
console.log('다음 작업');
```

![](https://i.imgur.com/3rvXGzS.png)

다음과 같은 작업들은 주로 비동기적으로 처리하게 됩니다.

- **Ajax Web API 요청**: 만약 서버쪽에서 데이터를 받와아야 할 때는, 요청을 하고 서버에서 응답을 할 때 까지 대기를 해야 되기 때문에 작업을 비동기적으로 처리합니다.
- **파일 읽기**: 주로 서버 쪽에서 파일을 읽어야 하는 상황에는 비동기적으로 처리합니다.
- **암호화/복호화**: 암호화/복호화를 할 때에도 바로 처리가 되지 않고, 시간이 어느정도 걸리는 경우가 있기 때문에 비동기적으로 처리합니다.
- **작업 예약**: 단순히 어떤 작업을 몇초 후에 스케쥴링 해야 하는 상황에는, setTimeout 을 사용하여 비동기적으로 처리합니다.

비동기 작업을 다룰 때에는 callback 함수 외에도 Promise, 그리고 async/await 라는 문법을 사용하여 처리 할 수 있습니다. 이번 챕터에서는 이에 대하여 알아보게 됩니다.

