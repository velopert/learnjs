## 01. Hello JavaScript!

자바스크립트는 여러분의 브라우저에서 언제든지 사용 할 수 있습니다. 만약 현재 여러분이 크롬브라우저가 아닌 다른 브라우저를 사용중이라면 크롬을 설치하여 실행해보세요. 그리고 개발자 도구를 열어보세요.

개발자 도구는 윈도우 Ctrl + Shift + I 또는 macOS Command + Option + I 키를 눌러서 열 수 있습니다.

> Safari, FireFox 에도 개발자 도구가 있습니다. 단, 이 튜토리얼에서는 크롬을 사용하기에 크롬 설치를 권장드립니다.

크롬 개발자 도구에서 Console 탭을 열고 입력창에 다음 코드를 입력해보세요.

```javascript
console.log('Hello JavaScript!');
```

![](https://i.imgur.com/xA2b56x.png)

위 이미지와 같이 Hello JavaScript! 가 보여졌나요?

여기서 `console.log` 는 콘솔에 특정 내용을 출력하라는 것을 의미합니다.

이번에는 조금 다른걸 해볼까요?

다음 코드를 한번 입력해보세요.

```javascript
console.log(1 + 2 + 3 + 4);
```

10 이라는 결과물이 나타났나요?

우리는 이렇게 JavaScript 를 통하여 연산을 할 수도 있답니다.

그런데 아무래도 매번 코드를 작성 할 때마다 크롬 개발자 도구에서 하는 것은 조금 불편합니다.

그래서, 여러분께 유용한 웹사이트를 소개드려볼까 합니다.

바로 [CodeSandbox](https://codesandbox.io) 이라는 사이트인데요, 코드를 작성하고 바로 결과물을 확인 할 수 있는 서비스입니다.

위 링크를 열고 우측 상단의 Create Sandbox 를 누르세요.

![](https://i.imgur.com/a0xc3s2.png)

그 다음에 Vanilla 를 선택하세요. Vanilla 는, 다른 라이브러리 없이 자바스크립트만 사용하겠다는 의미입니다.

![](https://i.imgur.com/rmGGFI1.png)

다음과 같은 에디터가 나타날텐데, 상단에 Fork 버튼을 누르세요.

![](https://i.imgur.com/QcpNUR9.png)

그 다음,

index.js 파일의 내용을 다 지우고 다음 코드를 입력해보세요.

```javascript
console.log('안녕하세요!');
console.log('JavaScript 를 배워봅시다');
```

그 다음에 우측의 Console 을 누르시면 결과물이 나타납니다.

![](https://i.imgur.com/QPqvmW8.png)

흰 페이지는 HTML 결과물을 보여주는 곳인데, 지금은 필요 없으니 이렇게 Console 창을 드래그하여 위로 쭉 끌어 올려주세요.

![](https://i.imgur.com/g3NRbuj.gif)

또는 이렇게 할 수도 있습니다.

![](https://i.imgur.com/TAjKRUv.gif)

이렇게 콘솔 탭을 옮기고 나서 다시 자바스크립트를 실행하려면, 코드에 변화를 주어야 합니다 (위 화면에서는 JavaScript 를 배워봅시다 뒤에 느낌표를 찍었습니다.)

이제 여러분은 JavaScript 를 작성하고, 실행 할 준비가 되었습니다!

> CodeSandbox 에서는 코드 테마도 바꿀 수 있답니다.
> ![](https://i.imgur.com/DHETwEp.png)
