
Brain teasers every day
每日脑残题
====
> 最近喜欢上了做一些看起来比较简单实际上考察的有点‘脑残’的那种题型，
> 之前一直是发在别的地方，今天有闲功夫，想把之前发过的整理下，以备后续查看。

ES6系列
-------
```js
经典题目   
一、
    ['10','10',10',10'].map(parseInt)
    运行结果：[10 ,NaN, 2,3]

    这道题考察的是对数组的map()方法的参数，以及parseInt（）方法的参数的理解，
    1、map()方法创建一个新数组，其结果是该数组中的每个元素是调用一次提供的callback函数后的返回值。
    2、callback 函数会被自动传入三个参数：数组元素，元素索引，原数组本身。
    3、parseInt(string, radix)   解析一个字符串并返回指定基数的十进制整数， radix 是2-36之间的整数，
    表示被解析字符串的基数。
    4、parseInt的返回值：从给定的字符串中解析出一个整数，或者NaN，
    （当radix小于2或者大于36，或者第一个非空字符串不能转换为数字）

二、
    let x = 1;
    let y = 2;
    [x,y]=[y,x]
    console.log(x,y)//2,1
    合理地使用数组的解构赋值，某些情况下可以快速的交换变量的值；
三、
    console.log([[1, 2], [3, 4],[5,6].map(([a, b]) => a + b))
    输出：[3,7，11]
    数组：[[1,2],[3,4],[5,6] 调用map方法，map方法内部是一个回调函数，默认会传入数组的项，下标，数组本身，
    对与数组的第一项[1,2]首先传入，item:[1,2];index:0;array:数组本身；
    map内部的会掉函数对传入的参数进行解构赋值，因为参数是一个数组的形式（[1,2}）对其进行解构，[a,b]=[1,2],返回a+b 即 1+2 =3,返回值组成一个数组，
    对与原来数组的第二项亦是如此，返回3+4=7，最终返回数组：[3,7,11]
    
    另一个例子：function add([x, y]){
    return x + y;
    }
    add([1, 2]); // 3
    
四、
        var obj = {
        foo: function () { console.log(this.bar) },
        bar: 1
        };
    声明一个e对象，对象中保存着一个名为foo的方法；该方法可以打印对象obj的另一个属性bar,
    
    我们吧这个obj下的foo方法赋值给声明在全局中的foo方法，
    我们分别调用该方法，输出不同的bar变量，
    obj.foo输出的是与其在同一作用域的变量，全局的foo方法输出全局的bar变量
        var foo = obj.foo;
        var bar = 2;

        obj.foo() // 1
        foo() // 2
        
    JavaScript 允许在函数体内部，引用当前环境的其他变量。
    由于函数可以在不同的运行环境执行，所以需要有一种机制，能够在函数体内部获得当前的运行环境（context）。
    所以，this就出现了，它的设计目的就是在函数体内部，指代函数当前的运行环境。

```


​        

​        五、

```js
        let obj={
            ['a'+'b']:123,
            ['he'+'llo']:()=>{
                console.log('hi')
            }
        }
        obj.hello()             //hi
        console.log(obj.ab)     //123
```

ES6允许使用表达式作为对象的属性名或者方法名

六、

```js
const proto = {
  foo: 'hello'
};

const obj = {
  foo: 'world',
  find() {
    return super.foo;
  }
};

Object.setPrototypeOf(obj, proto);
obj.find() // "hello"
```

​              我们知道，`this`关键字总是指向函数所在的当前对象，ES6 又新增了另一个类似的关键字`super`，指向当前对象的原型对象。

Class 可以通过extends关键字实现继承，这比 ES5 的通过修改原型链实现继承，要清晰和方便很多。

```js
class ColorPoint extends Point {
  constructor(x, y, color) {
    super(x, y); // 调用父类的constructor(x, y)
    this.color = color;
  }

  toString() {
    return this.color + ' ' + super.toString(); // 调用父类的toString()
  }
}
```
 子   类必须在constructor方法中调用super方法，否则新建实例时会报错。
 这是因为子类自己的this对象，必须先通过父类的构造函数完成塑造，得到与父类同样的实例属性和方法，
 然后再对其进行加工，加上子类自己的实例属性和方法。如果不调用super方法，子类就得不到this对象。
9-19日

## common.js 与ES6模块异同

```
讨论 Node.js 加载 ES6 模块之前，必须了解 ES6 模块与 CommonJS 模块完全不同。

它们有三个重大差异。

CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。
CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。
CommonJS 模块的require()是同步加载模块，ES6 模块的import命令是异步加载，有一个独立的模块依赖的解析阶段。
```

#### CommonJS 模块输出的是值的拷贝，也就是说，一旦输出一个值，模块内部的变化就影响不到这个值。请看下面这个模块文件`lib.js`的例子。

```js
// lib.js
var counter = 3;
function incCounter() {
  counter++;
}
module.exports = {
  counter: counter,
  incCounter: incCounter,
};
```

七、

```js
        quit({commit}){
            commit('QUIT')
            commit('tagsview/DEL_ALL',null,{root:true})
        }
```

在一个store的模块调用另一个模块的方法，要传递三个参数吧，

第一个参数，目标方法所在模块的“路径”（模块名/方法）

第二个参数，给目标传递的实参，“DATA”,即使没有也应该使用null或者{}占位

第三个参数，是配置参数，表明使用的其他模块的方法。

此外还有rootGetters方法，可以调用其他模块的getters

```js
console.log(rootGetters['user/getuser'])
```

