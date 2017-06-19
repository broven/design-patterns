# Strategy 策略模式

## 适用场景
有几种相似的行为, 由客户端来决定使用哪一种. 比如说:
- 选择不同种的快递公司 (ups, express, 顺丰), 它们暴露出的行为都是一样的, 比如都暴露出一个send()方法
- 不同种的排序算法. 你写了很多种排序, 客户端可以自行选择一个使用, 可以见我[另一个repo](https://github.com/broven/Algorithms/blob/master/src/sort/sortTest.java#L49), 这里我在学习不同排序算法时误打误撞使用了策略模式, 所有的算法类都提供了一个sort方法

# Strategy in JAVA
在JAVA中一个基本的策略模式是这样的
```JAVA
interface IStrategy {
  public void doSomething();
}
class Strategy1 imlements Istrategy {
  public void doSomething() {
    System.out.println("Strategy1");
  }
}
class Strategy2 imlements Istrategy {
  public void doSomething() {
    System.out.println("Strategy2");
  }
}
....

class Context {
  private Strategy strategy;
  public Context(IStrategy strategy){
    this.strategy = strategy;
  }
  public void execute(){
    strategy.doSomething();
  }
}
```
使用:
```JAVA
public class Client {
  public static void main(String[] args){
    Context context;
    System.out.println("-----执行策略1-----");
    context = new Context(new ConcreteStrategy1());
    context.execute();

    System.out.println("-----执行策略2-----");
    context = new Context(new ConcreteStrategy2());
    context.execute();
  }
}
```

其实在学会的面向对象的思想之后, 这样写十分的自然, 然后大佬们把它抽出来, 变成了一个约定俗成的模式.

# 优缺点
## 优点
- 增加一个新的方法时不需要修改以前的方法, 添加新的if...else
## 缺点
- 需要向使用者暴露所有的策略类, 使用者还需要了解各种不同的策略有啥区别
- 维护各个策略类会给开发带来额外开销(大佬说的, 我还不太理解这条)

## Strategy in JS
策略模式在JS中就不需要JAVA那一套了, 我们直接用函数就可以
```javascript
let strategies = {
  Strategy1: function () {
    console.log('Strategy1')
  },
  Strategy2: function () {
    console.log('Strategy2')
  }
}


let Context = function (strategy) {
  this.str = strategy
}
Context.prototype.execute = function() {
  return this.str()
}
```

使用:
```javascript
let context = new Context(strategies.Strategy1)
context.execute()
```