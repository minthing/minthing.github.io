---
title: "REACT 기초 다시 정리 : 1일차"
categories:
  - react
tags:
  - react
  - basic
---
# REACT 기초 : 1일차


### 리엑트란

리엑트는 프레임워크가 아닌 라이브러리. 오로지 뷰만을 담당하므로 나머지 부분은 직접 구현해야함.

### virtual dom

리엑트는 Virtual DOM을 사용한다 -> 큰 규모의 어플리케이션을 다룰 때, DOM을 최소한으로 조작하기 위해서 DOM의 업데이트를 추상화 한다.

### 적용과정

- 데이터가 업데이트 되면 전체 UI를 Virtual DOM에 리랜더링.
- 이전 Virtual DOM에 있던 내용과 현재 내용을 비교.
- 바뀐 부분을 실제 DOM에 적용.

참고 : [(번역) 블로그 답변: React 렌더링 동작에 대한 (거의) 완벽한 가이드](https://velog.io/@superlipbalm/blogged-answers-a-mostly-complete-guide-to-react-rendering-behavior)

### setting

- note: 노드 버전 14 이상을 요구. -> ~~생각보다 설치가 매우 오래걸림. 예전에 공부할때도 이랬나?~~

```jsx
npm install -g create-react-app
create-react-app my-app
```

Vue 프로젝트가 먼저 포트 3000을 차지하고 있으므로, `package.json`을 만져주었다.

```jsx
  "scripts": {
    "start": "export PORT=3001 && react-scripts start",
	...
  },
```

### JSX

리액트에서는 JSX라는 문법을 사용. 해당 코드는 브라우저에서 실행되기 전 바벨에서 임의로 자바스크립트 형태의 코드로 변환함. -> 가독성과 활용도를 높일 수 있음.

- note: 문법 자체는 Vue와 비슷하다. 최상위 wrapper가 필요하다는 점과 내부에서 조건문 사용하는 방식도 비슷…
    - 리엑트 네이티브 공부할 때 스타일에서 카멜 케이스 쓴 거 리액트 문법이었구나.

### 컴포넌트

리엑트의 컴포넌트에는 `함수형 컴포넌트`와 `클래스형 컴포넌트`가 있다.

### 함수형 컴포넌트의 예시

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

### class형 컴포넌트의 예시

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

### what’s the difference?

**함수형 컴포넌트**

- 선언 하기가 훨씬 편하다.
- 메모리 자원이 비교적 적음. (Remarkable하지는 않음)
- state 기능 및 라이프 사이클 기능을 사용할 수 없음 -> Hooks라는 기능을 통해 일부 해결됨.

**클래스형 컴포넌트**

- state 기능 및 라이프 사이클 기능을 사용할 수 있다.
- 임의의 메서드를 정의할 수 있다.
- 랜더 함수가 반드시 존재해야 하며, 그 안에서 보여주어야 할 JSX를 반환해야 한다.

### props

- 컴포넌트가 사용되는 과정에서 부모 컴포넌트가 설정하는 값.
- 컴포넌트에서는 해당 props를 읽기 전용으로만 사용할 수 있으며, 바꾸기 위해서는 부모 컴포넌트에서 설정해야 한다.
- MyComponent.js

```jsx
const MyCompoennt = (props) => {
  return <div>안녕 나의 {props.name} 컴포넌트</div>;
}

// 하단에 다음과 같이 default를 지정할 수 있음
MyComponent.defaultProps = {
  name: '리액트'
}

export default MyCompoennt;
```

- App.js

```jsx
import MyCompoennt from './MyComponent';

function App() {
  return <MyCompoennt name="react" />;
}

export default App;
```

- 추가 ) 컴포넌트 태그 사이에 있는 내용을 보여주는 props : children
- > 보통 비구조화 할당해서 씀. ~~난 왜 이 용어가 어렵지?~~`const MyCompoennt = ({name, children}) => {...}`

### propsTypes

필수 props를 지정하거나, 타입을 지정할 때 사용. 코드 상단에 import 해야 함.

```jsx
import PropsTypes from 'prop-types';

//...

MyComponent.PropsTypes = {
  name: PropsTypes.string.isRequired
}
```

