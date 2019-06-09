## 01. 카운터


첫번째로 만들어볼것은, 버튼을 클릭하면 숫자가 올라가거나 내려가는 카운터입니다. CodeSandbox 에서 새로운 Vanilla 샌드박스를 만들고, index.js 파일 내용은 비우고, index.html 을 다음과 같이 수정해보세요.

### UI 만들기


```html
<!DOCTYPE html>
<html>
  <head>
    <title>Parcel Sandbox</title>
    <meta charset="UTF-8" />
  </head>

  <body>
    <h2 id="number">0</h2>
    <div>
      <button id="increase">+1</button>
      <button id="decrease">-1</button>
    </div>

    <script src="src/index.js"></script>
  </body>
</html>
```

![](https://i.imgur.com/pD4FYbQ.png)

위와 같은 결과물이 나타났나요? 우리가 보여준 `h2` 와 `button` 태그에 `id` 값을 설정해주었는데요, 이렇게 `id` 값을 설정해주면 JavaScript 에서 쉽게 해당 DOM 을 선택 할 수 있습니다. 여기서 DOM 이란, 각 태그에 대한 정보를 지니고 있는 JavaScript 객체입니다.

### DOM 선택하기

우선, DOM 을 선택해봅시다. index.js 를 다음과 같이 수정해보세요.

```javascript
const number = document.getElementById("number");
const increase = document.getElementById("increase");
const decrease = document.getElementById("decrease");

console.log(number);
console.log(increase);
console.log(decrease);
```

![](https://i.imgur.com/8hqsuiZ.png)

각 DOM 에 내장되어있는 기능들은 [정말 다양하지만](https://developer.mozilla.org/en-US/docs/Web/API/Element) 그 중에서 중요한것 몇가지만 사용해보겠습니다.

```javascript
const number = document.getElementById("number");
const increase = document.getElementById("increase");
const decrease = document.getElementById("decrease");

console.log(number.innerText); // 내용
console.log(increase.offsetTop); // top 위치
console.log(decrease.id); // id
```

![](https://i.imgur.com/54OuPQB.png)


### 이벤트 설정하기

이제 DOM 이벤트를 설정해봅시다. 버튼들이 클릭 됐을 때 콘솔에 텍스트를 출력하는 이벤트를 설정해보겠습니다.

```javascript
const number = document.getElementById("number");
const increase = document.getElementById("increase");
const decrease = document.getElementById("decrease");

increase.onclick = () => {
  console.log("increase 가 클릭됨");
};

decrease.onclick = () => {
  console.log("decrease 가 클릭됨");
};
```
버튼들을 클릭했을 때 콘솔에 우리가 설정한 텍스트들이 출력되는지 확인해보세요.


DOM 에 이벤트를 설정 할 때에는 `on이벤트이름` 값에 함수를 설정해주면 됩니다. DOM 이벤트의 종류는 정말 [다양](https://developer.mozilla.org/ko/docs/Web/Events)합니다.

그럼 이제, 버튼들이 클릭될 때 숫자값을 올리거나 내려보겠습니다.

```javascript
const number = document.getElementById("number");
const increase = document.getElementById("increase");
const decrease = document.getElementById("decrease");

increase.onclick = () => {
  const current = parseInt(number.innerText, 10);
  number.innerText = current + 1;
};

decrease.onclick = () => {
  const current = parseInt(number.innerText, 10);
  number.innerText = current - 1;
};
```

`parseInt` 는 문자열을 숫자로 변환해주는 함수입니다. 두번째 10을 넣어준 것은, 10진수로 숫자를 받아오겠다는 의미입니다.

![](https://i.imgur.com/ssFSKEx.gif)

잘 작동하나요?


[![Edit cool-ramanujan-tqdvh](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/cool-ramanujan-tqdvh?fontsize=14)