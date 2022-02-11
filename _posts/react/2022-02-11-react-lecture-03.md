---
title: "리엑트 공부 : 3rd week"
categories:
  - react
tags:
- react
---

### 반응 속도 게임 만들기

##### React에서의 조건문
- 리엑트에서는 `for`나 `if`문 사용을 하지 않는다 👉 삼항연산자 혹은 AND 연산자를 대신 사용함

```javascript
{this.state.result.length === 0 ? null : <div>평균 시간: {this.state.result.reduce((a, c) => a + c) / this.state.result.length}ms</div>}
```

##### useRef

이거 진심 처음 보는 녀석이었음... 리엑트는 오른손에 `useState` 왼손에 `useEffect`로 해결하는 녀석이 아니었던거임?

* 특정 DOM을 선택할 수 있게끔 해주는 기능을 가짐
* 함수형 컨포넌트에서 ref를 사용할 때에는 useRef라는 Hooks함수를 사용
* 랜더링 할 때마다 매 번 동일한 객체를 제공해줌
* useRef는 `current` 속성을 가지는데 상태가 변경되어도 React 컴포넌트가 재랜더링 되지 않음

```javascript
const refContainer = useRef(initialValue);
```

```javascript
// 공식문서에서 가져온 사용 예시
function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  const onButtonClick = () => {
    // `current` points to the mounted text input element
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```