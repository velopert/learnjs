## 06. 비구조화 할당 (구조분해) 문법

이번에는 1장 섹션 6 에서도 배웠던 [비구조화 할당](https://learnjs.vlpt.us/basics/06-object.html#%EA%B0%9D%EC%B2%B4-%EB%B9%84%EA%B5%AC%EC%A1%B0%ED%99%94-%ED%95%A0%EB%8B%B9) 문법을 잘 활용하는 방법에 대해서 알아보겠습니다.

이전에 배웠던것을 복습해보자면, 비구조화 할당 문법을 사용하면 다음과 같이 객체 안에 있는 값을 추출해서 변수 혹은 상수로 바로 선언해 줄 수있었죠?

```javascript
const object = { a: 1, b: 2 };

const { a, b } = object;

console.log(a); // 1
console.log(b); // 2
```

그리고, 함수의 파라미터에서도 비구조화 할당을 할 수 있는것도 배웠습니다.

```javascript
const object = { a: 1, b: 2 };

function print({ a, b }) {
  console.log(a);
  console.log(b);
}

print(object);
```

그런데 여기서 만약 b 값이 주어지지 않았다고 가정해봅시다.

```javascript
const object = { a: 1 };

function print({ a, b }) {
  console.log(a);
  console.log(b);
}

print(object);
// 1
// undefined
```

두번째 출력에서 undefined가 나타날 것입니다. 

### 비구조화 할당시 기본값 설정

이러한 상황에 b 값에 기본 값을 주고 싶다면 이렇게 해줄 수 있습니다.

```javascript
const object = { a: 1 };

function print({ a, b = 2 }) {
  console.log(a);
  console.log(b);
}

print(object);
// 1
// 2
```


이는 꼭 함수의 파라미터에서만 할 수 있는 것은 아닙니다.

```javascript
const object = { a: 1 };

const { a, b = 2 } = object;

console.log(a); // 1
console.log(b); // 2
```


### 비구조화 할당시 이름 바꾸기

이번에는, 비구조화 할당을 하는 과정에서 선언 할 값의 이름을 바꾸는 방법을 알아보겠습니다.

예를 들어서 다음과 같은 코드가 있다고 가정해봅시다.

```javascript
const animal = {
  name: '멍멍이',
  type: '개'
};

const nickname = animal.name;

console.log(nickname); // 멍멍이
```

위 코드에서는 animal.name 값을 nickname 값에 담고 있는데요, 이름이 같다면 그냥 우리가 이전에 배웠던 대로 비구조화 할당을 쓰면 되는데 지금은 이름이 서로 다릅니다.

이러한 상황에서는 : 문자를 사용해서 이름을 바꿔줄 수 있습니다.

```javascript
const animal = {
  name: '멍멍이',
  type: '개'
};

const { name: nickname } = animal
console.log(nickname);
```

위 코드는 'animal 객체 안에 있는 name 을 nickname 이라고 선언하겠다.' 라는 의미입니다.

### 배열 비구조화 할당

비구조화 할당은 객체에만 할 수 있는 것이 아닙니다. 배열에서 할 수 있어요.

예시 코드를 봅시다.

```javascript
const array = [1, 2];
const [one, two] = array;

console.log(one);
console.log(two);
```

이 문법은 배열 안에 있는 원소를 다른 이름으로 새로 선언해주고 싶을 때 사용하면 매우 유용합니다.

객체 비구조화 할당과 마찬가지로, 기본값 지정이 가능합니다.

```javascript
const array = [1];
const [one, two = 2] = array;

console.log(one);
console.log(two);
```

### 깊은 값 비구조화 할당

객체의 깊숙한 곳에 들어있는 값을 꺼내는 방법을 알아봅시다.

예를들어서 다음과 같은 객체가 있다고 가정해봅시다.

```javascript
const deepObject = {
  state: {
    information: {
      name: 'velopert',
      languages: ['korean', 'english', 'chinese']
    }
  },
  value: 5
};
```

여기서, name, languages, value 값들을 밖으로 꺼내주고 싶다면 어떻게 해야 할까요? 이럴땐 두가지 해결 방법이 있는데요, 첫번째는 비구조화 할당 문법을 두번 사용하는 것입니다.

```javascript
const deepObject = {
  state: {
    information: {
      name: 'velopert',
      languages: ['korean', 'english', 'chinese']
    }
  },
  value: 5
};

const { name, languages } = deepObject.state.information;
const { value } = deepObject;

const extracted = {
  name,
  languages,
  value
};

console.log(extracted); // {name: "velopert", languages: Array[3], value: 5}
```

그런데 잠깐! 지금 extracted 객체를 선언 할 때 이런식으로 했는데요

```javascript
const extracted = {
  name,
  languages,
  value
}
```

이 코드는 다음 코드와 똑같습니다.
```javascript
const extracted = {
  name: name,
  languages: languages,
  value: value
}
```

만약에 key 이름으로 선언된 값이 존재하다면, 바로 매칭시켜주는 문법입니다. 이 문법은 ES6 의 object-shorthand 문법이라고 부릅니다. (이름은 굳이 알아둘 필요는 없습니다..!)

다시 본론으로 돌아와서, 아까 deepObject 객체에서 names, languages, value 를 추출하는 과정에서 비구조화 할당을 두번 했었죠?

이번엔 두번째 방법, 한번에 모두 추출하는 방법을 알아보겠습니다.

```javascript
const deepObject = {
  state: {
    information: {
      name: 'velopert',
      languages: ['korean', 'english', 'chinese']
    }
  },
  value: 5
};

const {
  state: {
    information: { name, languages }
  },
  value
} = deepObject;

const extracted = {
  name,
  languages,
  value
};

console.log(extracted);
```

이렇게 하면 깊숙히 안에 들어있는 값도 객체에서 바로 추출 할 수 있답니다. 

![](https://i.imgur.com/npMktDb.png)

위 이미지에서 주황색으로 나타난 값들이 추출 된 것입니다. 반면, 빨간색으로 나타난 값들은 따로 추출되지 않으니 참고하세요.

이렇게 깊숙한 객체안에 있는 값을 추출하는 방법을 알아보았는데요, 사람들마다 성향이 다르겠지만, 저는 개인적으로 한번에 다 추출하는 것 보다는 여러번에 걸쳐서 추출하는 것이 더욱 코드가 깔끔하다고 생각합니다. 정해진 답은 없으니 여러분이 편한 방식을 택해서 하세요.

