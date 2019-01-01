---
layout: post
title: javascript self study (JS fundamental)
subtitle: I studied with javascript.info website
category: [javascript, ]
tags: [javascript, es6, ]
---

## 1. fundamentals
- script tag : html 파일 내부에서 `<script>` 태그를 사용하여 js코드를 작성할 수 있다는 기초내용을 읽었다.

- 문장끝에 semicolon붙이는 습관을 들이자.
- let, const 키워드를 사용해서 변수선언할 수 있으며 camelCase 규칙을 지키자.

## 2. seven data types
#### 2.1) number
다른 언어에서는 볼 수 없는 특별한 number value가 몇가지 있다.
`Infinity`, `-Infinity`, `NaN`가 그것들이다.
`Infinity`는 수학적 무한대를 나타낸다. `1/0`이와 같은 연산의 결과값이 `Infinity`이며 `let num=Infinity;`와 같은 코드에 대해서도 변수 num은 무한대다.
`NaN`는 계산error를 나타낸다. 가령 `"num"/10`와 같은 expression의 결과는 `NaN`이다.

#### 2.2) string : 문자열.
#### 2.3) boolean : true, false
#### 2.4) null
c, java에서와 같은 null **_널 포인터_** 를 생각하면 안된다. 단지 empty, unknown을 뜻한다.
`typeof null;`의 결과가 `object`라는 것 기억하자.
#### 2.5) undefined
정의는 다음과 같다. : `value is not assigned`.

#### 2.6) object
#### 2.7) symbol

## 3. type conversion
[http://javascript.info/type-conversions](http://javascript.info/type-conversions) 이곳 홈페이지에서 task 문제 풀어보는게 제일 좋을듯싶다.

## 4. operator
비트연산자는 operand를 32비트 숫자로 취급한다. [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators) 에서 bit연산자에 대해 읽어보면 도움이 될 것이다.

## 5. Comparison
`null`은 `0`으로, `undefined`는 `NaN`으로 conversion된다.
> js에서는 동등비교 `==`와 대소비교 `> < >= <=`규칙이 다르다. 대소비교는 수학적비교와 다르지 않지만 동등비교는 미리 정의된 rule을 따른다.  
> `null`과 `undefined`는 서로에게만 동일하고 다른 value에 대해 같지 않다.

## 6. user interaction
alert, prompt, confirm

## 7. logical operator
문제풀고 skip

## 8. 반복문
`continue`, `break`를 label과 함께 사용하여 좀 더 유연한 제어를 할 수 있다.

## 9. switch, case문
- 다른 언어와 달리 js에서는 `switch()`, `case()` 괄호안에 expression이 올 수 있다.
- 또한 여기에서 이뤄지는 equality check은 strict하다. 즉 `===`

## 10. 함수
- es6부터 default parameter value를 지정할 수 있게 되었다.
- 일급함수라는 용어는 function을 value로 취급하여 변수에 할당할 수 있고 함수 파라미터로 넘길 수 있고 심지어 함수의 리턴값으로도 쓰일 수 있음을 말한다.

## 11. function expression VS function declaration
- function declaration은 코드블럭(**_함수블럭이 아님!!_**) 또는 스크립트 전체에서 사용가능하다.
- function expression은 실행 flow가 도달했을 때 부터 사용가능하다.
