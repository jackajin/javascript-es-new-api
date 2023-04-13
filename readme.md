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
```
const promise1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('promise1');
    }, 1000);
})
const promise2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('promise2');
    }, 2000);
})
const promise3 = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject('promise3');
    }, 1000);
})

// 所有的Promise对象均成功后才会执行all中的then回调，否则返回的是最先rejected状态的值。
Promise.all([promise1, promise2, promise3]).then(res => {
  console.log(res) ['promise1', 'promise2', 'promise3']
}).catch(res => {})

// 所有的Promise对象均出现结果（无论成功或失败）后才会执行allSettled中的then回调（只会进入then回调）
Promise.allSettled([promise1, promise2, promise3]).then((values) => {
    console.log('allSettled_then', values)
}).catch(reason => {
    console.log('allSettled_catch', reason)
})

// 和all相反，所有的Promise对象均失败后才会执行any中的失败回调，否则当任意一个Promise对象成功就会直接进入then回调。
Promise.any([promise1, promise2, promise3]).then((values) => {
    console.log('any_then', values)
}).catch(reason => {
    console.log('any_catch', reason)
})

// 顾名思义，谁跑得快就返回当前Promise状态的值
Promise.race([promise1, promise2, promise3]).then((values) => {
    console.log('race_then', values)
}).catch(reason => {
    console.log('race_catch', reason)
})
```
10. Symbol
- Symbol是ES6中新增的一种数据类型, 被划分到了基本数据类型中，表示独一无二的值
```
const name = Symbol('name')
```
11. Map 和 Set
```
// Set 构造函数能让你创建 Set 对象，其可以存储任意类型的唯一值，无论是基本类型或者对象引用。
const set1 = new Set([1, 2, 3, 4, 5]); //Set(5) {1, 2, 3, 4, 5}

// 返回一个布尔值，表示该值在 Set 中存在与否。
set1.has(6) // false 

// 在Set对象尾部添加一个元素。返回该 Set 对象
set1.add(6)

// 删除元素
set1.delete(6)

// Map 对象保存键值对，并且能够记住键的原始插入顺序。任何值（对象或者基本类型）都可以作为一个键或一个值。类似于对象。

const map1 = new Map();
map1.set('a', 1);

map.get(a) // 1

map1.size // 1
```
12. 迭代器和生成器
```
// 迭代器
let arr = [1, 2, 3]
let myIte = arr[Symbol.iterator]()
console.log(myIte.next()); //{value: 1, done: false}
console.log(myIte.next()); //{value: 2, done: false}
console.log(myIte.next()); //{value: 3, done: false}
console.log(myIte.next()); //{value: undefined, done: true}

// 生成器
function *ride(num){
    console.log("函数执行了...");
    yield num*2;
    console.log("第二步...");
    yield num*4;
    console.log("第三步...");
    yield num*8;
    console.log("函数执行end...");
}
const myride=ride(10) //生成器函数调用的时候 会生成一个迭代器对象

console.log(myride.next()); //{value: 20, done: false}
console.log(myride.next()); //{value: 40, done: false}
console.log(myride.next()); //{value: 80, done: false}
console.log(myride.next()); //{value: undefined, done: true}
```

13. for...of 循环
- for…of 循环允许您遍历可迭代对象（数组、集合、映射、字符串等）
```
// for…of 与数组
const students = ['John', 'Sara', 'Jack'];
for(let item of students ){
  console.log(item) // 'John', 'Sara', 'Jack'
}

// for…of 与字符串
const string = 'code';
for (let i of string) {
    console.log(i) // c, o, d, e
}

// for…of 与 Set
const set = new Set([1, 2, 3])
for(let i of set){
  console.log(i) // 1, 2, 3
}

// for…of 与 Map
const map = new Map()
map.set('name', 'ajin')
map.set('age', 18)

for(let [key, value] of map){
  console.log(key + '-' + value)// name-ajin, age-18
}

// for…of 循环遍历迭代器
const iterableObj = {
  [Symbol.iterator](): {
    let step = 0
    return {
      next(){
        step++
        if (step === 1) {
            return { value: '1', done: false};
          }
          else if (step === 2) {
            return { value: '2', done: false}
          }
          else if (step === 3) {
            return { value: '3', done: false};
          }
          return { value: '', done: true };
      }
    }
  }
}
for (const i of iterableObj) {
 console.log(i);
}

// for…of 与生成器
function* generatorFunc() {
  yield 10;
  yield 20;
  yield 30;
}
const obj = generatorFunc();
for (let value of obj) {
  console.log(value);
}
```
14. Proxy 和 Reflect

