# es6

- 新的语言特性

1. let 和 const 关键字，用于声明变量和常量
```
  var a = 1 // 不推荐使用
  let b = 1
  const c = 2
```
2. 箭头函数
```
  function fn() {} 
  等价于
  const fn = () => {}
```
3. 模板字符串
```
  const age = 10
  const a = age + '' // 不推荐使用
  const b = `${age}` // 推荐使用
```
4. 解构赋值
```
  /** 数组解构 */ 
  let [a, b, c] = [1, 2, 3];
  console.log(a, b, c); // 1 2 3

  /** 对象解构 */
  let {x, y} = {x: 1, y: 2};
  console.log(x, y); // 1 2
```
5. 默认参数值
```
  function foo(x, y = 2) {
    console.log(x, y)
  }

  foo(1); // 1, 2
  foo(1, undefined); // 1, 2
  foo(1, 3); // 1, 3
```
6. 剩余参数
```
  function foo(, b, ...rest){
    console.log(a); // 1
    console.log(b); // 2
    console.log(rest); // [3, 4, 5]
  }
  foo(1, 2, 3, 4, 5);
  ps: 在函数定义中，剩余参数必须是最后一个参数，否则会报错。
```
7. 类和继承
- ES6中引入了类（class）的概念，可以使用它来定义一个类。
```
  class Person {
    constructor(name, age) {
      this.name = name;
      this.age = age;
    }

    sayHello() {
      console.log(`my name is ${this.name}, I am ${this.age} years old`)
    }
  }

  class Student extends Person {
    constructor(name, age, grade) {
      super(name, age);
      this.grade = grade;
    }
    study() {
      console.log(`${this.name} is studying in grade ${this.grade}.`);
    }
  }
```

在上面的代码中，Student 类继承自 Person 类。在 Student 类的构造函数中，我们先调用了父类的构造函数 super(name, age)，然后再添加自己的属性 this.grade。

通过 extends 关键字可以实现继承。在子类中，可以使用 super 关键字来调用父类的构造函数和方法。

使用 extends 关键字继承的类会自动成为 constructor 方法的 super 对象。因此，在子类的 constructor 方法中必须先调用 super 方法，然后再添加自己的属性和方法。

在继承中，子类可以覆盖父类的方法。如果子类中定义了与父类同名的方法，那么在调用时将优先调用子类中的方法。如果需要调用父类的同名方法，可以使用 super 关键字。
<br >
8. 模块化
 - ES6 模块化通过关键字 import 和 export 实现模块的导入和导出：
```
// utils.js
const isNumber => value => typeof value === 'number'
const isString => value => typeof value === 'string'

exprot {isNumber}
exprot defualt isString

// index.jsx
improt isString, {isNumber} from './utils.js'
```
9. Promise
10. Symbol
11. Map 和 Set
12. 迭代器和生成器
13. for...of 循环
14. Proxy 和 Reflect