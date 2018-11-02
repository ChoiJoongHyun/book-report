ECMAScript6: 빠르게 배우는 ES6 스킬과 비동기 프로그래밍
=======================================================

let & const
-----------

##### let

-	let 으로 선언된 변수는 다시 선언 불가.

```javascript
let msg = "1";
let msg = "1"; //error

var msg = "1";
var msg = "2"; //success
```

##### const

-	const 는 선언하면서 초기화 필수. (상수)

```javascript
const myName; //error
const name = "joonghyun";
name = "choi" //error
```

##### Block scope

-	Block-scope : {} 로 감싸진 유효 범위
-	기존의 var 는 function scope 레벨 호이스팅
-	let 변수의 스코프는 블록 스코프 처리된다.

```javascript
let num = 1;
if(true) {
  let num = 2;
  console.log(num); //2
}
console.log(num); //1

```

##### Temporal Dead Zone

-	let 은 var 와 달리 변수가 초기화 되기 전에 접근하 undefiend 가 아닌 ReferenceError 가 발생한다.
	-	var 는 선언과 동시에 초기화가 되지만, let 은 변수가 스코프에 선언은 되지만 (호이스팅) 선언문에 도달해야 초기화가 이루어진다.

```javascript

let product = 'phone';
if(true) {
  // 변수 product 에 대한 tdz 시작
  console.log(product);
  // tdz 종료
  let product = 'tv';
}
console.log(product); //ReferenceError

```

-	let 으로 선언된 변수가 초기화되기전에 access 할수 없는 구역을 Temporal Dead Zone 이라 한다. (TDZ)
-	let 은 변수의 유효범위를 블록 스코프 처리해준다.
-	원시형 변수는 let, 상수는 const 사용

Template Literals (표현식과 템플릿 문자열)
------------------------------------------

-	es6 에서는 템플릿 문자열 도입 (백틱 문자 (esc 바로아래))

```javascript
let name = "choi";
let weight = "10";

console.log(` //백틱으로 문자열을 연다.
name = ${name}
weight = ${weight}
weight + bagWeight = ${weight + 3}
`);

```

-	백틱 내에 멀티라인 스트링을 입력 가능
-	템플릿 문자열의 표현식을 통해 문자열에 외부 변수를 입력 할 수 있다.
-	표현식은 계산식 등 해석이 가능한 대상이라면 모두 허용한다.

Destructuring (비구조와 할당)
-----------------------------

-	객체 또는 배열에서 데이터를 분석하여 각각의 변수에 할당하는 것을 의미한다. (json 형식의 객체나 배열을 쉽게 변수에 할당 가능)

```javascript
let data = [{
  count: 1,
  list: [{
    name: ["choi", "joong"],
    group: "hyun"
  }]
}];

let  [{count,list: [{name, group}]}] = data;
console.log(`
count: ${count}
group: ${group}
`);
```

-	배열이 아닌 객체도 가능하다.

```javascript
function productObject({name, price, color}) {  //인자로 객체 표현식을 받는다.
  return {
    productName: "this product name : " + name,
    addToCar() {
      console.log(name + "is added");
    },
    detailView() {
      console.log(`
        ${productName}
        price: ${price}
        color: ${color}
      `);
    }
  };
}
//함수 에서 객체를 리턴할때 비구조와할당을 통해 여러 변수로 받을 수 있다.
var {productName, addToCar, detailView} = productObject({name: "apple", price: 199, color: "sliver"});
addToCar();
detailView();

```

-	객체의 속성이나 배열의 값을 변수에 할당할때 destructuring 을 통해 간편하게 할당하고 정의 가능

Class & Class 상속
------------------

-	생성자 함수는 constructor
-	new 키워드로 객체 생성하여 사용

```javascript
class Lang {
  constructor(name) {
    this.name = name;
  }
  getName() {
    return this.name;
  }
}
```

-	extends 키워드를 사용해 상속 가능
-	부모 클래스에 정의된 메서드나 변수를 자식 클래스에서 사용 가능

```javascript
class Javascript extends Lang {
  constructor(name) {
    super(name);
  }
}
```

-	자식클래스를 초기화 하려면 부모클래스의 생성자를 호출하여야 함으로 super 메소드를 통해 부모클래스의 생성자를 호출한다.

-	클래스는 내부적으로 함수처럼 동작.

-	ES6 에서는 객체지향에서 가장 중요한 특징인 클래스와 상속의 개념을 제대로 적립하여 객체지향 프로그래밍이 가능하다.

Arrow Function (화살표 함수) & this
-----------------------------------

##### Arrow Function

-	익명 함수를 간략하게 표현 할 수 있는 화살표 표현식

```javascript
function () {}  //기존

() => {}  //es6
```

-	실행문이 하나라면 중괄호도 생략 가능

```javascript
const myFunction = () => console.log("ES6");
```

##### 함수 실행에서의 this

-	자바스크립트 함수 실행에서의 this 는 기본적으로 전역 객체이다.
-	es5 에서는 call(), apply() 로 this 를 binding 해주는 방법을 사용하였다.

```javascript
var name = "es5";

function Lang() {
  this.name = "es6";

  setTimeout(function() {
    console.log("Global name is " + this.name); //es5 "this 는 윈도우 전역 객체이다."
  }, 100);
  setTimeout(() => {
    console.log("My name is " + this.name); //es6
  },100);
}
```

##### IIFE (Immediately-invoked function expression) (즉시 실행 함수)

-	즉시 실행 함수는 한번의 실행만 필요로 하는 초기화 코드 부분에 많이 사용된다.

