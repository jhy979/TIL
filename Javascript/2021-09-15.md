# JavaScript

> 저만의 언어로 js를 정리해봤습니다. js는 제가 이 언어로 프로젝트를 진행한 적도 있고 C,C++과 비슷한 것들이 많아서 많이 알고 있는 편입니다. 따라서 여기서는 기본적인 내용들을 쓰고 제가 잘 잊어버리는 내용들을 위주로 작성하려고 합니다. 설명이 아마 불친절할 수 있어요.
___
## 0. index.html 에 js 연결
- defer 속성 필수
```js
<head>
  <script defer src="./main.js"></script>
</head>
```
___
## 1. 표기법
- dash-case (kebab-case) : html,css에서 단어를 표기하는 방법 
- snake_case : html,css에서 주로 사용
- camelCase : ```theQuickBrownFoxJumps ``` 대문자, JS에서 주로 사용
- PascalCase : ```TheQuickBrownFoxJumps ``` 처음도 대문자, JS에서 주로 사용
___
## 2. 변수
- let,const로 변수를 선언합니다. (var는 사용하지 않는걸 권장)
- const는 재할당이 안되므로 낭비, 에러 막기 위해 const를 기본적으로 쓰길 권장해요.
#### 문자열
```js
let myName="JHY979";
let email = 'jhy979@gmail.com';
let hello = `Hello $(myName}?`; // 백틱으로 보간법 사용합니다.
```
####  숫자
```js
let number =123;
let opacity = 1.54;
```
#### Boolean
```js
let checked = true;
let isShow = false;
```
#### Undefined
```js
let undef;
let obj = {abc:123};

console.log(undef); //undefined
console.log(obj.abc); //123
console.log(obj.xyz); //undefined
```
#### Null
- 의도적으로 비어있기에 undefined 랑은 달라요.
```js
let empty = null;
```
#### Object
```js
let user = {
   name: 'jhy',
   age: 25,
   isValid: true
  };

console.log(user.name); // jhy
```
#### Array
```js
let fruits = ['Apple','Banana','Cherry'];

console.log(fruits[0]); // 'Apple'
```
___
## 3. 함수
#### 기명함수
```js
function helloFunc() {
  console.log(1234);
  return 12;
}
let a = helloFunc(); //1234
console.log(a); // 12
```
#### 익명함수
```js
let world = function () {
  console.log('World!');
}
world(); // World! 출력
```
#### 메소드
```js
const jhy = {
  name : 'JHY',
  age : 25,
  getName: function(){
    return this.name;
  }
};

console.log(jhy.getName()); // JHY
```
___
## 4. 조건문
```js
let isShow = true;

if(isShow){
  console.log('Show !'); // Show!
}
else {
  console.log('Hide?');
}
```
___
## 5. DOM API (Document Object Model, Application Programming Interface)
- DOM : html 속 div,input,span 요소들
- API : html을 제어하는 js의 명령들
#### document.querySelector
```js
let boxEl =document.querySelector('.box'); // .box라는 선택자로 html 요소 가장 먼저 나오는 거 1개 찾기
let boxEls =document.querySelectorAll('.box'); // .box라는 선택자를 가진 html 요소 전부 찾기 (boxEls는 유사 배열이지 배열은 아니예요)
```
#### addEventListener
```js
boxEl.addEventListener(1,2); // boxEl을 1했을 때 2를 실행합니다.

boxEl.addEventListener('click', function (){
    console.log('Click occurs');
  });
```
#### classList
```js
  boxEl.classList.add('active') // 'active' 클래스 추가
  boxEl.classList.contains('active') // 'active' 클래스 있으면 true 없으면 false 반환
  boxEl.classList.remove('active') // 'active' 클래스 삭제
```
#### forEach
```js
boxEls.forEAch(function(AAA, index) {}) // AAA : 반복중인 요소, index : 인덱스

boxEls.forEach(function(boxEl,index){
  boxEl.classList.add(`order-${index}`)
  console.log(index,boxEl)
})
```
#### textContent
- Getter로 쓸 때
- text만 반환
```js
console.log(boxEl.textContent) //Box!!
```
- Setter로 쓸 때
```js
boxEl.textContent = 'JHY';
```
___
## 6. 메소드 체이닝
```js
const a = 'Hello'
const b = a.split('').reverse().join('');
```
