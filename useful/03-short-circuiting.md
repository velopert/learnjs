## 03. 단축 평가 (short-circuit evaluation) 논리 계산법

이번에는 논리 연산자를 조금 더 유용하게 사용하는 방법에 대해서 배워보겠습니다.

우리가 이전에 연산자를 배울때, 다음과 사항을 잘 숙지하셨을겁니다.

```javascript
true && true // true
true && false // false
true || false // true
false || true // true
```

논리 연산자를 사용 할 때에는 무조건 우리가 true 혹은 false 값을 사용해야 되는 것은 아닙니다. 문자열이나 숫자, 객체를 사용 할 수도 있고, 해당 값이 Truthy 하냐 Falsy 하냐에 따라 결과가 달라집니다.

예를 들어서 다음과 같은 코드가 있다고 가정해보겠습니다.

```javascript
const dog = {
  name: '멍멍이'
};

function getName(animal) {
  return animal.name;
}

const name = getName(dog);
console.log(name); // 멍멍이
```

그런데 만약, getName 의 파라미터에 제대로된 객체가 주어지지 않으면 어떻게 될까요?

```javascript
const dog = {
  name: '멍멍이'
};

function getName(animal) {
  return animal.name;
}

const name = getName();
console.log(name);
```

![](https://i.imgur.com/SHJP2MU.png)

animal 객체가 undefined 이기 때문에, undefined 에서 name 값을 조회 할 수 없어서 이렇게 에러가 발생하게 됩니다.

그렇다면, 만약 함수에서 animal 값이 제대로 주어졌을 때만 name 을 조회하고, 그렇지 않을때는 그냥 undefined 를 반환하게 하고 싶으면 어떻게 해야 할까요?

```javascript
const dog = {
  name: '멍멍이'
};

function getName(animal) {
  if (animal) {
    return animal.name;
  }
  return undefined;
}

const name = getName();
console.log(name);
```

이렇게 하면 animal 값이 주어지지 않아도, 에러가 발생하지 않게 됩니다. 이러한 코드를 논리 연산자를 사용하면 코드를 단축시킬 수 있습니다.

### && 연산자로 코드 단축시키기

이렇게 코드를 작성해보세요.

```javascript
const dog = {
  name: '멍멍이'
};

function getName(animal) {
  return animal && animal.name;
}

const name = getName();
console.log(name); // undefined
```

아까 코드와 이 코드는 완벽히 똑같이 작동하는 코드입니다. 한번 다음과 같이 파라미터를 넣어서 호출도 해보세요.

```javascript
const dog = {
  name: '멍멍이'
};

function getName(animal) {
  return animal && animal.name;
}

const name = getName(dog);
console.log(name); // 멍멍이
```

이게 작동하는 이유는, A && B 연산자를 사용하게 될 때에는 A 가 Truthy 한 값이라면, B 가 결과값이 됩니다. 반면, A 가 Falsy 한 값이라면 결과는 A 가 됩니다.


다음 예시를 한번 살펴보세요.

```javascript
console.log(true && 'hello'); // hello
console.log(false && 'hello'); // false
console.log('hello' && 'bye'); // bye
console.log(null && 'hello'); // null
console.log(undefined && 'hello'); // undefined
console.log('' && 'hello'); // ''
console.log(0 && 'hello'); // 0
console.log(1 && 'hello'); // hello
console.log(1 && 1); // 1
```

이러한 속성을 잘 알아두면, 특정 값이 유효할때에만 어떤 값을 조회하는 작업을 해야 할 때 매우 유용합니다.


### || 연산자로 코드 단축시키기

|| 연산자는 만약 어떤 값이 Falsy 하다면 대체로 사용 할 값을 지정해줄 때 매우 유용하게 사용 할 수 있습니다.

예를 들어서 다음과 같은 코드가 있다고 가정해봅시다.

```javascript
const namelessDog = {
  name: ''
};

function getName(animal) {
  const name = animal && animal.name;
  if (!name) {
    return '이름이 없는 동물입니다';
  }
  return name;
}

const name = getName(namelessDog);
console.log(name); // 이름이 없는 동물입니다.
```

위 코드는 || 연산자를 사용하면 다음과 같이 단축시킬 수 있습니다.

```javascript
const namelessDog = {
  name: ''
};

function getName(animal) {
  const name = animal && animal.name;
  return name || '이름이 없는 동물입니다.';
}

const name = getName(namelessDog);
console.log(name); // 이름이 없는 동물입니다.
```

A || B 는 만약 A 가 Truthy 할경우 결과는 A 가 됩니다. 반면, A 가 Falsy 하다면 결과는 B 가 됩니다.

