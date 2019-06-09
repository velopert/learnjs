## 05. 조건문 더 스마트하게 쓰기

이번에는 조건문을 조금 더 스마트하게 쓰는 방법에 대해서 알아보겠습니다.

### 특정 값이 여러 값중 하나인지 확인해야 할 때

만약, 여러분이 특정 값이 여러 값 중 하나인지 확인을 해야 하는 상황이 생겼다고 해봅시다.

그러면, 이러한 시도를 할 수도 있을 것입니다.

```javascript
function isAnimal(text) {
  return (
    text === '고양이' || text === '개' || text === '거북이' || text === '너구리'
  );
}

console.log(isAnimal('개')); // true
console.log(isAnimal('노트북')); // false
```

비교해야 할 값이 많아질 수록 코드는 길어집니다. 

이러한 코드를 간단하게 해결 할 수 있는방법은, 배열을 만들고 배열의 includes 함수를 사용하는 것 입니다.


```javascript
function isAnimal(name) {
  const animals = ['고양이', '개', '거북이', '너구리'];
  return animals.includes(name);
}

console.log(isAnimal('개')); // true
console.log(isAnimal('노트북')); // false
```

어떤가요? 훨씬 깔끔하죠? 


원한다면, animals 배열을 선언하는 것도 생략하고, 화살표 함수로 작성할 수도 있습니다.

```javascript
const isAnimal = name => ['고양이', '개', '거북이', '너구리'].includes(name);

console.log(isAnimal('개')); // true
console.log(isAnimal('노트북')); // false
```

물론, 코드가 짧다고 해서 무조건 좋은것은 아닙니다. 단, 코드가 짧으면서도 읽었을 때 어떤 역할을 하는지 잘 이해가 될 수 있어야 비로소 좋은 코드 입니다.


### 값에 따라 다른 결과물을 반환 해야 할 때

이번에는 주어진 값에 따라 다른 결과물을 반환해야 할 때 사용 할 수 있는 유용한 팁을 알아보겠습니다. 

예를 들어서, 동물 이름을 받아오면, 동물의 소리를 반환하는 함수를 만들고 싶다고 가정해보겠습니다.

```javascript
function getSound(animal) {
  if (animal === '개') return '멍멍!';
  if (animal === '고양이') return '야옹~';
  if (animal === '참새') return '짹짹';
  if (animal === '비둘기') return '구구 구 구';
  return '...?';
}

console.log(getSound('개')); // 멍멍!
console.log(getSound('비둘기')); // 구구 구 구
```

> if 문의 코드 블록이 한줄짜리라면 { } 를 생략 할 수도 있습니다.

만약 여기서 우리가 배운 switch case 문을 사용하여 다음과 같이 구현 할 수도 있습니다.

```javascript
function getSound(animal) {
  switch (animal) {
    case '개':
      return '멍멍!';
    case '고양이':
      return '야옹~';
    case '참새':
      return '짹짹';
    case '비둘기':
      return '구구 구 구';
    default:
      return '...?';
  }
}

console.log(getSound('개')); // 멍멍!
console.log(getSound('비둘기')); // 구구 구 구
```

참고로 switch 문에서 return 을 할 때에는 break 를 생략해도 됩니다.

우리가 방금 구현한 코드는 큰 문제는 없지만, 이걸 깔끔하게 해결 할 방법을 알고 나면 좀 맘에 들지 않는 코드의 형태입니다.

이 코드를 더욱 깔끔하게 작성하는 방법을 알려드리겠습니다.

```javascript
function getSound(animal) {
  const sounds = {
    개: '멍멍!',
    고양이: '야옹~',
    참새: '짹짹',
    비둘기: '구구 구 구'
  };
  return sounds[animal] || '...?';
}

console.log(getSound('개')); // 멍멍!
console.log(getSound('비둘기')); // 구구 구 구
```

훨씬 더 간략하고 가독성도 좋지요? 이렇게 특정 값에 따라 반환해야 하는 값이 다른 조건이 여러가지 있을 때는 객체를 활용하면 좋습니다.

반면, 값에 따라 실행해야 하는 코드 구문이 다를 때는 어떻게 해야 할까요?

그럴 떄는 객체에 함수를 넣으면 됩니다.

```javascript
function makeSound(animal) {
  const tasks = {
    개() {
      console.log('멍멍');
    },
    고양이() {
      console.log('고양이');
    },
    비둘기() {
      console.log('구구 구 구');
    }
  };
  if (!tasks[animal]) {
    console.log('...?');
    return;
  }
  tasks[animal]();
}

getSound('개');
getSound('비둘기');
```

이것을 잘 알아두면, 앞으로 매우 쓸모 있을 것입니다.

