> 发布自[Kindem的博客](http://www.kindemh.cn/)，欢迎大家转载，但是要注意注明出处

# 什么是lambda表达式
lambda表达式基于数学中的λ演算演算得名，直接对应其中的lambda抽象。而在编程中，你只需要知道lambda表达式是一中匿名函数就行了。

# C#中的lambda表达式
说到C#中的lambda表达式，就需要先说一说C#的委托(delegate)，C#的委托和C或C++的指针很类似，委托是存有对某个方法的引用的一种引用类型变量，这种引用可以在运行时被改变。你可以把他理解为存放函数的变量。

在C#中，类似这样声明一个委托：
```csharp
public delegate int doSomething(int p);
```
像这样的委托可以接受任何带有一个int型参数并且返回一个int型变量的函数

然后你就可以使用这个委托实例化，接受任何满足条件的函数并且使用委托来调用它了：
```csharp
// 假设存在函数
// int double(int p) { return p * 2; }
// int split(int p) { return p / 2; }
doSomething do1 = new doSomething(double);
doSomething do2 = new doSomething(csharp);

do1(4);
do2(8);
```
委托的思想其实从某种意义上也是一种泛型。

而我们的lambda表达式不正是匿名函数吗？显而易见它可以和委托很好地配合，在C#，lambda表达式要像这样写：
```csharp
x => x * 2
// 如果有多个参数
(x, y, z) => x + y + z
// 如果有多条语句
x => { int y = x * 2; return y; }
```
当然，通常它们会和委托搭配使用：
```csharp
doSomething do3 = new doSomething(x => x * 2);
```
这样只要调用委托就能访问匿名函数了。

# Java中的lambda表达式
在java中，lambda表达式有一些特殊，其他的绝大多数语言中，lambda表达式都被解释成匿名函数，但是在java中，匿名函数将会被解释成一个内部类中的接口函数。

在java中有很多使用匿名内部类的情况，比如多线程和安卓开发中各种各样的接口等，而这些匿名内部类通常只有一个接口函数，遇到这种情况就能使用java的lambda表达式，使用lambda表达式之后，lambda表达式代表的匿名函数将会自动被解释成可传递的内部类中唯一的哪一个接口函数。

在java中，lambda表达式和其他的很类似，只是改成了
```java
x -> x * 2
```

像安卓开发中的事件绑定，如果没有使用lambda表达式：
```java
button.addActionListener(new ActionListener() {
  public void actionPerformed(ActionEvent actionEvent) {
    System.out.println("Actiondetected");
  }
});
```
可见大多数事件绑定中都是只有一种可能性，这种情况下改用lambda表达式：
```java
button.addActionListener((e) -> {
  System.out.println("Actiondetected");
})
```

当然多线程也能使用lambda表达式：
```java
Runnable run = () -> {
  //...
};
```

最后一定要注意一点，java的lambda表达式从java8才开始被支持，之前的版本一定不要乱用。

# python中的lambda表达式
很多其他的语言都是在日后的更新和维护中才把lambda表达作为一个特性，而python却直接支持lambda表达式，python的lambda表达式更简单易用，因为它在设计之初就只把lambda当成一种特殊函数而不是什么奇奇怪怪的东西，像这样：
```python
double = lambda x: x * 2
double(4)
```

# JavaScript ES6中的箭头函数
JavaScript E6中的lambda表达式被称为箭头函数，语法和C#的很类似：
```javascript
x => x * 2
```
在JavaScript中，箭头函数用的最多的地方就是作为钩子函数，因为钩子函数通常意义上都是匿名函数而且是一次性的，复用性差，非常符合箭头函数的发挥场景。

除了通常意义上的lambda表达式优点，JavaScript ES6中的箭头函数还有独到的优势，就是在箭头函数中的this会指向外部的this，这一特点在React的开发中起到了巨大作用，如果不使用箭头函数作为钩子函数而是声明一个普通的函数，将需要手动将函数体内部的this绑定到外部this，才不会引起一些奇奇怪怪的错误：
```javascript
// react开发举例
class ClickToSendHello extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <div>
        <button onClick={() => {
          alert('Hello!');
        }}>Send</button>
      </div>
    );
  }
}
```
