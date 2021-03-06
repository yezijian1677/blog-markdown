![React](../../img/public/react-logo.png)

> 发布自[Kindem的博客](http://www.kindemh.cn/)，欢迎大家转载，但是要注意注明出处

# 写在前面

`ES6`和`JSX`是`React`推荐使用的`js`语法特性和扩展语法，当然他们也不是`React`必须使用的玩意，只是使用他们的时候，能使`React`代码的书写变得更加简洁，所以推荐使用。



如果你从来没有听说过这俩，也完全没有关系，其实他们很简单，只需要这一篇文章，就能了解一个大概。



# 1. `ECMAScript 2015`(`ES6`)

众所周知`ECMAScript`是`JavaScript`的一个标准，`ES6`则是新一代的标准，关于它的名字你只需了解那么多就够了，它的兼容性不如老一代的标准，很多浏览器甚至还不兼容(比如万恶的老一代`IE`)，但是它带来的语法糖和新特性是十分诱人的，因为`Babel`等库的出现，`ES6`能够被编译成老一代的兼容性`js`代码从而兼容各种浏览器，所以，你大可放心使用`ES6`的新特性。



下面则开始介绍在`React`中常用的`ES6`新特性：

## 1.1 `let`、`const`

`ES6`增加了`let`和`const`来代替从前的`var`变量声明。



`let`的使用方法很像以前的`var`，但是不同的地方是`let`是拥有作用域的，`let`声明的变量将只在其所在的代码块才起作用，这样就避免了不同作用域声明的`var`互相污染的问题，来看一个例子：

```javascript
{
    let a = 10;
    var b = 1;
}

console.log(a);	// 报a的undefined错误，因为a的作用域在括号内
console.log(b); // 不报错
```

而`const`则是用来声明只读常量的命令，一旦声明，被声明的常量的值就无法被修改，比如这样：

```javascript
const a = 1;

a = 2; // 报错，const声明的值无法被修改
```



## 1.2 箭头函数

箭头函数是`ES6`添加的一种新函数，用于快速构造一个匿名函数，在各种事件、回调等场合能够发挥大作用。



举几个例子：

```javascript
x => 5 * x
// 相当于
// function(x) {
//     return 5 * x;
// }

x => {
    if (x <= 0) {
        return true;
    } else {
        return false;
    }
}
// 相当于
// function(x) {
//     if (x <= 0) {
//         return true;
//     } else {
//         return false;
//     }
// }

(x, y) => x * 2 + y * 2
// 相当于
// function(x, y) {
//     return x * 2 + y * 2;
// }
```

看了上面的几个例子，你差不多已经对箭头函数有了一定了解了吧，箭头函数的主要语法就是使用箭头=>来连接参数块和函数体，如果参数只有一个，参数块可以不使用括号包裹，但是如果有多个参数则需要使用括号包裹，函数体的返回结果如果为一个可以直接得出的表达式或值，就可以不用括号包裹直接给出，但是如果不能，则要将函数体完全写出，并且使用大括号包裹。



另外，箭头函数最大的优点就是箭头函数内部的`this`是指向外部语义块的`this`的，通常我们写的函数如果想调用外部的`this`，则需要先将函数`bind`到外部的`this`，但箭头函数不用，这就是为什么箭头函数在`React`的事件处理中用的非常多的原因，举一个例子：

```javascript
var obj = {
    birth: 1990,
    getAge: function () {
        var b = this.birth; // 1990
        var fn = function () {
            return new Date().getFullYear() - this.birth; // this指向window或undefined
        };
        return fn();
    }
};
```

但是如果我们使用箭头函数：

```javascript
var obj = {
    birth: 1990,
    getAge: function () {
        var b = this.birth; // 1990
        var fn = () => new Date().getFullYear() - this.birth; // this指向obj对象
        return fn();
    }
};
obj.getAge(); // 25
```



## 1.3 `ES6` 类

在传统的`JavaScript`中，类的定义和使用时依赖构造函数的编写来实现的，这和传统`oo`语言的思想有着非常大的区别，而在`ES6`中，为了让`JavaScript`的`oo`更加贴切传统语言的写法，推出了新的类写法。



举一个例子：

```javascript
class Person {
    constructor(name, sex) {
        this.name = name;
        this.sex = sex;
    }

    getInfo() {
        return {
            name: this.name;
            sex: this.sex;
        }
    }
}
```

`constructor`则是构造方法，在`ES6`类中，所有的方法都直接放入类内部，方法与方法之间不需要加分号，加了会报错。



需要使用这个类来构造对象的时候，只需要像传统面向对象语言一样使用`new`关键字即可：

```javascript
let kindem = new Person('John Kindem', 'male');
```



`ES6`类中也存在着静态方法，也就是类的所有对象共用的方法，声明的时候，只需要在前面添加`static`关键字即可：

```javascript
class NUAAStudent {
    static getSchool() {
        return 'NUAA';
    }
}

let kindem = new NUAAStudent();
console.log(kindem.getSchool());
console.log(NUAAStudent.getSchool());
```

两者输出的字符串将会是一样的。



另外，`ES6`也有继承的概念，比如下面的例子：

```javascript
class Student {
    constructor(name, number) {
        this.name = name;
        this.number = number;
    }

    getName() {
        return this.name;
    }

    getNumber() {
        return this.number;
    }

    getInfo() {
        return {
            name: this.name;
            number: this.number;
        }
    }
}

class CollegeStudent extends Student {
    constructor(name, number, collegeName) {
        super(name, number);
        this.collegeName = collegeName;
    }

    getName() {
        return this.name;
    }

    getNumber() {
        return this.number;
    }

    getCollegeName() {
        return this.collegeName;
    }

    getInfo() {
        return {
            name: this.name;
            number: this.number;
            collegeName: this.collegeName
        }
    }
}
```

`ES6`类使用`extends`完成类与类的继承，子类将会获取父类的所有属性与方法，并且能够添加新的属性、方法，或是复写父类的属性、方法。



这里要注意的是，子类必须调用`super()`，来调用父类的构造函数，否则子类将无法构建。



## 1.4 more

当然`ES6`的新特性并不只这一点，只是这些特性在`React`中使用的比较多，关于`ES6`，你了解这几个新特性就差不多了，就已经能够进入`React`的战场了，但是如果你想学习完整的`ES6`特性，你可以参考阮一峰的`ES6`教程：

[ECMAScript 6入门](http://es6.ruanyifeng.com/#docs/class-extends)



# 2 `JSX`

## 2.1 `JSX`是什么?

我们先来看一个使用`JSX`的例子：

```javascript
const helloWorld = <h1>Hello, World!</h1>
```

乍一看，这一个变量是不是有点奇怪，它既不是一个字符串也不是`HTML`，这就是`JSX`，它的存在是为了解决在`JavaScript`中写`HTML`十分痛苦的问题。



如果你使用过`jQuery`或者原生`JavaScript`来对`html`中的`DOM`节点添加新的元素的时候，你可能会体会到这一件事情有多么痛苦，就像这样：

```javascript
$('#helloBlock').append(
	'<h1>Hello, World!</h1>'
);
```



更加可怕的如果你要使用`JavaScript`代码添加大量的`DOM`节点，你就必须不断使用+号来连接每一行的`html`字符串，这样会大大降低代码执行的效率。



每一个涉及到`DOM`操作的界面库，都避免不了这种问题，`React`也是一样，这就是为什么`JSX`被广泛运用在`React`中的原因。



那么`JSX`要怎么使用呢？



你可以把`JSX`认为是一个值，就像`1`,`'hello'`这样，`JSX`通常只有一个根标签，根标签内部可以有很多子标签或者嵌套，通常，使用`JSX`的时候需要使用小括号将其包裹起来，作为一个值使用：

```javascript
// 正确
const hello = (
	<div>
    	<h1>John Kindem</h1>
    	<h2>A student in NUAA.</h2>
    </div>
);

// 错误，一个JSX值中只能有一个根标签
const hello = (
    <h1>John Kindem</h1>
    <h2>A student in NUAA.</h2>
);
```



既然`JSX`是一个值，你大可将将其赋值给变量、作为返回值、作为参数传递，这些都是可以的：

```javascript
function getHelloWorldJSX() {
    return (
    	<h1>Hello, World!</h1>
    );
}
```



## 2.2 在`JSX`中使用表达式

当然你也可以在`JSX`中任意使用表达式，不过表达式在`JSX`中需要使用大括号包裹起来：

```javascript
const date = {
    year: '2018',
    month: '4',
    day: '1'
}

const getWeather(day) {
    if (day === '1') {
        return 'sun';
    } else {
        return 'rain';
    }
}

function getTodayInfoJSX() {
    return (
    	<div>
        	<h1>date: {date.year + date.month + date.day}</h1>
        	<h1>weather: {getWeather(date.day)}</h1>
        </div>
    );
}
```



关于`ES6`和`JSX`就介绍到这里了，至于一些额外的细节，在以后详细介绍`React`的时候会顺便给大家讲，当然，如果需要更加详细地了解`ES6`和`JSX`，可以登录他们的官方文档查阅。



在`React`轻松入门系列的下一篇文章中，我会给大家介绍如何写一个`React`组件，并且在其他组件中使用它或是将其直接渲染，欢迎大家关注我和我的个人博客了解详情。
