## 02. Truthy and Falsy

이것은 자바스크립트 문법까지는 아니지만, 알아둬야 하는 개념입니다.

Truthy: true 같은거...
Falsy: false 같은거...

라고 이해를 하면 되는데요, 예를 들어서 다음과 같은 함수가 있다고 가정해봅시다.

```javascript
function print(person) {
  console.log(person.name);
}

const person = {
  name: 'John'
};

print(person);
```

만약에 이러한 상황에서, 만약 print 함수가 다음과 같이 파라미터가 비어진 채로 실행됐다고 가정해봅시다.

```javascript
function print(person) {
  console.log(person.name);
}

const person = {
  name: 'John'
};

print();
```

이 코드는 다음과 같은 에러를 생성해냅니다.

```
TypeError: Cannot read property 'name' of undefined
```

이러한 상황에서, 만약에 print 함수에서 만약에 object 가 주어지지 않았다면, 문제가 있다고 콘솔에 출력해야 한다면 다음과 같이 구현 할 수 있습니다.

```javascript
function print(person) {
  if (person === undefined) {
    return;
  }
  console.log(person.name);
}

const person = {
  name: 'John'
};

print();
```

그런데 만약에 다음과 같이 print 에 null 값이 파라미터로 전달되면 어떨까요?

```javascript
function print(person) {
  if (person === undefined) {
    console.log('person이 없네요');
    return;
  }
  console.log(person.name);
}

const person = null;
print(person);
```

그러면 또 오류가 발생하게 됩니다.

```
TypeError: Cannot read property 'name' of null
```


그러면 또.. print 함수에 조건을 추가해줘야합니다.

```javascript
function print(person) {
  if (person === undefined || person === null) {
    console.log('person이 없네요');
    return;
  }
  console.log(person.name);
}

const person = null;
print(person);
```


이렇게 person 이 undefined 이거나, null 인 상황을 대비하려면 위와 같이 코드를 작성해야하는데요, 여기서 위 코드는 다음과 같이 축약해서 작성 할 수 있답니다.

```javascript
function print(person) {
  if (!person) {
    console.log('person이 없네요');
    return;
  }
  console.log(person.name);
}

const person = null;
print(person);
```

이게 작동하는 이유는, undefined 와 null 은 Falsy 한 값입니다. Falsy 한 값 앞에 느낌표를 붙여주면 true 로전환됩니다.

다음 코드를 입력해보세요.

```javascript
console.log(!undefined);
console.log(!null);
```

Falsy 한 값은 이 외에도 몇개 더 있습니다.

```javascript
console.log(!undefined);
console.log(!null);
console.log(!0);
console.log(!'');
console.log(!NaN);
```

이 값은 모두 true 가 됩니다.

여기서 NaN 이란 값은 조금 생소하지요, 이 값은 Not A Number 라는 의미를 가지고 있는데요, 보통 NaN 은 문자열을 숫자로 변환하는 자바스크립트 기본함수 parseInt 라는 함수를 사용하게 될 때 볼 수 있습니다.

```javascript
const num = parseInt('15', 10); // 10진수 15를 숫자로 변환하겠다는 의미
console.log(num); // 10
const notnum = parseInt('야호~', 10);
console.log(notnum); // NaN
```

다시 본론으로 돌아와서, Falsy 한 값은 아까 나열한 다섯가지 입니다.

그리고, 그 외의 값은 모두! Truthy 한 값입니다. 


한번, 이렇게 코드를 적어보세요.

```javascript
console.log(!3);
console.log(!'hello');
console.log(!['array?']);
console.log(![]);
console.log(!{ value: 1 });
```

이번에는 아까와는 반대로 모든 값이 false 가 됩니다. 


Truthy 한 값과 Falsy 한 값은 if 문에서도 사용 할 수있습니다.

```javascript
const value = { a: 1 };
if (value) {
  console.log('value 가 Truthy 하네요.');
}
```

value 가 Truthy 한 값이기 때문에, 콘솔에 메시지가 출력 될 것입니다. 반면, value 가 null, undefined, 0, '', NaN 중 하나라면, 나타나지 않을 것입니다.


그래서 이렇게, Truthy 한 값과 Falsy 한 값을 잘 알아놓으면 조건문을 작성할 때 편할 것입니다.


추가적으로, 알아두면 유용한 팁 하나를 드리겠습니다.

만약에, 특정 값이 Truthy 한 값이라면 true, 그렇지 않다면 false 로 값을 표현하는 것을 구현해보겠습니다.

```javascript
const value = { a: 1 };

const truthy = value ? true : false;
```

우리가 이전에 배운 삼항연산자를 사용하면 쉽게 value 값의 존재 유무에 따라 쉽게 true 및 false 로 전환이 가능합니다. 그런데, 이를 더 쉽게 할 수도 있습니다.

```javascript
const value = { a: 1 };
const truthy = !!value;
```

!value 는 false 가 되고, 여기에 !false 는 true 가 되어서, 결과는 true 가 됩니다.