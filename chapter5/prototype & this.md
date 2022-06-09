### prototype

prototype은 JavaScript에서 상속을 하기 위해 만들어졌다.
prototype을 사용해서 코드를 재사용 할 수 있다

```javascript
const x = {};
const y = {};

// x 와 y 는 동일한 proto를 상속받기 때문에 true
console.log(x.__proto__ === y.__proto__);

function CoffeeMachine(beans) {
  // 만들어지는 instance마다 생성된다.
  this.beans = beans;
}
const machine1 = new CoffeeMachine(10);
const machine2 = new CoffeeMachine(20);

// CoffeeMachine prototype에 makeCoffee 함수 추가
// CoffeeMachine으로 만들어진 instance는 모두 makeCoffee 함수를 갖는다.
CoffeeMachine.prototype.makeCoffee = (shots) => {
  console.log(`making... ${shots}coffee`);
};

function LatteMachine(milk) {
  this.milk = milk;
}

// CoffeeMachine 상속
LatteMachine.prototype = Object.create(CoffeeMachine.prototype);

const latteMachine = new LatteMachine(123);
latteMachine.makeCoffee(2);
```

---

### this

JavaScript에서 this 동작

```javascript
// 전역객체(window / global)를 기리킨다
console.log(this);

function simpleFunc() {
  console.log(this);
}
simpleFunc(); // window window.simpleFunc()와 동일

class Counter {
  count = 0;
  increase = function () {
    console.log(this);
  };
}

const counter = new Counter();
counter.increase(); // Counter
// this의 정보를 잃는다.
// const 와 let으로 선언된 변수는 window에 등록되지 않는다.
const caller = counter.increase;
// 따라서 undefined
caller();
const caller2 = counter.increase.bind(counter); // this binding
caller2(); // counter

class Bob {}
const bob = new Bob();
bob.run = counter.increase;
bob.run(); // bob
```
