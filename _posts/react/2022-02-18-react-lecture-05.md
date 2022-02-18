---
title: "리엑트 공부 : 5th week"
categories:
  - react
tags:
- react
---

### useEffect

`useEffect`는 컴포넌트가 실행될 때마다 특정한 작업을 수행할 수 있도록 하는 컴포넌트다.
* 지연 이벤트 동안에 레이아웃 배치와 그리기를 완료한 후 발생합
* 함수 내부에 defendency를 설정하면 해당 값이 변화 할 때마다 실행 시킬 수 있음

```javascript
import useEffect from 'react'

const  = () => {
  import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
}
```

### 리엑트의 생애주기

![react lifecycle](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQVf6qIYlp-2sui6e4fqNr2MleCnq9N7L4dUQ&usqp=CAU)

* initialization : 컴포넌트가 state와 props가 설정됨에 따라 여행을 시작하는 단계
* mounting: 컴포넌트가 처음 랜더링 되는 상태
    * `componentWillMount()` : 컴포넌트 안에 DOM이 탑재되거나 render 메서드가 호출되기 직전. 생명주기에서 한 번 호출됨.
  * `componentDidMount()` : 컴포넌트가 DOM에 탑재된 후 호출. 생명주기에서 한 번 호출됨.

* Updating : 컴포넌트의 값이 바뀔 수 있으며 re-rendering이 일어난다. 컴포넌트 내의 state 또는 props 가 유저에 반응하여 수정될 수 있다.
  * `shouldComponentUpdate()` : 컴포넌트의 업데이트 유무에 따라 판단을 하는 함수. 특정 데이터의 상태 변화에만 재랜더링이 일어날 수 있도록 조절하게 해줌. 현재의 props와 state를 통해 데이터를 변경할 수 있도록 nextProps와 nextState 인자를 가짐.
  * `componentWillUpdate()`: 컴포넌트가 re-rendering 되기 전에 호출됨. 지금의 props와 state 값이 변한 후 데이터를 작성하고 싶다면 이 함수를 사용. 현재의 props와 state를 통해 데이터를 변경할 수 있도록 nextProps와 nextState 인자를 가짐.
  * `componentDidUpdate()` : 컴포넌트가 완전히 재랜더링 된 후 호출됨. 이 메서드는 prevProps와 prevState를 가짐