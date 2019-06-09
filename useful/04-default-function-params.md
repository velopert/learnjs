## 04. 함수의 기본 파라미터

이번에는 함수의 기본 파라미터를 설정하는 방법에 대해서 알아보겠습니다. 

한번, 우리가 원의 넓이를 구하는 함수를 만들어보겠습니다.

```javascript
function calculateCircleArea(r) {
  return Math.PI * r * r;
}

const area = calculateCircleArea(4);
console.log(area); // 50.26548245743669
```

여기서 Math.PI 는 원주율 파이(π) 값을 가르킵니다.

만약 우리가 이 함수에 r  값을 넣어주지 않으면 어떤 결과가 나타날까요?

```javascript
function calculateCircleArea(r) {
  return Math.PI * r * r;
}

const area = calculateCircleArea();
console.log(area); // NaN
```

결과는 NaN 이 나옵니다. Not a Number 라는 의미로, 우리가 undefined * undefined 이렇게 숫자가 아닌 값에 곱셈을 하니까 이상한 결과물이 나와버렸습니다.

이 함수에서 만약에 r 값이 주어지지 않았다면 기본 값을 1을 사용하도록 설정해봅시다.

우리가 지금까지 배운 것들을 활용하면 이렇게 작성 할 수 있습니다.

```javascript
function calculateCircleArea(r) {
  const radius = r || 1;
  return Math.PI * radius * radius;
}

const area = calculateCircleArea();
console.log(area); // 3.141592653589793
```

ES5 시절엔 위와 같이 하는게 최선이였는데, ES6 에선 다음과 같이 할 수 있게 되었습니다.

```javascript
function calculateCircleArea(r = 1) {
  return Math.PI * r * r;
}

const area = calculateCircleArea();
console.log(area); // 3.141592653589793
```

훨씬 깔끔하죠?

함수의 기본 파라미터 문법은 화살표 함수에서도 사용 할 수 있습니다.

```javascript
const calculateCircleArea = (r = 1) => Math.PI * r * r;

const area = calculateCircleArea();
console.log(area); // 3.141592653589793
```