```javascript
//es5
(function(lang) {
    console.log(lang);
}("es5"));

//es6
((lang)=>{
  console.log(lang);
})("es6");  //괄호를 먼저 묵고 함수를 호출하여야 한다.
```

-	es6 에서는 익명함수에서 function 키워드를 생략하고 괄호와 화살표를 사용 가능.
-	콜백 함수로 실행될때 기존의(es5) 익명함수는 글로벌 컨텍스트에 접근하였으나. 화살표 함수는 콜백 함수를 할당한 당시의 컨텍스트를 그대로 활용한다.

Default Parameter (기본 매개변수)
---------------------------------

-	자바스크립트에서 함수의 배개변수는 기본값이 undefiend 이다.

```javascript
function animal(name) { //undefiend, null, false, 0, 공백 에 대해서 적용 가능하다.
  var name = name || "dog";
  console.log(name);
}
animal();       //dog
animal(null);   //dog
animal(false);  //dog

const defaultColor = "red"; //undefined 일 경우에만 적용되니 주의 필요
function defalutValue(value, color = defaultColor, myArray = []) {
  myArray.push(value, color);
  return console.log(myArray);
}
defaultValue("strawberry");  //두번째 인자값이 없어 undefiend 로 넘어감
defaultValue("apple", undefiend);
defalutValue("banana", "yellow");
```

Iterator & Symbol
-----------------

##### Iterator & for-of

-	모든 이터러블 객체에서 사용 가능

```javascript
const myArray = [1,2,3];
for(let value of myArray) {
  console.log(value);
}
```

##### Symbol

-	객체에 다른 어떤것과도 다른 유니크한 속성을 만들기 위한 타입
-	typeof 가 반환되는 타입
	-	Undefined, Boolean, String, Number, Object, Function, Symbol (typeof null -> object 로 출력됨)

```javascript
let name = Symbol("kin");
console.log(typeof name); //symbol
```

```javascript
//symbol 은 유니크하다.
const myObject = {
  symbol1: [Symbol("1")];
  symbol2: [Symbol("1")];
}
console.log(myObject.symbol1 == myObject.symbol2);  //false
```

```javascript
const myObj = {};
myObject.a = "apple";
myObject["b"] = "book";

let c = Symbol("c");
myObj[c] = "cat";
myObj[Symbol("d")] = "dog";

console.log(Object.key(myObj)); //a,b
console.log(myObject[c]); //cat
console.log(Object.getOwnPropertySymbols(myObj)); //[Symbol(c), Symbol(d)]
```

##### Iterator

-	for-of 루프는 symbol.iterator 메서드 호출로 시작된다.
-	next() 메소드와 value, done 을 속성으로 가진다.
-	next() 를 내부적으로 반복하며 collection 을 순회한다.

나머지 매개 변수, 전개 연산자
-----------------------------

##### Rest Parameter (나머지 매개 변수)

-	가변 인자에 대한 기능 추가

```javascript
function myFunc(a,b,c,d, ...rest) {
  console.log(a,b); //1 2
  console.log(rest);  //[5,6,7,8]
  console.log(rest.length); //4
}
myFunc(1,2,3,4,5,6,7,8);
```

-	나머지 매개 변수는 두개 이상의 매개변수를 하나의 요소로 모은다.

##### 전개 연산자

-	함수를 호출할때 키워드를 사용하 해당 배열을 펼쳐서 여러개의 인자로 넘겨주는 것

```javascript
function rest(a,b,c, ...rest) {
  console.log(b,c); //2 3
  for(let i of rest) {
    console.log(i); // 4 / 5 / 6
  }
}
var spread = [2,3];
rest(1, ...spread, 4, ...[5,6])

```

-	대이터가 동적으로 바뀌는 환경에서 가변인자를 다루기에 유용하게 활용한다.

-	전개 연산자는 배열이나 객체를 확장하는 것

Map & Set
---------

-	es5 는 object 나 array 를 사용하였으나 es6 에서는 map 과 set 이 추가 되었다.

##### map

-	map 은 key 와 value 가 한쌍인 컬렉션

```javascript
const myMap = new Map();
myMap.set("lang", "javascript")

const myData = new Map({
  ["key1", "value1"],
  ["key2", "value2"]
});

const myMap2 = new Map();
myMap2.set("key1", "value1").set("key2", "value2");

const myMap3 = new Map();
const myArray = [["key1", "value1"], ["key2", "value2"]];
for(let i of myArray) {
  myMap3.set(...i)  //전개연산자로 myArray 의 배열을 풀어 set 가능
}

for(let [key, value] of myMap3) { //Destructuring 가능
  console.log(key + " : " + value);
}
```

##### MapIterator

-	for-of, entries(), next(), keys(), values() 사용
-	map.keys() : 키 들을 갖는 맵 이터레이터를 반환
-	map.values() : value 들을 갖는 맵 이터레이터를 반환
-	map.entries() : 키와 value 을 갖는 맵 이터레이터를 반환
-	이터레이터는 next() 메소드를 갖는다. next() 를 통해 순회 가능

##### Filtering

-	맵을 특정 조건을 필터링하여 다른 맵에 담을수 있다.

```javascript
const myData = new Map({
  ["key1", "value1"],
  ["key2", "value2"]
});

const newMap = new Map(
  [...myData].filter(()[a,b])=> b==='value2')
);
console.log(newMap);//Map {'key2', 'value2'}
```

##### set

-	중복을 허용하지 않는 집합

-	맵과 사용법은 비슷하지만 키가 없이 value 들만 존재한다.

```javascript
var set = new Set();
set.add("a").add("b").add("b")  //set : a, b
```
