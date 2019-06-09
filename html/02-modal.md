## 02. 모달 만들기

모달이란, 다음 이미지와 같이 기존의 내용을 가리고 나타나는 메시지박스 같은 형태의 UI 를 의미합니다.

![](https://i.imgur.com/FRt5Agc.png)

이번에는 이런 UI 를 HTML 과 JavaScript 를 사용하여 만들어보겠습니다.

우선, Codesandbox 에서 새로운 Vanilla Sandbox 를 만드세요.

그리고, index.js 를 열고 맨 위 `import "./styles.css";` 하단의 코드를 지워주세요. 이번에 우리는 스타일링을 할 것이기 때문에 css 를 불러와야 합니다. 

그 다음에, index.html 을 열어서 다음과 같이 수정해보세요.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Parcel Sandbox</title>
    <meta charset="UTF-8" />
  </head>

  <body>
    <h1>안녕하세요!</h1>
    <p>내용내용내용</p>
    <button>버튼 열기</button>
    <script src="src/index.js"></script>
  </body>
</html>
```


![](https://i.imgur.com/q6IowoG.png)

이렇게 화면이 나타났나요?

그 다음엔, 버튼 아래에 다음 내용을 보여주세요.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Parcel Sandbox</title>
    <meta charset="UTF-8" />
  </head>

  <body>
    <h1>안녕하세요!</h1>
    <p>내용내용내용</p>
    <button>버튼 열기</button>
    <div class="modal-wrapper">
      <div class="modal">
        <div class="modal-title">안녕하세요</div>
        <p>모달 내용은 어쩌고 저쩌고..</p>
        <div class="close-wrapper">
          <button>닫기</button>
        </div>
      </div>
    </div>
    <script src="src/index.js"></script>
  </body>
</html>
```

그러면 다음과 같이 보여질텐데요

![](https://i.imgur.com/H05agKs.png)

여기에 CSS 로 스타일링을 해보겠습니다.

src 디렉터리 안에 들어있는 styles.css 파일을 열어서 다음과 같이 수정해보세요.

```css
body {
  font-family: sans-serif;
}

.modal-wrapper {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  background: white;
  padding: 24px 16px;
  border-radius: 4px;
  width: 320px;
}

.modal-title {
  font-size: 24px;
  font-weight: bold;
}

.modal p {
  font-size: 16px;
}

.close-wrapper {
  text-align: right;
}
```

그럼 다음과 같이 나타날 것입니다.

![](https://i.imgur.com/FRt5Agc.png)

### display 스타일을 사용하여 모달 열고 닫기

이제 모달을 열고 닫는 기능을 구현해보겠습니다. 방법은 굉장히 간단한데요, 바로 `display` 스타일을 사용하는 것 입니다. index.html 을 다음과 같이 수정해보세요. .modal-wrapper 쪽에는 인라인 스타일이 추가되었고, 각 버튼에 `id` 가 붙었습니다.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Parcel Sandbox</title>
    <meta charset="UTF-8" />
  </head>

  <body>
    <h1>안녕하세요!</h1>
    <p>내용내용내용</p>
    <button id="open">버튼 열기</button>
    <div class="modal-wrapper" style="display: none;">
      <div class="modal">
        <div class="modal-title">안녕하세요</div>
        <p>모달 내용은 어쩌고 저쩌고..</p>
        <div class="close-wrapper">
          <button id="close">닫기</button>
        </div>
      </div>
    </div>
    <script src="src/index.js"></script>
  </body>
</html>
```

`display: none;` 스타일을 사용하게 되면 해당 엘리먼트는 화면에서 숨겨지게됩니다.


이제, index.js 를 열어서 버튼과 모달의 DOM 을 선택해주고, 클릭 이벤트를 설정해주세요

```javascript
import "./styles.css";

const open = document.getElementById("open");
const close = document.getElementById("close");
const modal = document.querySelector(".modal-wrapper");
open.onclick = () => {
  modal.style.display = "flex";
};
close.onclick = () => {
  modal.style.display = "none";
};
```

`id` 가 아닌 클래스로 DOM을 선택하고 싶을땐 `document.getElementsByClassName` 또는 `document.querySelector` 를 사용하면 됩니다. `document.querySelector` 를 사용하여 class 값으로 DOM 을 선택 할 때에는 텍스트 앞에 `.` 을 붙여주어야 합니다.


이제 버튼들을 눌러보세요. 잘 작동하나요?

![](https://i.imgur.com/0MqEVWr.gif)

[![Edit vigorous-shadow-dx22s](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/vigorous-shadow-dx22s?fontsize=14)

