## 02. async/await

async/await 문법은 ES8에 해당하는 문법으로서, Promise 를 더욱 쉽게 사용 할 수 있게 해줍니다.

기본적인 사용법을 알아봅시다.

```javascript
function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function process() {
  console.log('안녕하세요!');
  await sleep(1000); // 1초쉬고
  console.log('반갑습니다!');
}

process();
```

async/await 문법을 사용할 때에는, 함수를 선언 할 때 함수의 앞부분에 `async` 키워드를 붙여주세요. 그리고 Promise 의 앞부분에 `await` 을 넣어주면 해당 프로미스가 끝날때까지 기다렸다가 다음 작업을 수행 할 수 있습니다.

위 코드에서는 `sleep` 이라는 함수를 만들어서 파라미터로 넣어준 시간 만큼 기다리는 Promise 를 만들고, 이를 `process` 함수에서 사용해주었습니다.

함수에서 `async` 를 사용하면, 해당 함수는 결과값으로 Promise 를 반환하게 됩니다. 따라서 다음과 같이 코드를 작성 할 수 있습니다.

```javascript
function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function process() {
  console.log('안녕하세요!');
  await sleep(1000); // 1초쉬고
  console.log('반갑습니다!');
}

process().then(() => {
  console.log('작업이 끝났어요!');
});
```

`async` 함수에서 에러를 발생 시킬때에는 `throw` 를 사용하고, 에러를 잡아낼 때에는 try/catch 문을 사용합니다.

```javascript
function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function makeError() {
  await sleep(1000);
  const error = new Error();
  throw error;
}

async function process() {
  try {
    await makeError();
  } catch (e) {
    console.error(e);
  }
}

process();
```

![](https://i.imgur.com/5HndlIW.png)


이번에는, 비동기 함수를 몇개 더 만들어보겠습니다.

```javascript
function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

const getDog = async () => {
  await sleep(1000);
  return '멍멍이';
};

const getRabbit = async () => {
  await sleep(500);
  return '토끼';
};
const getTurtle = async () => {
  await sleep(3000);
  return '거북이';
};

async function process() {
  const dog = await getDog();
  console.log(dog);
  const rabbit = await getRabbit();
  console.log(rabbit);
  const turtle = await getTurtle();
  console.log(turtle);
}

process();

```

현재 위 코드에서는 `getDog` 는 1초, `getRabbit` 은 0.5초, `getTurtle` 은 3초가 걸리고 있습니다. 이 함수들을 `process` 함수에서 연달아서 사용하게 되면서, `process` 함수가 실행되는 총 시간은 4.5초가 됩니다.

지금은 `getDog` -> `getRabbit` -> `getTurtle` 순서대로 실행이 되고 있는데요, 하나가 끝나야 다음 작업이 시작하고 있는데, 동시에 작업을 시작하고 싶다면, 다음과 같이 `Promise.all` 을 사용해야합니다.

```javascript
function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

const getDog = async () => {
  await sleep(1000);
  return '멍멍이';
};

const getRabbit = async () => {
  await sleep(500);
  return '토끼';
};
const getTurtle = async () => {
  await sleep(3000);
  return '거북이';
};

async function process() {
  const results = await Promise.all([getDog(), getRabbit(), getTurtle()]);
  console.log(results);
}

process();
```

![](https://i.imgur.com/cQtv48g.png)

만약에 여기서 배열 비구조화 할당 문법을 사용한다면 각 결과값을 따로 따로 추출해서 조회 할 수 있습니다.

```javascript
function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

const getDog = async () => {
  await sleep(1000);
  return '멍멍이';
};

const getRabbit = async () => {
  await sleep(500);
  return '토끼';
};
const getTurtle = async () => {
  await sleep(3000);
  return '거북이';
};

async function process() {
  const [dog, rabbit, turtle] = await Promise.all([
    getDog(),
    getRabbit(),
    getTurtle()
  ]);
  console.log(dog);
  console.log(rabbit);
  console.log(turtle);
}

process();
```


`Promise.all` 를 사용 할 때에는, 등록한 프로미스 중 하나라도 실패하면, 모든게 실패 한 것으로 간주합니다.


이번에는 `Promise.race` 라는 것에 대해서 알아봅시다. 이 함수는 `Promise.all` 과 달리, 여러개의 프로미스를 등록해서 실행했을 때 가장 빨리 끝난것 하나만의 결과값을 가져옵니다.

```javascript
function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

const getDog = async () => {
  await sleep(1000);
  return '멍멍이';
};

const getRabbit = async () => {
  await sleep(500);
  return '토끼';
};
const getTurtle = async () => {
  await sleep(3000);
  return '거북이';
};

async function process() {
  const first = await Promise.race([
    getDog(),
    getRabbit(),
    getTurtle()
  ]);
  console.log(first);
}

process();
```

`Promise.race` 의 경우엔 가장 다른 Promise 가 먼저 성공하기 전에 가장 먼저 끝난 Promise 가 실패하면 이를 실패로 간주합니다. 따라서, 현재 위의 코드에서 `getRabbit` 에서 에러를 발생시킨다면 에러를 잡아낼 수 있지만, `getTurtle` 이나 `getDog` 에서 발생한 에러는 무시됩니다.