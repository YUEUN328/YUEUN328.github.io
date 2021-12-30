---
layout: single
title: 43일차
categories: TIL
tag: [CSS]
author_profile: false
---

## TIL

* display 속성(property):

  1. block: \<div>, \<p>, \<section>, \<article>, \<h1>, \<ul>, \<li>, ...

     - 항상 새 줄(new line)에서 시작한다.
     - width, height를 변경할 수 있다.
     - margin, padding을 변경할 수 있다.

  2. inline: \<span>, \<strong>, \<em>, \<a>, ...

     - 같은 줄에서 시작한다.

     - width, height를 변경할 수 없다!

     - margin, padding을 변경할 수 있다.

  3. inilne-block: inline 속성 + block 속성

     - 같은 줄에서 시작한다(inline 속성)!
     - width, height, padding, margin 변경 가능하다(block 속성).    

* 속성이 여러 개일 때 순서는 상관 없다. 공백만 있으면 된다.

* 요소를 찾는 방법이 중요하다!

* display: none;은 요소가 차지하는 영역 자체가 없지만, visibility: hidden;은 영역은 그대로 있다.

* absolute에서 부모가 \<body>면 fixed랑 같아진다.

* [Bootstrap v4.6](https://getbootstrap.com/docs/4.6/getting-started/download/)을 권장한다.