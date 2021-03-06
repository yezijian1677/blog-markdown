![React](../../img/public/react-logo.png)

> 发布自[Kindem的博客](http://www.kindemh.cn/)，欢迎大家转载，但是要注意注明出处

# 开始之前
该React教程系列的前两节基本上都只是对React的认识和学习之前的铺垫，从本节开始，将真正介绍React的功能和使用，所以需要搭建React的开发环境。

创建一个React项目的最简方法就是使用官方的create-react-app库来创建React项目，你可以看这里：
[使用create-react-app来创建react项目-Kindem的博客](http://www.kindemh.cn/post/15)

这里推荐使用JetBrain家的WebStorm来进行开发，当然，create-react-app也可以被集成在WebStorm中使用，这里就不再赘述了，使用WebStorm，你可以很方便地检测你ES6和JSX的语法错误，并且能够一键打开CMD进行配置、测试等，非常方便。

另外，这里还要再次强调一下，**React的项目中，只有一个index.html文件**，这一个index.html就承担了整个站点的功能，如果你需要构建多个页面，则需要使用React Router来配置路由，而不是每一个页面写一个html和js文件，这是因为React的原则是将原页面重新“渲染”，而不是重新加载。另外值得一提的是，create-react-app使用的默认打包工具是webpack，其配置文件并没有将所有的js文件与html文件对应打包，而是将所有js文件打包在一起，所以，官方是怎么做的，大概也就能说明怎么做比较合理了吧。

# Hello, React!
使用一门编程语言或者一个库的第一件事情，当然是先Hello一下了，下面，就在React的世界中写一个Hello World吧，当然你先不用看懂所有代码，之后会慢慢解释：

/public/index.html
```html
<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <title>React-Test</title>
</head>
<body>
    <div id="root"></div>
</body>
</html>
```
index.html文件就像上面这样写，**当然以后，未经说明，该文件不会再变动**，React的思想是，你只管写js文件就行了，其他的交给它。

/src/index.js
```javascript
import React from 'react';
import ReactDom from 'react-dom';

class HelloWorld extends React.Component {
    render() {
        return (
            <div>
                <h1>Hello, World!</h1>
            </div>
        );
    }
}

ReactDom.render(
    <HelloWorld/>,
    document.getElementById('root')
);
```
接下来在命令行中输入
```
npm run start
// 如果你安装了yarn，也可以使用
yarn start
```
来开启调试服务器，稍等之后输入命令行中告知你的url，就可以看到页面效果了：
![Hello, World](../../img/2018/4/4-6-0.png)

现在来解释一下代码，html文件我们自然不用关注，因为React的原则就是让你专注于js组件的构建，整个站点只有一个html文件，让我们看看index.js。

```javascript
import React from 'react';
import ReactDom from 'react-dom';
```
这两条语句是ES6的导包语句，React是React的核心类，而ReactDom操作是对React中DOM操作的封装。

然后再看
```javascript
class HelloWorld extends React.Component {
  ...
}
```
这就是我们一直所说的React组件，一个React组件就是一个继承自React组件基类的ES6类，之后会详细介绍，至于
```javascript
ReactDom.render(
    <HelloWorld/>,
    document.getElementById('root')
);
```

它的作用是把一个组件渲染到index.html中的DOM元素中，尖括号包裹类名则是React组件的使用方法。

# React组件
通过上面的例子，你对React组件也了解了一个大概了，React组件是React最基本的元素，在React的世界中，万物皆为组件。那么该如何写一个React组件呢？

```javascript
class ComponentName extends React.Component {
    render() {
        return (...);
    }
}
```

这就是写一个最简单的React组件的办法，你只需要写一个ES6类，以你想要的组件名为类名，这个类必须要继承自React的组件基类React.Component，并且至少要复写其中一个方法——render()，这个方法需要返回一个JSX，用来表示该组件被渲染的时候，需要加载到DOM中的内容。

写好了组件之后，你就可以通过类名+xml标签的形式来使用React组件，你可以将其作为参数传递，也可以在其他的React组件中使用它，向下面这样：
```javascript
import React from 'react';
import ReactDom from 'react-dom';

class Hour extends React.Component {
    render() {
        return (
            <span>17</span>
        );
    }
}

class Minute extends React.Component {
    render() {
        return (
            <span>58</span>
        );
    }
}

class Time extends React.Component {
    render() {
        return (
            <div>
                Current Time:
                <Minute/>
                <span>:</span>
                <Hour/>
            </div>
        );
    }
}

ReactDom.render(
    <Time/>,
    document.getElementById('root')
);
```

看到这里，也许你对React组件的了解又更深了一些，现在差不多了解为什么React要使用组件化的思想了，用这一种方法来构建一个页面，只需要将页面中可能出现的各种可复用的代码块单独抽出来构成组件，写页面的时候就能将代码结构化，并且提高代码复用性。

这种思想是不是和各种OO语言中的面向对象思想很像？封装和复用，这就是React组件的魅力。

这一节到这里就结束了，你已经了解到了写一个最基本的React组件的方法，在下一节中，我会为大家介绍React组件的两大灵魂之一——props(属性)，欢迎大家关注。
