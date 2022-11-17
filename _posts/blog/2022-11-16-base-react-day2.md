---
title: "REACT 기초 다시 정리 : 2일차"
categories:
  - react
tags:
  - react
  - basic
---
# REACT 기초 : 2일차


### ref
* html에서 `id를 사용하듯이`, 리액트 내부에서 DOM에 이름을 다는 방법. state만으로는 해결할 수 없는, DOM을 꼭 직접적으로 건들여야 할 때 사용한다.
	* 포커스, 텍스트 선택영역, 혹은 미디어의 재생을 관리할 때.
	* 애니메이션을 직접적으로 실행시킬 때.
	* 서드 파티 DOM 라이브러리를 React와 같이 사용할 때.
* 전역적으로 작동하지 않고 컴포넌트 내부에서만 작동하기 때문에 중복 id 생성과 같은 이슈에서 자유롭다.
* * 함수 컴포넌트는 인스턴스가 없기 때문에 **함수 컴포넌트에 ref 어트리뷰트를 사용할 수 없음**.
* 함수 컴포넌트에 ref를 사용할 수 있도록 하려면,  [forwardRef](https://ko.reactjs.org/docs/forwarding-refs.html)  (높은 확률로  [useImperativeHandle](https://ko.reactjs.org/docs/hooks-reference.html#useimperativehandle) 와 함께)를 사용하거나 클래스 컴포넌트로 변경할 수 있음.

###### callback 함수를 활용한 방법
* ref를 달고자 하는 요소에 ref라는 callback 함수를 props로 전달. 이 콜백 함수는 ref 값을 파라미터로 전달 받음.

```javascript
<input ref = {(ref) => {this.input = ref}} />
// this.input은 unput 요소의 DOM으로 지정됨.
```

###### createRef를 통한 설정

* 16 이후 버전부터는 다음과 같은 방법을 통해서 만들라고 함.

```javascript
import React, {Component} from 'react';

class RefSample extends Component{
  input = React.createRef(); // ref props 달기

  handleFocus = () => {
    this.input.current.focus();
  }

  render() {
    return(
      <div>
        <input ref={this.input} />
      </div>
    )
  }
}

export default RefSample;
```

###### 컴포넌트에서 ref 사용하기

**check**
* clientHeight 는 요소의 내부 높이입니다. 패딩 값은 포함되며, 스크롤바, 테두리, 마진은 제외됩니다.
* offsetHeight 는 요소의 높이입니다. 패딩, 스크롤 바, 테두리(Border)가 포함됩니다. 마진은 제외됩니다.
* scrollHeight  는 요소에 들어있는 컨텐츠의 전체 높이입니다. 패딩과 테두리가 포함됩니다. 마진은 제외됩니다.

https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F9940E34F5EE2947508

**scrollBox.js**
```javascript
import React, {Component} from 'react';

class ScrollBox extends Component{

  scrollToBottom = () => {
    const {scrollHeight, clientHeight} = this.box;

    // 위 구조분해 할당 코드와 동일한 코드
    // const scrollHeight = this.box.scrollHeight;
    // const clientHeight = this.box.clientHeight;

    this.box.scrollTop = scrollHeight - clientHeight;
  }


  render(){
    const style = {
      border:'1px solid black',
      height:'300px',
      width:'300px',
      overflow:'auto',
      position:'relative'
    }

    const innerStyle = {
      width: '100%',
      height:'650px',
      background:'linear-gradient(white, black)'
    }

    return(
      <div style={style} ref={(ref) => {this.box = ref}}>
        <div style={innerStyle}></div>
      </div>
    )
  }
}

export default ScrollBox;
```

**App.js**
* 클래스형으로 변경한 줄도 모르고 개삽질함
```javascript
import React, { Component } from "react";
import ScrollBox from "./ScrollBox";

class App extends Component {
  // return <MyClassComponent>헬로우</MyClassComponent>;
  render(){
    return (
      <div>
        <ScrollBox ref={(ref) => (this.scrollBox = ref)} />
        <button onClick={() => this.scrollBox.scrollToBottom()}>to bottom</button>
      </div>
    );
  }
}

export default App;
```


###### conclusion
컴포넌트 내부에서 DOM에 직접 접근해야 할 때는 ref를 사용한다. 단 ref를 사용하지 않고는 도저히 기능 구현이 어렵다고 판단될 때만 사용하는 것이 좋다고 강조 또 강조됨.

### 컴포넌트 반복
###### map함수
* 배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환함
```javascript
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```

vue와 동일하게, 고유한 key 값을 넣어주어야 한다. -> 컴포넌트 배열이 랜더링 되었을 때 어떤 원소에 변경이 생겼는지 알아내기 위해 사용.
```javascript
const IterationSample = () => {
  const names = ['mina', 'sana', 'momo'];
  const nameList = names.map((name, index) => <li key={index}>{name}</li>)
  return <ul>{nameList}</ul>
}

export default IterationSample;
```

###### 데이터 추가 기능의 구현
```javascript
import React, {useState} from 'react';

const IterationSample = () => {
  const [names, setNames] = useState([
    {id:1, text:'사나'},
    {id:2, text:'미나'},
    {id:3, text:'모모'}
  ]);
  const [inputText, setInputText] = useState('');
  const [nextId, setNextId] = useState(4);

  const onChange = e => {
    // 키보드에 입력한 값!
    setInputText(e.target.value);
  }

  const onClick = () => {
    // 새로운 object를 넣은 배열을 반환
    const nextNames = names.concat({
      id:nextId,
      text:inputText
    })
    // key값을 하나 늘려줌
    setNextId(nextId + 1);
    // names 배열을 방금 concat을 통해 만든 배열로 바꿔치기
    setNames(nextNames);
    setInputText('')
  }

  const nameList = names.map((name) => <li key={name.id}>{name.text}</li>)
  return (<>
  <input value={inputText} onChange={onChange} />
  <button onClick={onClick}>추가</button>
  <ul>{nameList}</ul>
  </>
  )
}

export default IterationSample;
```

###### filter
뭘 하든 `불변성을 유지하면서 업데이트`를 해주어야 한다.

```javascript
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```

###### filter를 활용한 삭제 기능 구현
```javascript
import React, {useState} from 'react';

const IterationSample = () => {
  const [names, setNames] = useState([
    {id:1, text:'사나'},
    {id:2, text:'미나'},
    {id:3, text:'모모'}
  ]);
  const [inputText, setInputText] = useState('');
  const [nextId, setNextId] = useState(4);

  const onChange = e => {
    // 키보드에 입력한 값!
    setInputText(e.target.value);
  }

  const onClick = () => {
    // 새로운 object를 넣은 배열을 반환
    const nextNames = names.concat({
      id:nextId,
      text:inputText
    })
    // key값을 하나 늘려줌
    setNextId(nextId + 1);
    // names 배열을 방금 concat을 통해 만든 배열로 바꿔치기
    setNames(nextNames);
    setInputText('')
  }

  const onRemove = id => {
    const nextNames = names.filter(name => name.id !== id);
    setNames(nextNames);
  }

  const nameList = names.map((name) => <li key={name.id} onDoubleClick={()=>{onRemove(name.id)}}>{name.text}</li>)
  return (<>
  <input value={inputText} onChange={onChange} />
  <button onClick={onClick}>추가</button>
  <ul>{nameList}</ul>
  </>
  )
}

export default IterationSample;
```


### 라이프 사이클
📍 참고자료 :  [25. LifeCycle Method · GitBook](https://react.vlpt.us/basic/25-lifecycle.html)
##### mount
`mount` : DOM이 생성되고 웹 브라우저 상에 나타나는 상태.
###### mount에서의 라이프 사이클 메서드
 * `constructor` : 컴포넌트를 새로 만들 때마다 호출되는 클래스 생성자, 초기 `state`를 정할 수 있다.
```javascript
constructor(props){...}
```
 * `getDerivedStateFromProps`:prop에 있는 값을 state에 넣을 때(동기화) 사용하는 메서드
	 * 다른 생명주기 메서드와는 달리 앞에 static 을 필요로 하고, 이 안에서는 this 롤 조회 할 수 없음.
	 * 특정 객체를 반환하게 되면 해당 객체 안에 있는 내용들이 컴포넌트의 state 로 설정이 됨.
	 * null 을 반환하게 되면 아무 일도 발생하지 않습니다.
```javascript
  static getDerivedStateFromProps(nextProps, prevState) {
    console.log("getDerivedStateFromProps");
    if (nextProps.color !== prevState.color) {
      return { color: nextProps.color };
    }
    return null;
  }
```
 * `render`: UI를 랜더링 하는 메서드 (당연하다…)
	* 컴포넌트의 모양을 정의한다.
	* `this.props`와 `this.state`에 접근할 수 있으며 리엑트 요소를 반환한다.
	* 이 메서드 안에서는 이벤트 설정이 아닌 곳에서 `setState`를 사용해서는 안되며, 브라우저의 DOM에 접근해서는 안된다. -> DOM 정보를 가져오거나 `state`에 변화를 줄 때는 `componentDidMount`에서 처리해야 함.
 * `componentDidMount`: 컴포넌트가 웹 브라우저 상에 나타난 후 호출하는 메서드
	 * 자바스크립트 라이브러리 혹은 프레임워크 함수를 호출하거나 이벤트 등록, setTimeout 등등의 비동기 작업을 처리하면 됨.

##### update
###### 컴포넌트에서 업데이트가 일어나는 경우
* 부모 컴포넌트에서 넘겨주는  `props`가 바뀔 때
* 컴포넌트 자신이 들고 있는 `state` 가 바뀔 때
* 부모 컴포넌트가 리랜더링 될 때
* `this.forceUpdate`를 통해 강제로 랜더링을 트리거 할 때

###### 업데이트에서의 라이프 사이클 메서드
* `getDerivedStateFromProps`메서드의 경우 마운트 과정에서도 호출 되지만, 업데이트가 시작하기 전에도 호출된다. -> props의 변화에 따라 state 값에 변화를 주고 싶을 때 활용하기 유용하다.
* `shouldComponentUpdate` : 컴포넌트가 리랜더링 되어야 할지 말아야 할지를 결정하는 메서드. 이 메서드에는 boolean 값을 반환해야 함.
	* true가 반환되었을 때 라이프 사이클 메서드를 계속 실행, false일 경우 작업을 중지(리랜더링X) -> 컴포넌트를 최적화 할 때 사용.
	* 만약 특정 함수에서 `this.forceUpdate`를 호출하면 이 과정을 생략하고 `render`함수를 호출
	* 이 메서드 안에서는 `props`와 `state`는 `this`를 통해 접근 가능함. 새로 설정된 `props`와 `state`는 `nextProps`와 `nextState`를 통해 접근 가능하다.
```javascript
  shouldComponentUpdate(nextProps, nextState) {
    console.log("shouldComponentUpdate", nextProps, nextState);
    // 숫자의 마지막 자리가 4면 리렌더링하지 않습니다
    return nextState.number % 10 !== 4;
  }
```
* `render` : 컴포넌트를 리랜더링 (당연함…)
* `getSnapshotBeforeUpdate` : 컴포넌트 변화를 DOM에 반영하기 바로 직전에 호출하는 메서드
	* 리엑트 16.3 이후부터 만들어진 메서드.
	* `render`에서 만들어진 결과물이 브라우저에 노출되기 직전에 호출.
	* 이 메서드에서 반환하는 값은 해당 메서드의 세번째 파라미터인 `snapshot`을 통해 전달받을 수 있다. -> 업데이트 직전의 값을 참고할 일이 있을 때 활용.
```javascript
  getSnapshotBeforeUpdate(prevProps, prevState) {
    console.log("getSnapshotBeforeUpdate");
    if (prevProps.color !== this.props.color) {
      return this.myRef.style.color;
    }
    return null;
  }
```
* `componentDidUpdate` : 컴포넌트의 업데이트 작업이 끝난 후 호출하는 메서드.
	* 리랜더링이 완료된 후 실행되므로 DOM에 접근 가능!
	* 컴포넌트가 이전에 가졌던 데이터를 `prevProps` 및 `prevState`를 통해 접근 가능. `getSnapshotBeforeUpdate`에서 전달받은 값이 있다면, `snapshot`을 통해 전달 받을 수 있음.
```javascript
  componentDidUpdate(prevProps, prevState, snapshot) {
    console.log("componentDidUpdate", prevProps, prevState);
    if (snapshot) {
      console.log("업데이트 되기 직전 색상: ", snapshot);
    }
  }
```

#####  unmount
컴포넌트를 DOM에서 제거하는 과정.
###### 언마운트에서의 라이프 사이클 메서드
* `componentWillUnmount` 컴포넌트가 웹 브라우저 상에서 사라지기 전에 호출하는 메서드.
	* 이벤트, 타이머, 직접 생성한 DOM을 해당 과정에서 제거해 줘야함

##### error
`componentDidCatch ` : 컴포넌트 랜더링 도중 에러가 발생했을 때, 오류 UI를 발생시키게 해준다.
```javascript
  componentDidCatch(error, info) {
    // Example "componentStack":
    //   in ComponentThatThrows (created by App)
    //   in ErrorBoundary (created by App)
    //   in div (created by App)
    //   in App
    logComponentStackToMyService(info.componentStack);
  }
```


### react HOOKS
###### useState
* `useState`는 한번에 하나의 상태값만 관리할 수 있다.
* 관리할 상태가 여러개라면 그냥 여러번 사용하면 됨.

###### useEffect
* 리액트 컴포넌트가 랜더링 될 때마다 특정 작업을 수행할 수 있도록 설정
* `useEffect`의 첫번째 파라미터는 마운트 시에, 두번째 파라미터는 업데이트 시에 동작되므로, 처음 랜더링 될 때에만 실행시키고 싶을 때는 빈 배열을 넣어주면 된다.

###### useReducer
* `useState`보다 더 다양한 컴포넌트 상황에 따라 다양한 상태를 다른 값으로 업데이트 해주고 싶을 때 사용하는 Hook.
* 컴포넌트의 상태 업데이트 로직을 컴포넌트에서 분리시킬 수 있음
* 상태 업데이트 로직을 컴포넌트 바깥에 작성 할 수도 있음
* 다른 파일에 작성 후 불러와서 사용 할 수 있음 -> 코드의 가독성 증가
```javascript
function reducer(state, action) {
  // 새로운 상태를 만드는 로직
  // const nextState = ...
  return nextState; // reducer에서 반환하는 값이 곧 state의 새로운 상태.
}
```

###### 코드 예시
```javascript
import React, { useReducer } from 'react';

function reducer(state, action) {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    case 'DECREMENT':
      return state - 1;
    default:
      return state;
  }
}

function Counter() {
  // useReducer(리듀서 함수, 기본값)
  const [number, dispatch] = useReducer(reducer, 0);

  const onIncrease = () => {
    dispatch({ type: 'INCREMENT' });
  };

  const onDecrease = () => {
    dispatch({ type: 'DECREMENT' });
  };

  return (
    <div>
      <h1>{number}</h1>
      <button onClick={onIncrease}>+1</button>
      <button onClick={onDecrease}>-1</button>
    </div>
  );
}

export default Counter;
```

### useMemo
* 함수 내부에서 발생하는 연산을 최적화 할 수 있다. -> 랜더링 하는 과정에서 특정 값이 바뀌었을 때만 연산을 실행하고, 원하는 값이 바뀌지 않았다면 이전 연산 결과를 그대로 활용한다.

다음 코드에서 useMemo를 사용해, 리스트 내부의 값이 변경 되었을 때만 getAverage함수를 불러오도록 설정할 수 있다.

```javascript
import React, {useState, useMemo} from 'react';

const getAverage = numbers => {
  console.log("평균을 계산 중입니다...");
  if(numbers.length === 0){
    return 0;
  }
  const sum = numbers.reduce((a, b) => a+b);
  return sum / numbers.length;
}

const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState('');

  const onChange = e => {
    setNumber(e.target.value);
  }

  const onInsert = e => {
    const nextList = list.concat(parseInt(number));
    setList(nextList);
    setNumber('')
  }

  const avg = useMemo(() => getAverage(list), [list])

  return(<div>
    <input value={number} onChange={onChange} />
    <button onClick={onInsert}>등록</button>
    <ul>
      {list.map((value,index) => (<li key={index}>{value}</li>))}
    </ul>
    // <div>{getAverage(list)}</div> 대신!
    <div>{avg}</div>
  </div>)
}


export default Average;
```

###### useCallback
`useMemo`와 비슷한 역할을 한다. 랜더링 성능을 최적화 해야 할 때 자주 씀. -> 만들어놨던 함수를 재사용 할 수 있다.

* useCallback의 첫번째 파라미터에는 생성하고 싶은 함수를 넣고, 두번째 파라미터에는 배열을 넣는다. -> 배열에는 어떤 값이 바뀌었을 때 함수를 새로 작성해야하는지  명시해야 한다.

###### useRef
함수 컴포넌트에서 ref를 사용할 수 있도록 해준다. -> useRef를 사용해서 ref를 만들면 이를 통해 만든 객체 안의 current값이 실제 엘리먼트를 가리킨다.

```javascript
import React, {useState, useMemo, useCallback, useRef} from 'react';

const getAverage = numbers => {
  console.log("평균을 계산 중입니다...");
  if(numbers.length === 0){
    return 0;
  }
  const sum = numbers.reduce((a, b) => a+b);
  return sum / numbers.length;
}

const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState('');
  const inputEl = useRef(null);

  const onChange = useCallback(e => {
    setNumber(e.target.value);
  }, [])

  const onInsert = e => {
    const nextList = list.concat(parseInt(number));
    setList(nextList);
    setNumber('')
  }

  const avg = useMemo(() => getAverage(list), [list])

  return(<div>
    <input value={number} onChange={onChange} ref={inputEl}/>
    <button onClick={onInsert}>등록</button>
    <ul>
      {list.map((value,index) => (<li key={index}>{value}</li>))}
    </ul>
    <div>{avg}</div>
  </div>)
}


export default Average;
```