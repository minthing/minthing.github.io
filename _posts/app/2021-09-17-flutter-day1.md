---
title: "flutter 기초 : day 1"
categories:
  - flutter
tags:
  - flutter
---

##### widget

기본 디자인 요소를 widget이라고 함. flutter는 위젯이 쌓여 앱을 만듬.

##### 기본적인 앱 구성해보기


<img src="https://user-images.githubusercontent.com/54466684/133742750-88479283-ca88-486d-b13e-3d874660eed9.png" width="30%" height="30%" style="display:block;margin:0 auto">

```dart
children: <Widget>[
  Text("hello world"), // text
  Icon(Icons.add), // add button
  Container( // 한 개의 자식을 갖는 레이아웃 위젯입니다.
    child: Text("i'm not container"), color: Colors.redAccent,),
  TextButton(onPressed: (){ // press 시 function
    print("text button pressed");
    },
    child: Text("text button!!")
    )
],
```