다음 과정을 클래스 컴포넌트를 통해 표현하면 다음과 같다.

```jsx
import {React, Component} from 'react';
import PropTypes from 'prop-types';

class MyClassComponent extends Component{
  static defaultProps ={
    name:'class'
  };
  static propTypes = {
    name: PropTypes.string,
  };
  render(){
    const {name, favoriteNumber, children} = this.props;
    return (<div>안녕 나의 {name} 컴포넌트<br/>{children}</div>);
  }
}

export default MyClassComponent;
```

### state

- 컴포넌트 내부에서 바뀔 수 있는 값.
- constructor라는 컴포넌트 생성자를 통해 state의 초깃값을 생성하며, `super(props)`를 반드시 호출해 주어야 한다.
- render 함수에서 state를 조회할 때는 `this.state`를 통해 조회하면 된다.
- state의 값을 변환시키고 싶을 때는 `this.setState`를 사용한다 -> 내부에서 참조한 값만을 변화시킨다.

```jsx
// Counter.js
import {React, Component} from 'react';

class Counter extends Component{
  constructor(props){
// 컴포넌트 생성자 메서드
    super(props);
    this.state={
      number: 0,
      fixedNumber:0
    }
  }

  render(){
    const {number, fixedNumber} = this.state;
    return(
      <div>
        <h1>{number}</h1>
        <h2>{fixedNumber}</h2>
        <button onClick = {() => {
          this.setState({number: number + 1})
        }}>Click ME!</button>
      </div>
    )
  }
}

export default Counter;
```

### better way

```jsx
import {React, Component} from 'react';

class Counter extends Component{

  state = {
    number:0,
    fixedNumber:0
  }

  render(){
    const {number, fixedNumber} = this.state;
    return(
      <div>
        <h1>{number}</h1>
        <h2>{fixedNumber}</h2>
        <button onClick = {() => {
          this.setState({number: number + 1})
        }}>Click ME!</button>
      </div>
    )
  }
}

export default Counter;
```

### setState 좀 더 알아보기

- `this.setState` 를 통해 값을 업데이트 시킬 때는 상태가 비동기적으로 업데이트 된다. -> onClick 내에 setState를 두 번 호출해도 값은 1번 호출할 때와 동일하게 바뀐다.
- 해결 : **객체 대신 인자로** 넣어준다.
    - prevState: 지난 상태
    - props는 현재 지니고 있는 상태를 나타낸다.

```jsx
this.setState({prevState, props}=> {
    return { //...}
    }
  }
)
```

**적용 시**

```jsx
import {React, Component} from 'react';

class Counter extends Component{

  state = {
    number:0,
    fixedNumber:0
  }

  render(){
    const {number, fixedNumber} = this.state;
    return(
      <div>
        <h1>{number}</h1>
        <h2>{fixedNumber}</h2>
        {/* <button onClick = {() => {
          this.setState({number: number + 1})
        }}>Click ME!</button> */}
        <button onClick = {() => {
          this.setState(prevState => ({number: prevState.number + 1}))
          this.setState(prevState => ({number: prevState.number + 1}))
        }}>Click ME!</button>
      </div>
    )
  }
}

export default Counter;
```

### callback

setState를 통해 값을 업데이트 한 후 특정 작업을 시행하고 싶을 때, 두번째 파라미터르 callback 함수를 등록하면 된다.

```jsx
import {React, Component} from 'react';

class Counter extends Component{

  state = {
    number:0,
    fixedNumber:0
  }

  render(){
    const {number, fixedNumber} = this.state;
    return(
      <div>
        <h1>{number}</h1>
        <h2>{fixedNumber}</h2>
        {/* <button onClick = {() => {
          this.setState({number: number + 1})
        }}>Click ME!</button> */}
        <button onClick = {() => {
          this.setState(
            prevState => (
              {number: prevState.number + 1}
              ),
              () => {
                console.log('state가 호출되었습니다.');
                console.log(this.state)
              }
            )
        }}>Click ME!</button>
      </div>
    )
  }
}

export default Counter;

```

### 함수 컴포넌트에서의 useState

함수 컴포넌트에서는 useState라는 함수를 불러와  사용한다.

