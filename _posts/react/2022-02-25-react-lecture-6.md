---
title: "리엑트 공부 : 6th week"
categories:
  - react
tags:
- react
---


### useEffect


`useEffect`는 컴포넌트가 실행될 때마다 특정한 작업을 수행할 수 있도록 하는 컴포넌트다.
* 지연 이벤트 동안에 레이아웃 배치와 그리기를 완료한 후 발생합
* 함수 내부에 defendency를 설정하면 해당 값이 변화 할 때마다 실행 시킬 수 있음


##### 첫번째 방법

랜더링이 될 때마다 실행

```javascript
useEffect(()=>{
},[]);
```

##### 두번째 방법

첫번째 useEffect가 호출되고 나서는 number의 값이 변경될 때마다 실행됨

```javascript
useEffect(()=>{
  document.title = number
},[number]);
```



##### useEffect를 사용하는 올바른 방법
클린코드에서는 각 하나의 함수가 하나의 기능을 가지므로 `useEffect` 하나에 너무 많은 기능을 넣지 않도록 한다.

나 또한 클론코딩 프로젝트에서 `useEffect`를 너무 막 사용한 것 같아 반성중이다...

* 참고자료 : https://ui.toast.com/weekly-pick/ko_20200916