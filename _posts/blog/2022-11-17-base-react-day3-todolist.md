---
title: "REACT 기초 다시 정리 : TodoList"
categories:
  - react
tags:
  - react
  - basic
---

### simple todo list

책에 나와 있는 예제를 가볍게 리엑트 복습용으로 훑어볼 겸, 개인적으로 디자인(ㅎㅎ)을 좀 본격적으로 짜볼까 싶어서 개선해 보았다.

일단 reset.css를 새로 제작해 App.js에 import 한 후, css의 선언 순서 또한 기준에 맞게 순서대로 배치하고자 했다. (정리수인 📦)

###### this
<img width="576" alt="image" src="https://user-images.githubusercontent.com/54466684/202707961-27eb95ee-6b42-4ca5-89bc-b1ce0865cf47.png">

**여기서 의문인 점** 각 컴포넌트 최상위만 카멜 케이스 > 그 밑은 `-`로 연결한 것은 리엑트의 권장사항인가? 🤔
난 언더 스코프를 주로 사용해서 요것도 변경...

### todo에서 배열 추가하기
* id값과 같이 변경된다 해도 화면에 보이지도, 리랜더링 될 필요도 없는 값은 `useRef()`를 통해 관리해 준다.
* 제출에 관해서는 `onSubmit`이 추가 로직 작성할 여지가 적어서 더 경제적임.