- useState 함수의 인자에는 상태의 초깃값을 넣어준다. 반드시 객체일 필요는 없고 숫자, 문자열, 객체, 배열 등등 가능.

```jsx
import React, {useState} from 'react';

const Say = () => {
  const [message, setMessage] = useState('');
  const onClickEnter = () => {
    setMessage('hello');
  }
  const onClickLeave = () => {
    setMessage('bye')
  }
  const [color, setColor] = useState('black');

  return (
    <div>
      <button onClick = {onClickEnter}>입장</button>
      <button onClick = {onClickLeave}>퇴장</button>
      <h1 style={{color}}>{message}</h1>
      <button onClick={() => setColor('green')}>green</button>
      <button onClick={() => setColor('blue')}>blue</button>
    </div>
  )
}

export default Say;
```

### state를 사용할 때의 주의

- state의 값을 바꿔야 할 때는 setState 혹은 useState를 통해 전달받은 세터 함수를 사용해야 한다.
- 배열이나 객체를 업데이트 해야 할 때 -> 배열이나 객체의 사본을 만들고 그것을 setState 혹은 세터 함수를 통해 업데이트
    - 리액트에서는 state 의 변경을 감지하고, 변경된 부분을 리렌더링을 하는데 setState (또는 useState 의 세터 함수)를 사용하지 않고 직접 state 값을수정할 경우 변경을 감지하지 못하기 때문

**잘못된 예시**

```jsx
// 클래스형 컴포넌트
this.state.number = this.state.number + 1;
this.state.array = this.array.push(2);
this.state.object.value = 5;
// 함수형 컴포넌트
const [object, setObject] = useState({a: 1, b: 1});
object.b = 2;
```

```jsx
 // 사본을 만들어서 업데이트

const object = {a: 1, b: 2, c: 3};
const nextObject = {...object, b: 2};
// {...object}를 활용해서 새로운 객체를 만들고 b를 덮어쓰고 있음.

// 배열 다루기
const array = [
	{ id: 1, value: true },
	{ id: 2, value: true },
	{ id: 3, value: false}
];
let nextArray = array.concat({ id: 4 });
// 새 항목 추가 concat -> 인자로 주어진 배열이나 값들을 기존 배열에 합쳐서 새 배열을 반환
nextArray.filter(item => item.id !== 2); // id가 2인 항목 제거
nextArray.map(item => (item.id === 1 ? { ...item, value: false } : item));
// id가 1인 항목의 value를 false로 변환, 사본을 만든다는 점은 위와 같음

{/*
	객체에 대한 사본을 만들 때는 spread 연산자라 불리는 ...을 사용하여 처리하고,
	배열에 대한 사본을 만들 때는 배열의 내장 함수들을 활용함.
*}
```

### 리액트의 이벤트 시스템
* DOM 요소에만 이벤트를 설정할 수 있다. -> 컴포넌트에 직접 이벤트를 건다면, 그것은 이벤트를 컴포넌트에 전달해 줄 뿐이다.

```javascript
import React, {Component} from 'react';

class EventPractice extends Component{
  render(){
    return(
      <div>
        <h1>let's practice event!</h1>
        <input type="text" name="message" placeholder='write something...' onChange={(e) => {console.log(e)}} />
      </div>
    )
  }
}

export default EventPractice;
```
위 콘솔의 결과는 다음과 같다.

```javascript
SyntheticBaseEvent {_reactName: 'onChange', _targetInst: null, type: 'change', nativeEvent: InputEvent, target: input, …}
```

여기서 `SyntheticBaseEvent`는 웹 브라우저의 네이티브 이벤트를 감싸는 객체로, 네이티브 이벤트와 인터페이스가 같으므로 순수 자바스크립트의 이벤트와 동일하게 다루면 된다. -> BUT, 이것은 이벤트가 끝나고 나면 초기화 되므로 비동기적 이벤트를 참조할 일이 있을 땐 `e.persist()`를 사용하면 된다.

