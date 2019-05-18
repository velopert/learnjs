## 01. 삼항 연산자

첫번째로 배울 문법은, 삼항 연산자입니다. 이 문법은 ES6 문법은 아닙니다.

```javascript
const array = [];
let text = '';
if (array.length === 0) {
  text = '배열이 비어있습니다.';
} else {
  text = '배열이 비어있지 않습니다.';
}
console.log(text);
```

예를 들어 위와 같이 특정 조건에 따라 text 값이 달라야 하는 상황이 있다고 가정해봅시다.

그런 경우에는 다음과 같이 코드를 작성 할 수 있습니다.

```javascript
const array = [];
let text = array.length === 0 ? '배열이 비어있습니다' : '배열이 비어있지 않습니다.';

console.log(text);
```

삼항 연산자의 사용법은 다음과 같습니다.

```javascript
조건 ? true일때 : false일때
```

라인의 길이가 너묵 길어진다면 다음과 같이 작성하기도 합니다.

```javascript
const array = [];
let text = array.length === 0 
  ? '배열이 비어있습니다' 
  : '배열이 비어있지 않습니다.';

console.log(text);
```

다음과 같이 삼항 연산자를 중첩해서 쓸 수도 있는데요

```javascript
const condition1 = false;
const condition2 = false;

const value = condition1 
  ? '와우!' 
  : condition2 
    ? 'blabla' 
    : 'foo';

console.log(value);
```

가독성이 그렇게 좋지 않으니 이러한 코드는 피하시는 것이 좋습니다. 이런 상황에는 차라리 if문으로 처리하는게 오히려 코드를 읽기가 쉬워질 수도 있습니다.
