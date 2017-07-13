# Javascript ES6 syntax 

***
> ### Class
>
> 자바스크립트는 예전부터 Prototype 기반 언어로 Object.prototype 이런 식으로 사용해 왔습니다. 하지만 ES6 문법이 자바스크립트에 적용된 이후론 드디어 자바스크립트에도 Class을 사용할 수 있게 되었습니다. 그래서 Class를 통해 프로토 타입 기반 상속, super, 인스턴스 및 정적 메서드 및 생성자를 사용할 수 있습니다.
> ```javascript
> class Shape {
> 	...
> 	to String() {
> 		return `Shape(${this.id})`
>    }
>}
> class Rectangle extends Shape {
>    constructor (id, x, y, width, height) {
>        super(id, x, y);
>        ...
>    }
>    toString () {
>        return "Rectangle > " + super.toString();
>    }
> }
> class Circle extends Shape {
>    constructor (id, x, y, radius) {
>        super(id, x, y);
>        ...
>    }
>    toString () {
>        return "Circle > " + super.toString();
>    }
> }
> ```
***
> ### let, const
> 기존의 자바스크립트의 var는 function-scope였지만 let과 const는 Block-scoped binding constructs으로 let은 var 처럼 사용하고 const는 참조형으로 사용됩니다.
>> * let
>> ```javascript
>> for (let i = 0; i < a.length; i++) {
>>    let x = a[i];
>>    …
>> }
>> for (let i = 0; i < b.length; i++) {
>>    let y = b[i];
>>    …
>> }
>>
>> let callbacks = [];
>> for (let i = 0; i <= 2; i++) {
>>    callbacks[i] = function () { return i * 2; };
>> }
>> callbacks[0]() === 0;
>> callbacks[1]() === 2;
>> callbacks[2]() === 4;
>> ```
>> ***
>> * const
>>  ```javascript
>> const foo = [0, 1];
>> console.log(foo); // foo = [1,2]
>> const foo = [1, 2]; // syntax error
>> console.log(foo);
>>  ```
>>
***
> ### Symbols
> Symbol은 객체 식별자로 사용할 수 있는 독특하고 고유한 데이터 타입입니다. 그래서 정의는 단 한번만 가능하며, 정의된 이후론 값 변경이 불가능합니다. 기본 문자열 값은 리터럴을 정의할 때마다 메모리가 늘어나지만 Symbol는 데이터 값이 변경되지 않기 때문에 정해진 메모리만 할당됩니다. 그래서 메모리 누수가 일어나지 않습니다.
> ```javascript
> Symbol("foo") !== Symbol("foo");
> const foo = Symbol();
> const bar = Symbol();
> typeof foo === "symbol";
> typeof bar === "symbol";
> let obj = {};
> obj[foo] = "foo";
> obj[bar] = "bar";
> JSON.stringify(obj); // {}
> Object.keys(obj); // []
> Object.getOwnPropertyNames(obj); // []
> Object.getOwnPropertySymbols(obj); // [ foo, bar ]
> ```
>
***
> ### Arrow function
> Arrow function은 말 그대로 화살표를 통해 표현된 함수로, '=>'을 이용해 바인딩합니다. Arrow function은 자신의 this, super, new.target를 바인딩하지 않고 항상 익명함수로 이용됩니다. 따라서 이 함수 표현은 메소드 함수가 아닌 곳에 사용해야 합니다. 그래서 생성자로서 Arrow function을 사용할 수 없습니다.
> ```javascript
> odds  = evens.map(v => v + 1); // odds = evens.map(function (v) { return v+1; };
> pairs = evens.map(v => ({ even: v, odd: v + 1 })); // pairs = evens.map(function (v) { return { even: v, odd: v + 1}; });
> nums  = evens.map((v, i) => v + i); // nums = evens.map(function (v, i) { return v + i });
>  ```
***
> ### Generator
> Generator 함수는 일반 함수와는 다르게 실행 중간에서 결과값을 반환할 수 있으며, 다른 작업을 처리한 이후로 다시 그 위치에서 코드를 시작할 수 있는 함수입니다. Generator 함수는 next 함수를 통해 반복 함수 iterator를 제공하고 결과값을 value로, 진행 상황을 done으로, yield으로 반환값을 표현가능합니다.
> ```javascript
> let fibonacci = {
>    *[Symbol.iterator]() {
>        let pre = 0, cur = 1;
>        for (;;) {
>            [ pre, cur ] = [ cur, pre + cur ];
>            yield cur;
>        }
>    }
> }
>
> for (let n of fibonacci) {
>    if (n > 1000)
>        break;
>    console.log(n);
> }
> ```
***
> ### Template string
> Template String은 back-tick(\` \`)로 감싸집니다. Template String은 단일 행 및 다중 행 문자열에 대한 직관적인 표현 방법으로 인젝션 공격을 피하거나 문자열 내용에서 데이터 값을 사용할 수 있습니다.
> ```javascript
> var customer = { name: "Foo" };
> var card = { amount: 7, product: "Bar", unitprice: 42 };
> var message = `Hello ${customer.name},
> want to buy ${card.amount} ${card.product} for
> a total of ${card.amount * card.unitprice} bucks?`;
> ```
***
> ### Map, Set, Weakmap, Weakset
> 자바스크립트는 다양한 내장객체들을 사용하여 표현될 수 있는데, 그들 중 key를 통해 삽입 순서대로 반복할 수 있는 객체인 Map, Set이 주로 쓰입니다. Map은 Object 객체와 동일한 기능을 하는 객체고 Set은 유일한 값을 저장해야 하는 객체입니다. WeakMap, WeakSet은 Map과 Set과는 다르게 key가 약하게 참조되는 컬렉션입니다. 그래서 WeakMap, WeakSet의 객체는 key이어야 하지만 값은 임의의 값으로 지정가능합니다.
>> * Map
>> ```javascript
>> let m = new Map();
>> let s = Symbol();
>> m.set("hello", 42);
>> m.set(s, 34);
>> m.get(s) === 34;
>> m.size === 2;
>> for (let [ key, val ] of m.entries())
>>     console.log(key + " = " + val);
>> ```
>> ***
>> * Set
>> ```javascript
>> let s = new Set();
>> s.add("hello").add("goodbye").add("hello");
>> s.size === 2;
>> s.has("hello") === true;
>> for (let key of s.values()) // insertion order
>>     console.log(key);
>> ```
>> ***
>> * Weakmap
>> ```javascript
>> var wm1 = new WeakMap(),
>>     wm2 = new WeakMap(),
>>     wm3 = new WeakMap();
>> var o1 = {},
>>     o2 = function(){},
>>     o3 = window;
>>
>> wm1.set(o1, 37);
>> wm1.set(o2, "azerty");
>> wm2.set(o1, o2); // 무슨 값이든 가능
>> wm2.set(o3, undefined);
>> wm2.set(wm1, wm2); // 키와 값은 어떤 객체 가능
>>
>> wm1.get(o2); // "azerty"
>> wm2.get(o2); // undefined
>> wm2.get(o3); // undefined
>>
>> wm1.has(o2); // true
>> wm2.has(o2); // false
>> wm2.has(o3); // true ( 값이 undefined 이지만 )
>>
>> wm3.set(o1, 37);
>> wm3.get(o1); // 37
>>
>> wm1.has(o1); // true
>> wm1.delete(o1);
>> wm1.has(o1); // false
>> ```
>> ***
>> * Weakset
>> ```javascript
>> var ws = new WeakSet();
>> var obj = {};
>> var foo = {};
>>
>> ws.add(window);
>> ws.add(obj);
>>
>> ws.has(window); // true
>> ws.has(foo);    // false, foo가 집합에 추가되지 않았음
>>
>> ws.delete(window); // 집합에서 window 제거함
>> ws.has(window);    // false, window가 제거되었음
>> ```
***
> ### Meta programming
> ES6 버전이 자바스크립트에 적용되면서 생긴 두 객체 Proxy와 Reflect 덕분에 Property 조회, 설정, 열거, 함수 호출 등 다양한 사용자가 정의해서 사용할 수 있게 되었습니다. Proxy는 property lookup, assignment, enumeration, function invocation 등을 변경하는데 사용됩니다. Reflect는 자바스크립트 작업을 중간에서 가로챌 수 있는 built-in 객체이고 함수 객체가 아니므로 생성자(constructor)로 사용될 수 없습니다.
> * Proxy
> ```javascript
>  var handler = {
>   get: function(target, name){
>   return name in target ? target[name] : 42;
> }};
> var p = new Proxy({}, handler);
> p.a = 1;
> console.log(p.a, p.b); // 1, 42
> ```
> ***
> * Reflect
> ```javascript
> let obj = { a: 1 };
> Object.defineProperty(obj, "b", { value: 2 });
> obj[Symbol("c")] = 3;
> Reflect.ownKeys(obj); // [ "a", "b", Symbol(c) ]
> ```
***
> ### Promise
> Promise는 비동기 프로그래밍을 위한 라이브러리로, 현재 작업을 하는 것이 아니라 나중에 작업을 진행하는 것으로 기대되는 연산을 합니다.
> ```javascript
> function msgAfterTimeout (msg, who, timeout) {
>    return new Promise((resolve, reject) => {
>        setTimeout(() => resolve(`${msg} Hello ${who}!`), timeout);
>    });
> }
> msgAfterTimeout("", "Foo", 100).then((msg) =>
>     msgAfterTimeout(msg, "Bar", 200)
> ).then((msg) => {
>     console.log(`done after 300ms:${msg}`);
> });
> ```
***
> ### Parameter(default, rest)
> ES6 버전에는 값이 대입되어 있지 않은 변수에 특정한 값을 넣을 수 있는 default와 여러 가지의 변수를 받도록 할 수 있는 rest의 기능을 가지고 있습니다.
>>* default
>>```javascript
>> function f (x, y = 7, z = 42) {
>>    return x + y + z;
>> }
>> f(1) === 50;
>> ```
>>* rest
>> ```javascript
>> function f (x, y, ...a) {
>>    return (x + y) * a.length;
>> }
>> f(1, 2, "hello", true, 7) === 9;
>> ```
***
> ### ES6 new methods
> * Object Property Assignment
> ```javascript
> var dst  = { quux: 0 };
> var src1 = { foo: 1, bar: 2 };
> var src2 = { foo: 3, baz: 4 };
> Object.assign(dst, src1, src2);
> dst.quux === 0;
> dst.foo  === 3;
> dst.bar  === 2;
> dst.baz  === 4;
> ```
> ***
> * Array Element Finding
> ```javascript
> [ 1, 3, 4, 2 ].find(x => x > 3); // 4
> [ 1, 3, 4, 2 ].findIndex(x => x > 3); // 2
> ```
> ***
> * Number Type Checking
> ```javascript
> Number.isNaN(42) === false;
> Number.isNaN(NaN) === true;
>
> Number.isFinite(Infinity) === false;
> Number.isFinite(-Infinity) === false;
> Number.isFinite(NaN) === false;
> Number.isFinite(123) === true;
> ```
> ***
> * Number Comparsion
> ```javascript
> Number.isNaN(42) === false;
> Number.isNaN(NaN) === true;
>
> Number.isFinite(Infinity) === false;
> Number.isFinite(-Infinity) === false;
> Number.isFinite(NaN) === false;
> Number.isFinite(123) === true;
> ```
> ***
>
