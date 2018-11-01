ECMAScript6: 빠르게 배우는 ES6 스킬과 비동기 프로그래밍
=======================================================

### let & const

-	let 으로 선언된 변수는 다시 선언 불가.

```javascript
let msg = "1";
let msg = "1"; //error

var msg = "1";
var msg = "2"; //success
```

-	const 는 선언하면서 초기화 필수. (상수)

```javascript
const myName; //error
const name = "joonghyun";
name = "choi" //error
```

### Block scope

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

### Temporal Dead Zone

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

### Template Literals (표현식과 템플릿 문자열)

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

### Destructuring (비구조와 할당)

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
