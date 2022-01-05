---
layout: single
title: 44일차
categories: TIL
tag: [JavaScript]
author_profile: false
---

## TIL

* 보통 \<script>는 \<body>의 마지막에 넣는다.

* id나 class를 주는 이유는 요소를 찾기 위해서이다.
* 자바스크립트의 변수 var의 범위
  * 전역 변수: \<script> 안에서(함수 밖에서) 선언.  \<script> 끝날 때까지 사용 가능하다.
  * 지역 변수: 함수 안에서 선언. 함수 안에서만 사용 가능하다.

* 함수 이름도 일종의 전역 변수이다. 따라서 함수 이름과 변수 이름이 겹치면 변수를 지역 변수로 써야 한다.

* \<select>나 \<input> 안에 있는 값은 value로 찾으면 된다.

* 자바스크립트는 정수든 실수든 문자열이든 타입을 전부 var라고 한다.

* 아래 메서드 안에 주석 처리한 코드와 그렇지 않은 코드는 같은 결과가 나온다.

  ```javascript
  for (var i = 1; i <= 6; i++) {
      //result.innerHTML += '<h' + i + '>' + '제목' + i + '</h' + i + '>';
      result.innerHTML += `<h${i}> 제목 ${i}<h${i}>`;
  }    
  ```

* NaN은 Not a Number이다.

* 자바스크립트의 모든 함수는 arguments라는 이름의 프로퍼티(property)를 가진다. 따라서 arguments를 지역 변수나 파라미터 이름으로 선언하면 안 된다.