```javascript
import React, {Component} from 'react';

class EventPractice extends Component{

  state = {
    message: ''
  }

  render(){
    return(
      <div>
        <h1>let's practice event!</h1>
        <input
          type="text"
          name="message"
          placeholder='write something...'
          value={this.state.message}
          onChange={(e) => {this.setState({message:e.target.value})}} />
          <button onClick={() => {
            alert(this.state.message);
            this.setState({message:''})
          }}>enter</button>
      </div>
    )
  }
}

export default EventPractice;
```

###### 임의 메서드를 통해 가독성 높히기

함수가 호출될 때, this는 호출부에 따라 결정됨. -> 클래스의 임의 메서드가 특정 요소의 이벤트로 등록되는 과정에서 메서드와 this의 관계는 끊어져 버림!

📍그러므로, 이벤트가 메서드에 등록되어도 this가 컴포넌트 자신을 가리키기 위해 `bind()`를 해주어야 함. (안하면 undefined가 뜹니다.)

```javascript
import React, {Component} from 'react';

class EventPractice extends Component{

  state = {
    message: '',
    title:''
  }

  constructor(props){
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.handleClick = this.handleClick.bind(this);
  }

  handleChange(e) {
    this.setState({
      message:e.target.value
    })
  }

  handleClick = () => {
    alert(this.state.message + '' + this.state.title);
    this.setState({
      title:''
      message:''
    })
  }

  render(){
    return(
      <div>
        <h1>let's practice event!</h1>
        <input
          type="text"
          name="message"
          placeholder='write something...'
          name="title"
          value={this.state.title}
          onChange={this.handleChange} />
          <input
          type="text"
          name="message"
          placeholder='write something...'
          name="desc"
          value={this.state.message}
          onChange={this.handleChange} />
          <button onClick={this.handleClick}>enter</button>
      </div>
    )
  }
}

export default EventPractice;
```

###### input이 여러개 일 때

input이 여러개일 경우, event객체를 활용할 수 있다. 객체 안에서 key를 []로 감싸면 그 안에 레퍼런스가 가리키는 실제 값이 key로 사용된다.

```javascript
  handleChange(e) {
    this.setState({
      [e.target.name]:e.target.value
    })
  }
```

###### 다음 코드를 함수형으로 변경하기

* this를 사용하지 않고 불러오는 게 더 간편하게 느껴진다.

```javascript
import React, {useState} from "react";

const EventFuncPractice = () => {
  const [username, setUsername] = useState('');
  const [message, setMessage] = useState('');
  const onChangeUser = e => setUsername(e.target.value);
  const onChangeMessage = e => setMessage(e.target.value);
  
  const onClick = () => {
    alert(username + ' : ' + message)
    setUsername('')
    setMessage('')
  }

  const onKeyPress = (e) => {
    if(e.key === 'Enter'){
      onClick();
    }
  }

  return(
    <div>
      <h1>let's practice event!</h1>
      <input
        type="text"
        name="message"
        placeholder='write something...'
        name="username"
        value={username}
        onChange={onChangeUser} />
        <input
        type="text"
        name="message"
        placeholder='write something...'
        name="message"
        value={message}
        onChange={onChangeMessage}
        onKeyPress = {onKeyPress} />
        <button onClick={onClick}>enter</button>
    </div>
  )
}

export default EventFuncPractice;
```

###### better way

```javascript
import React, {useState} from "react";

const EventFuncPractice = () => {
  const [form, setForm] = useState({
    username:'',
    message:''
  })
  const {username, message} = form;

  const onChange = e => {
    const nextForm = {
      ...form, // 기존의 form 내용을 복사
      [e.target.name] : e.target.value
    };
    setForm(nextForm);
  }

  const onClick = () => {
    alert(username + ' : ' + message)
    setForm({
      username: '',
      message : ''
    })
  }

  const onKeyPress = (e) => {
    if(e.key === 'Enter'){
      onClick();
    }
  }

  return(
    <div>
      <h1>let's practice event!</h1>
      <input
        type="text"
        name="message"
        placeholder='write something...'
        name="username"
        value={username}
        onChange={onChange} />
        <input
        type="text"
        name="message"
        placeholder='write something...'
        name="message"
        value={message}
        onChange={onChange}
        onKeyPress = {onKeyPress} />
        <button onClick={onClick}>enter</button>
    </div>
  )
}

export default EventFuncPractice;
```