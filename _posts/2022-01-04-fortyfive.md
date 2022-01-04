---
layout: single
title: 45일차
categories: TIL
tag: [JavaScript]
author_profile: false
---

* 자바스크립트는 자바와 달리 배열에 []를 쓴다.

* for-in 구문: 자바의 향상된 for 구문(enhanced for statement)과 비슷하다.
  * (주의) 자바스트립트에서 for-in 구문은 배열의 인덱스들을 꺼내준다.
  * 배열의 원소들을 꺼내지 않는다!

* 스타트 태그와 엔드 태그 사이에 모든 것은 innerHTML이다. innerHTML += 이라고 해야 지금까지  쓴 것에 더해서 출력되고, innerHTML = 이라고 하면 마지막만 출력된다. 

*  아래와 같은 코드를 자주 쓰니 기억하자!

  ```javascript
  // calculator 함수를 호출할 때, 익명 함수를 argument로 전달
  result = calculator(1, 2, function (x, y) {
      return x / y;
  });
  ```

* window.alert(); 에서 window는 생략 가능

* HTML 이벤트 처리 방법 1:
  * HTML 태그의 onevent 속성 값에 JavaScript 함수 호출 코드를 작성한다.
* HTML 이벤트 처리 방법 2:
  * HTML 요소(element)를 찾고, element가 가지고 있는 addEventListener(event, callback) 메서드를 사용한다.
  * 두 번째 방법이 장점이 많다.