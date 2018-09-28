### 为什么使用`Typescript`
我们看一段代码
```javascript
class Greeter {
    greeting: string;
    constructor (message: string) {
        this.greeting = message;
    }
    greet() {
        return "Hello, " + this.greeting;
    }
}  
```

他生成的`Javascript`代码是这样的
```javascript
var Greeter = (function () {
    function Greeter(message) {
        this.greeting = message;
    }
    Greeter.prototype.greet = function () {
        return "Hello, " + this.greeting;
    };
    return Greeter;
})();
```
可以看到在`TS`中定义的类型在`JS`中是不存在的，但编译器可以通过他发现错误

- 发现错误变得更简单了
- 同时你还可以定义接口，通过接口来规范类或者结构体的编写

例如
```javascript
inteface A {
    a:string;
    b:string;
}

let rst: A = {
    a:"",
    b:""
}
```
这里给rst赋予类型A,则 a,b都必须为string;



###Typescript获取类名

```javascript
class MyClass {}

const instance = new MyClass();

console.log(instance.constructor.name); // MyClass
console.log(MyClass.name);                          
```


###Typescript定义二维数组

```javascript
let arr : any[][] = []
or
let arr : Array<Array<any>> = new Array<Array<any>>()
```


### interface vs type

使用`interface`
```javascript
interface Point {
    x: number;
    y: number;
}
```
使用`type`
```javascript
type Point = {
    x: number;
    y: number;
};
```
- `interface`可以在`extends`或`implements`子句中命名，但是`type`类型不能
	`typescript 2.7+`版本 `type`支持了`extends`和`implements`
- `interface`可以有多个合并声明，但`type`类型不能

例如
```javascript
interface a {
    a:string
}

interface b {
    b:string
}
```
等同于
```javascript
interface c {
    a:string
    b:string
}
```
声明两个同名`type`会报错