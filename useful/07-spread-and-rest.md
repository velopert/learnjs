## 07. spread 와 rest

이번에는 ES6 에서 도입된 spread 와 rest 문법에 대해서 알아보겠습니다. 서로 완전히 다른 문법인데요, 은근히 좀 비슷합니다.

### spread

일단 spread 문법부터 알아봅시다. spread 라는 단어가 가지고 있는 의미는 펼치다, 퍼뜨리다 입니다. 이 문법을 사용하면, 객체 혹은 배열을 펼칠수있습니다.

예를 들어서 다음과 같은 객체들이 있다고 가정해봅시다.

```javascript
const slime = {
  name: '슬라임'
};

const cuteSlime = {
  name: '슬라임',
  attribute: 'cute'
};

const purpleCuteSlime = {
  name: '슬라임',
  attribute: 'cute',
  color: 'purple'
};

console.log(slime);
console.log(cuteSlime);
console.log(purpleCuteSlime);
```

![](https://i.imgur.com/XeRXMXb.png)

이 코드에서는 먼저 slime 이라는 객체를 선언했습니다. 그리고 cuteSlime 이라는 객체를 만들었는데요, 기존에 선언한 slime 을 건들이지 않고 새로운 객체를 만들어서 slime 이 가지고 있는 값을 그대로 사용하였습니다.

그 다음에는 purpleCuteSlime 이라는 객체를 만들었는데요, 이 객체는 cuteSlime 이 가지고 있는 속성을 그대로 사용하면서 추가적으로 color 가 추가되었습니다.

위 코드에서의 핵심은, 기존의 것을 건들이지 않고, 새로운 객체를 만든다는 것 인데요, 이러한 상황에 사용 할 수 있는 유용한 문법이 spread 입니다.

아까 코드는 spread 문법을 사용하면 다음과 같이 작성 할 수 있습니다.

```javascript
const slime = {
  name: '슬라임'
};

const cuteSlime = {
  ...slime,
  attribute: 'cute'
};

const purpleCuteSlime = {
  ...cuteSlime,
  color: 'purple'
};

console.log(slime);
console.log(cuteSlime);
console.log(purpleCuteSlime);
```

여기서 사용한 ... 문자가 바로 spread 연산자입니다.

spread 연산자는 배열에서도 사용 할 수 있습니다.


```javascript
const animals = ['개', '고양이', '참새'];
const anotherAnimals = [...animals, '비둘기'];
console.log(animals);
console.log(anotherAnimals);
```

![](https://i.imgur.com/Z8t1wEt.png)

기존의 animals 는 건드리지 않으면서, 새로운 anotherAnimals 배열에 animals 가 가지고 있는 내용을 모두 집어넣고, '비둘기' 라는 항목을 추가적으로 넣었습니다.

배열에서 spread 연산자를 여러번 사용 할 수도 있습니다.

```javascript
const numbers = [1, 2, 3, 4, 5];

const spreadNumbers = [...numbers, 1000, ...numbers];
console.log(spreadNumbers); // [1, 2, 3, 4, 5, 1000, 1, 2, 3, 4, 5]
```


### rest

rest는 생김새는 spread 랑 비슷한데, 역할이 매우 다릅니다.

rest는 객체, 배열, 그리고 함수의 파라미터에서 사용이 가능합니다.

#### 객체에서의 rest

우선 객체에서의 예시를 알아볼까요?

```javascript
const purpleCuteSlime = {
  name: '슬라임',
  attribute: 'cute',
  color: 'purple'
};

const { color, ...rest } = purpleCuteSlime;
console.log(color);
console.log(rest);
```

![](https://i.imgur.com/XYg74q3.png)

rest 안에 name 값을 제외한 값이 들어있습니다. 

rest 는 객체와 배열에서 사용 할 때는 이렇게 비구조화 할당 문법과 함께 사용됩니다. 주로 사용 할때는 위와 같이 rest 라는 키워드를 사용하게 되는데요, 추출한 값의 이름이 꼭 rest 일 필요는 없습니다.

```javascript
const purpleCuteSlime = {
  name: '슬라임',
  attribute: 'cute',
  color: 'purple'
};

const { color, ...cuteSlime } = purpleCuteSlime;
console.log(color);
console.log(cuteSlime);
```

이렇게 해도 무방합니다.

이어서, attribute 까지 없앤 새로운 객체를 만들고 싶다면 이렇게 해주면 되겠죠.

```javascript
const purpleCuteSlime = {
  name: '슬라임',
  attribute: 'cute',
  color: 'purple'
};

const { color, ...cuteSlime } = purpleCuteSlime;
console.log(color);
console.log(cuteSlime);

const { attribute, ...slime } = cuteSlime;
console.log(attribute);
console.log(slime);
```

![](https://i.imgur.com/ejvAHKJ.png)

#### 배열에서의 rest

다음, 배열에서의 사용 예시를 알아봅시다.

```javascript
const numbers = [0, 1, 2, 3, 4, 5, 6];

const [one, ...rest] = numbers;

console.log(one);
console.log(rest);
```

![](https://i.imgur.com/tEpTlMQ.png)

배열 비구조화 할당을 통하여 원하는 값을 밖으로 꺼내고, 나머지 값을 rest 안에 넣었습니다.

반면 이렇게 할 수는 없답니다.

```javascript
const numbers = [0, 1, 2, 3, 4, 5, 6];

const [..rest, last] = numbers;
```

![](https://i.imgur.com/E9dyzir.png)


#### 함수 파라미터에서의 rest

rest 를 함수파라미터에서 사용 할 수도 있습니다. 예를 들어서 우리가 파라미터로 넣어준 모든 값들을 합해주는 함수를 만들어주고 싶다고 가정해봅시다.

```javascript
function sum(a, b, c, d, e, f, g) {
  let sum = 0;
  if (a) sum += a;
  if (b) sum += b;
  if (c) sum += c;
  if (d) sum += d;
  if (e) sum += e;
  if (f) sum += f;
  if (g) sum += g;
  return sum;
}

const result = sum(1, 2, 3, 4, 5, 6);
console.log(result);
```

위에서의 sum 함수는 7개의 파라미터를 받아오는데, 아래에서 사용 할때에는 6개만 넣어줬습니다. 그러면, g 값이 undefined 가 되기 때문에 sum 에 더하는 과정에서 += undefined 를 하게 되면 결과는 NaN 이 되버립니다. 그렇기 때문에 함수에서 하나하나 유효한 값인지 확인을 해줬지요.

함수의 파라미터가 몇개가 될 지 모르는 상황에서 rest 파라미터를 사용하면 매우 유용합니다. 코드를 다음과 같이 수정해보세요.

```javascript
function sum(...rest) {
  return rest;
}

const result = sum(1, 2, 3, 4, 5, 6);
console.log(result);
```

![](https://i.imgur.com/Pvm0tha.png)

result 가 가르키고 있는 것은 함수에서 받아온 파라미터들로 이루어진 배열입니다. 우리가 이제 파라미터들이 들어가있는 배열을 받았으니, 그냥 모두 더해주면 되겠죠?

```javascript
function sum(...rest) {
  return rest.reduce((acc, current) => acc + current, 0);
}

const result = sum(1, 2, 3, 4, 5, 6);
console.log(result); // 21
```

여기서 reduce 함수가 사용 됐는데, reduce 를 잘 모르겠으면 [1장 섹션 9](https://learnjs.vlpt.us/basics/09-array-functions.html#reduce)를 복습하고 오세요.

### 함수 인자와 spread

이번에는, 다시 아까 배웠던 spread 로 돌아와서 한가지를 더 가르쳐드리겠습니다. 바로 함수의 인자와 spread 인데요, 만약 프로그래밍을 처음 배우신다면 파라미터와 인자가 좀 헷갈릴 수 있습니다. 이에 대해서 간단하게 설명 드려볼게요.

```javascript
const myFunction(a) { // 여기서 a 는 파라미터
  console.log(a); // 여기서 a 는 인자
}

myFunction('hello world'); // 여기서 'hello world' 는 인자
```

함수에서 값을 읽을때, 그 값들은 파라미터라고 부릅니다.
그리고 함수에서 값을 넣어줄 때, 그 값들은 인자라고 부릅니다.

인자가 무엇인지 이해를 하셨다면 이제 함수인자와 spread 문법을 사용하는 것에 대하여 알아볼게요.

우리가 방금 함수파라미터와 rest 를 사용한 것과 비슷한데, 반대의 역할입니다. 예를 들어서, 우리가 배열 안에 있는 원소들을 모두 파라미터로 넣어주고 싶다고 가정해보겠습니다.


```javascript
function sum(...rest) {
  return rest.reduce((acc, current) => acc + current, 0);
}

const numbers = [1, 2, 3, 4, 5, 6];
const result = sum(
  numbers[0],
  numbers[1],
  numbers[2],
  numbers[3],
  numbers[4],
  numbers[5]
);
console.log(result);
```

굉장히 불편하죠? 만약에 sum함수를 사용 할 때 인자 부분에서 spread 를 사용하면 다음과 같이 표현이 가능합니다.

```javascript
function sum(...rest) {
  return rest.reduce((acc, current) => acc + current, 0);
}

const numbers = [1, 2, 3, 4, 5, 6];
const result = sum(...numbers);
console.log(result);
```

어떤가요? 정말 편하죠?

이렇게, spread 와 rest 를 잘 사용하면 앞으로 보기 깔끔한 코드를 작성하는 것에 큰 도움을 줄 것입니다.


### 퀴즈

함수에 n 개의 숫자들이 파라미터로 주어졌을 때, 그 중 가장 큰 값을 알아내세요.

```javascript
function max() {
  return 0;
}

const result = max(1, 2, 3, 4, 10, 5, 6, 7);
console.log(result);
```

[![Edit gifted-davinci-qxqzn](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/gifted-davinci-qxqzn?fontsize=14)

위 CodeSandbox 링크에서 우측에 뜨는 Tests 를 통과시키시면 됩니다.

[정답](https://codesandbox.io/s/silly-napier-pippm)

