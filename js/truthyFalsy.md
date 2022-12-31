Truthy and Falsy
========

truthy 와 falsy: Boolean 문맥에서 true 또는 false로 여겨지는 값

Boolean 문맥 - boolean type의 값이 요구되는 상황을 의미합니다. boolean 문맥에서 값이 boolean type 이 아닐경우, javascript는 그 값을 boolean 값으로 평가하게 됩니다. 이때 true로 평가되는 값이 truthy이고, false로 평가되는 값이 falsy 입니다.

``` javascript
if("hihi"){
  console.log('hello world!');
}
```
javascript는 if 문 안의 값이 true로 평가되면 블럭문 내부 코드를 실행하게 됩니다. 위에 코드를 실행하게 됩니다. hello world!

falsy가 아닌 값은 전부 truthy이며 falsy와 truthy에 대한 정보는

[Truthy](https://developer.mozilla.org/ko/docs/Glossary/Truthy) - truthy mdn 링크
[Falsy](https://developer.mozilla.org/ko/docs/Glossary/Falsy) - falsy mdn 링크

위의 링크에서 확인하실수 있습니다.
- - -
### 연산자 && 와 ||

&& 연산자: 모든 값이 truthy이면 마지막 truthy 값을 반환합니다. 또는 첫 번째 falsy 값을 반환합니다. (첫번째: 가장 왼쪽 값)

```javascript
'a' && 'b' //return b
const val = 1 && 'hahaha' && [] // val의 값은 []가 됩니다.
'a' && NaN && '3' //return NaN
if('a' && NaN && '3'){
  alert('truthy')
}
// 'a' && NaN && '3' 의 결과로 NaN이 return 됩니다. NaN은 falsy 이므로, if 블럭문 안에 있는 alert 코드는 실행되지 않게됩니다.
```


|| 연산자: 가장 첫 번째 truthy 값을 반환 합니다. 또는 모든 값이 falsy라면, 가장 마지막 falsy 값을 반환합니다.

```javascript
const val = NaN || 'cat' || 0 //val의 값은 'cat' 이됩니다
const val2 = NaN || 0 || '' || undefined // val2 의값은 undefined가 됩니다.
if(NaN || 0 || 1 || null){
  alert('hello world!')
}
// NaN || 0 || 1 || null 의 결과로 1이 return 됩니다. 1은 truthy이므로 if 블록문 내부의 alert 코드가 실행됩니다. hello world!
```
- - -

### 연산자 &&= 와 ||=

a &&= b 는 a = a && b 의 축약 표현입니다.

```javascript
let a = 10;
a &&= 20; // a: 20
a &&= null; // a: null
a &&= '아무값' // a: null
```
-> a &&= b는 a의 값이 truthy라면 a에 b값이 할당됩니다. 반대로 a의 값이 falsy라면, a 값은 유지 됩니다.

a ||= b 는 a = a || b 의 축약 표현입니다.

```javascript
let a = null;
a ||= 0   // a: 0
a ||= 3   // a: 3
a ||= '아무거나' // a: 3
```

-> a ||= b 는 a의 값이 falsy라면 a에 b값이 할당됩니다. 반대로 a 값이 truthy라면 a값은 유지됩니다.