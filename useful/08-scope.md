## 08. 자바스크립트의 Scope 에 대한 이해

이번에는 자바스크립트의 Scope 에 대해서 알아봅시다. Scope 란, 우리가 변수 혹은 함수를 선언하게 될 때 해당 변수 또는 함수가 유효한 범위를 의미합니다. Scope 는 총 3가지 종류가있습니다.

1. **Global (전역) Scope**: 코드의 모든 범위에서 사용이 가능합니다.
2. **Function (함수) Scope**: 함수 안에서만 사용이 가능합니다.
3. **Block (블록) Scope**: if, for, switch 등 특정 블록 내부에서만 사용이 가능합니다.


### 예시를 통한 Scope 이해

한번, 예시 코드를 보고 Scope 를 이해해봅시다.

```javascript
const value = 'hello!';

function myFunction() {
  console.log('myFunction: ');
  console.log(value);
}

function otherFunction() {
  console.log('otherFunction: ');
  const value = 'bye!';
  console.log(value);
}

myFunction();
otherFunction();

console.log('global scope: ');
console.log(value);

```

위 코드의 결과는 다음과 같습니다.

![](https://i.imgur.com/8pSTR1B.png)

코드의 맨 윗줄에서 선언된 `value` 값은 Global Scope 로 선언된 값입니다. Global Scope 로 선언된 값은 어디서든지 사용이 가능합니다. `myFunction` 에서 바로 사용을 할 수 있었지요?

`otherFunction` 에서는 함수 내부에서 `value` 값을 `'bye!'` 로 새로 선언을 해주었습니다. 이렇게 되면, value 라는 값은 Function Scope 로 지정이 되서 해당 값은 `otherFunction` 내부에서만 유효한 값이 됩니다. 이렇게 값을 설정한다고 해서 기존에 Global Scope 로 선언된 `value` 값이 바뀌지 않습니다.

또 다른 예시를 확인해봅시다.

```javascript
const value = 'hello!';

function myFunction() {
  const value = 'bye!';
  const anotherValue = 'world';
  function functionInside() {
    console.log('functionInside: ');
    console.log(value);
    console.log(anotherValue);
  }
  functionInside();
}


myFunction()
console.log('global scope: ');
console.log(value);
console.log(anotherValue);
```

![](https://i.imgur.com/LWAlKxY.png)

`myFunction` 내부에 `anotherValue` 라는 새로운 값을 선언했고, `functionInside` 라는 함수도 선언을 했습니다. `functionInside` 함수에서는 `myFunction` 에서 선언한 `value` 값과 `anotherValue` 값을 조회 할 수 있습니다.

반면, `myFunction` 밖에서는 `anotherValue` 를 조회 할 수 없습니다.

이제, 또 다른 예시를 알아봅시다.

```javascript
const value = 'hello!';

function myFunction() {
  const value = 'bye!';
  if (true) {
    const value = 'world';
    console.log('block scope: ');
    console.log(value);
  }
  console.log('function scope: ');
  console.log(value);
}

myFunction();
console.log('global scope: ');
console.log(value);
```

![](https://i.imgur.com/wz0uA9I.png)

`const` 로 선언한 값은 Block Scope 로 선언이 됩니다. 따라서, if 문 같은 블록 내에서 새로운 변수/상수를 선언하게 된다면, 해당 블록 내부에서만 사용이 가능하며, 블록 밖의 범위에서 똑같은 이름을 가진 값이 있다고 해도 영향을 주지 않습니다.

`let` 또한 마찬가지 입니다.

하지만 `var` 는 어떨까요?

```javascript
var value = 'hello!';

function myFunction() {
  var value = 'bye!';
  if (true) {
    var value = 'world';
    console.log('block scope: ');
    console.log(value);
  }
  console.log('function scope: ');
  console.log(value);
}

myFunction();
console.log('global scope: ');
console.log(value);
```

`var` 는 Function Scope 로 선언이 되므로, if 문 블록 내부에서 선언한 value 값이 블록 밖의 value 에도 영향을 미치게 됩니다.

![](https://i.imgur.com/uHKGfKO.png)


### Hoisting 이해하기

Hoisting 이란, 자바스크립트에서 아직 선언되지 않은 함수/변수를 "끌어올려서" 사용 할 수 있는 자바스크립트의 작동 방식을 의미합니다.

다음 코드를 확인해보세요.


```javascript
myFunction();

function myFunction() {
  console.log('hello world!');
}
```

위 코드에서는 `myFunction` 함수를 선언하기 전에, `myFunction()` 을 호출해주었습니다. 함수가 아직 선언되지 않았음에도 불구하고 코드는 정상적으로 작동하게 됩니다.

이게 잘 작동하는 이유는, 자바스크립트 엔진이 위 코드를 해석하는 과정에서, 다음과 같이 받아들이게 되기 때문입니다.

```javascript
function myFunction() {
  console.log('hello world!');
}

myFunction();
```

이러한 현상을, Hoisting 이라고 부릅니다.

변수 또한 Hoisting 됩니다.

예를 들어서, 다음과 같은 코드를 실행한다면,

```javascript
console.log(number);
```

![](https://i.imgur.com/SQjmfQR.png)

이런 오류가 발생합니다.

그렇지만, 다음과 같은 코드는

```javascript
console.log(number);
var number = 2;
```

![](https://i.imgur.com/TIwGkJL.png)

`undefined` 가 출력됩니다.

자바스크립트 엔진이 위 코드를 해석 할 때는 다음과 같이 받아들이게 됩니다.

```javascript
var number;
console.log(number);
number = 2;
```

반면, `const` 와 `let` 은 hoisting 이 발생하지 않고, 에러가 발생하게 됩니다. Codesandbox 에서는 자바스크립트가 Babel 이라는 도구에 의하여 `const` 와 `let` 이 `var` 로 변환되기 때문에 오류가 발생하지 않습니다. Chrome 개발자 도구의 콘솔에서 다음 코드를 실행해보세요. (혹은 Codesandbox 의 설정에서 .babelrc 를 비워도 됩니다.

```javascript
function fn() {
	console.log(a);
    let a = 2;
}
fn();
```

![](https://i.imgur.com/sHIevmg.png)

Hoisting 은 자바스크립트 엔진이 갖고 있는 성질이며, Hoisting 을 일부러 할 필요는 없지만, 방지하는 것이 좋습니다. 왜냐하면 Hoisting 이 발생하는 코드는 이해하기 어렵기 때문에 유지보수도 힘들어지고 의도치 않는 결과물이 나타나기 쉽기 때문입니다.

Hoisting 을 방지하기 위해서, 함수의 경우 꼭 선언 후에 호출을 하도록 주의를 하시고, `var` 대신 `const`, `let` 을 위주로 사용하세요. 추가적으로, 나중에 자바스크립트 개발을 본격적으로 하게 될 때에는 ESLint 라는것을 사용하여 Hoisting 이 발생하는 코드는 에디터상에서 쉽게 발견해낼 수 있습니다.