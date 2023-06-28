javascript Prototype
====

## Prototype

javascript의 모든 함수에 존재하는 속성 입니다.

```javascript

const Meow = function() {}
console.log(Meow.prototype);  // Object

const cat1 = new Meow();
console.log(cat1.__proto__)   // Object

```

- 모든 자바스크립트 객체는 constructor 함수에 의해 만들어 집니다.
- 함수를 new 키워드를 사용해 호출하면 그 결과로 새로운 객체를 반환합니다.
- consturctor 함수가 호출되며 새로운 객체를 만들때마다, 새로운 객체의 __proto__ 속성이 consturctor의 prototype과 연결 되게 합니다.

## Prototype chain

자바스크립트에서 객체의 어떤 속성에 접근하려고 할 때, 객체 자체의 속성 뿐만 아니라 객체의 프로토타입, 프로토 타입의 프로토 타입... (이런 일련의 연결을 프로토 타입 체인이라고 부릅니다.) 을 전부 탐색합니다.


```javascript

function Dog(name) {
  this.name = name;
}

Dog.prototype.run = function(){console.log(`${this.name} run run~!`)}

let meongi = new Dog('meongi');

console.log(meongi.name) //객체 속성에 name이 존재하여 바로 출력합니다.
meongi.run();             // 객체에는 run이 없습니다. meongi.__proto__ 를 탐색하여 run을 실행시킵니다.
meongi.sleep()            // Uncaught TypeError: meongi.sleep is not a function

```

먼지의 이름은 객체 먼지가 가지고 있어서 출력되었습니다.
<br />
run 속성은 먼지 객체가 가지고 있지는 않지만, Dog.prototype에 포함되어 있어서 성공적으로 실행이 된 모습입니다.

<br />

sleep 이라는 속성은 meongi 객체, Dog.prototype에 없어서 실행되지 않았습니다.
아레 코드를 추가해 보겠습니다.

```javascript
Object.prototype.sleep = function () {console.log(`${this.name} sleep~`)}
meongi.sleep()          //meongi sleep~
```

Dog.prototype 또한 객체이기에, __proto__ 속성을 가지고 있습니다. (Dog.prototype 객체를 만든 constructor의 prototype). 지금 경우에는 Object.prototype이 되겠내요. 이렇게 객체에 속성에 접근하려고 할때, 객체의 속성 -> 객체의 __proto__ 속성 -> __proto__ 속성의 __proto__ 속성... -> __proto__ 가 null이 될떄까지 모든 값을 참조합니다. 이것이 가능한 이유가 protoType들이 계속 이어져 있기 때문이고, 이것을 Prototype chain 이라고 부릅니다.

## 객체를 생성하는 여러 방법과 프로토타입 체인

### 문법 생성자로 객체 생성

```javascript
let obj = {a: 1};     //obj -> Object.prototype -> null
let arr = [1,2,3]     //arr -> Array.prototype -> Object.prototype -> null
function func(){}     //func -> Function.prototype -> Object.prototype -> null
 ```

모든 프로토 체인의 끝은 Object.prototype -> null 인걸 볼 수 있습니다. 또한 Function.prototype을 상속받는 경우 call, bind, apply 와 같은 메소드를 가집니다.



### 생성자를 이용

new 연산자를 이용해 함수를 호출하면 됩니다.

```javascript
function Meow (name) { this.name = name;}
Meow.prototype.meow = function () {console.log(`${this.name} meeooow ~!`)}

let navi = new Meow('navi');  // navi.__proto___ === Meow.prototype

```
navi 객체의 proto 속성은 Meow.prototype에 연결됩니다.

<br />

### Object.create를 이용

navi 객체를 복사해 나비를 만들어보겠습니다.
```javascript
function Meow (name) { this.name = name;}
Meow.prototype.meow = function () {console.log(`${this.name} meeooow ~!`)}

let navi = new Meow('navi');  // navi.__proto___ === Meow.prototype

let 나비 = Object.create(navi)

console.log(나비)   // Object {}
console.log(나비.__proto__)   // navi Object

```

Object.create를 이용해 만들어낸 복제 의 proto 속성 값을보면, 복제 원본 객체를 가리키고 있음을 알 수 있습니다. <br />

나비의 proto chain은 나비 -> navi -> Object -> null 이 되갰내요


### Prototype과 hasOwnProperty, in

in 키워드는 특정 객체의 속성이 맞는지 boolean 값을 반환하는 키워드 입니다.

```javascript

function Meow (name) { this.name = name;}
Meow.prototype.meow = function () {console.log(`${this.name} meeooow ~!`)}

let navi = new Meow('navi');  // navi.__proto___ === Meow.prototype

console.log('name' in navi)   // true
console.log('meow' in navi)   // true

```

in keyword는 객체 자체의 속성 뿐만 아니라 프로토 체인을 모두 탐색하여 접근 가능하면 true를 반환합니다.


hasOwnProperty 함수는 어떤 속성에 대해 객체가 자신만의 속성으로 가지고 있는지 boolean 값을 반환하는 함수입니다.

```javascript

function Meow (name) { this.name = name;}
Meow.prototype.meow = function () {console.log(`${this.name} meeooow ~!`)}

let navi = new Meow('navi');  // navi.__proto___ === Meow.prototype

console.log(navi.hasOwnProperty('name'))   // true
console.log(navi.hasOwnProperty('meow'))   // false

```



출처:https://developer.mozilla.org/ko/docs/Web/JavaScript/Inheritance_and_the_prototype_chain