```
let obj = {a: 1, b: 2}
const poxyObj = new Poxy(obj, {
  // 依次为目标对象、属性名和 proxy 实例本身
  get: function(arget, attr, receiver) {
    return target[attr]
  },
  // 目标对象, 属性名, 属性值, proxy 实例本身
  set: function(target, attr, value, receiver) {
     target[attr] = value;
  }
})
```
- Reflect 是一个内置的对象，它提供拦截 JavaScript 操作的方法，是 ES6 为了操作对象而提供的新 API。
- Reflect不是一个函数对象，因此它是不可构造的。
- Reflect的所有属性和方法都是静态的。

### Api
1. Array.from()
```
  // 将一个类数组对象或者可遍历对象转换成一个真正的数组
  Array.from(new Set([1,2,3,4])) // [1,2,3,4]

  // 第二个参数类似于map
  Array.from(new Set([1,2,3,4]), item => item + 1) // [2, 3, 4, 5]
```
2. Array.of()
- 方法用于将一组值，转换为数组
```
Array.of(3, 11, 8) // [3,11,8]
Array.of() // []
```
3. Array.prototype.includes()
- 方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回 false
```
[1,2,3,4].includes(1) // true
[1,2,3,4].includes('1') // false
// 第二个参数代表，从第几位开始，默认0
[1,2,3,4].includes(1, 3) // false
```
4. Array.prototype.find()
- Array.prototype.find()方法用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有的数组成员依次执行这个回调函数，直到找出第一个返回值为true的成员，然后返回该成员。如果没有符合条件的成员，则返回undefined。

```
[1,2,3].find(it => it === 2) // 2
[1,2,3].find(it => it === 4) // undefined
```

5. Array.prototype.findIndex()
- Array.prototype.findIndex()方法返回满足测试条件的第一个元素的索引。如果没有元素满足，则返回-1。
```
[1,2,3].findIndex(it => it === 2) // 1
[1,2,3].findIndex(it => it === 4) // -1
```
6. String.prototype.startsWith()
- 判断当前字符串是否以给定的字符串作为开头。
```
'abcdefg'.startsWith('abc') // true
// 第二个参数表示第几位开始，负数为零
'abcdefg'.startsWith('abc', 1) // false
```
7. String.prototype.endsWith()
- 判断当前字符串是否以给定的字符串作为结尾。
```
'abcdefg'.startsWith('efg') // true

// 第二个参数默认是字符串的长度
'abcdefg'.startsWith('efg', 6) // true
```
8. String.prototype.includes()
- 判断字符串中是否包含了另一字符串
```
const str = "abcdefgh";
str.includes("def");     // true
str.includes("DEF");     // false
str.includes("def", 4);  // false，相当于在"efgh"中搜索"def"
str.includes("def", 3);  // true，相当于在"defgh"中搜索"def"
str.includes("def", -3); // true，相当于在原字符串中搜索"def"
```
7. Object.assign()
- 方法用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象
- 参数： target--->目标对象
       source--->源对象
       返回值：target，即目标对象
```
Object.assign(target, ...sources)
```
8. Object.is()
- 方法判断两个值是否是相同的值。
- 这种相等性判断逻辑和传统的 == 运算符所用的不同，== 运算符会对它两边的操作数做隐式类型转换（如果它们类型不同），然后才进行相等性比较，（所以才会有类似 "" == false 为 true 的现象），但 Object.is 不会做这种类型转换。
```
 这与'==='运算符也不一样。'===' 运算符（和==运算符）将数字值-0和+0视为相等，并认为Number.NaN不等于NaN
```
