一.接口的定义

1.1什么是接口,为什么使用接口

1. 接口解决多重继承

1. ts的核心原则之一是对值所有的结构类型进行类型检查

2. 鸭式辩型法或结构性子类型化

3. 接口作用为类型命名和代码定义契约

   ------

   1.2如何定义一个接口

```typescript
function printLabel ( labelledObj: { label: string }) {
  console.log(labelledObj.label)
};

let myObj = {label: '1', size: 10};
printLabel(myObj); //类型检查器

interface LabelledValue {
  label: string;
}

function printLabel1(labelledObj: LabelledValue) {
  console.log(labelledObj.label)
}

```

1.3接口的特点

是interface不会检查属性的顺序 只检查是否存在

可选参数 (option bags模式) → 给函数传入的参数只有部分属性赋值

优点 1.对存在的属性预定义,2.捕获引用不存在的属性错误

```typescript
interface SqyureConfig {
  color?: string;
  width?: number;
}
```

//只读属性
```
interface Point {
  readonly x: number;
  readonly y: number;
}
```
// 通过 一个对象字面量赋值 但是赋值后不能被改变
```
let p1: Point = {x: 10, y: 11}
p1.x = 5 //error!

```
// ts 具有ReadonlyArray<T>类型 和Array<T>相似 确保数组创建不能被修改
```
let a:number[] = [1,2,3,4,5];
let ro: ReadonlyArray<number> = a;
ro[0] = 12; //error
a = ro //error
//把整个ReadonlyArray赋值给一个普通数组也不行  但是可以用类型断言重写
a = ro as number[];
// readonly和const 变量用cosnt 属性用readonly
```

函数类型

定义:接口能够描述javascript中对象拥有的各种变量  →  接口和类相似

```typescript
interface SearchFunc {
    //定义方法签名
  (source: string, sub: number): boolean
}

let search : SearchFunc;
search = function (source: string, sub: number): boolean {
  //expression
  return false;
  //函数定义返回值类型 必须在函数内 return
}
search('xxx',2)

//函数名不必与接口定义的名字相同 只匹配顺序和类型
search = function (src: string, sub: number): boolean {
  //expression
  return false;
}

let search1 :SearchFunc
//如果不想指定类型 ts会根据接口推断类型
search1 = function (source, sub): boolean {
  //expression
  return false;
  //函数定义返回值类型 必须在函数内 return
}
search1('xxx', 'xxx') //error
```

可索引的类型 → 索引签名(描述对象索引类型,索引对象的返回值)

ts索引支持数字和字符串,但是数字索引的返回值必须是字符串索引返回值类型的子类型

# 二.类类型

## 2.1实现接口 

与C#或Java里接口的基本作用一样，TypeScript也能够用它来明确的强制一个类去符合某种契约。

```typescript
interface ClockInterface {
  time: Date;
}
class clock implements ClockInterface {
  time: Date
  constructor() {

  }
  func() {}
}
```

你也可以在接口中描述一个方法，在类里实现它，如同下面的`setTime`方法一样：

```typescript
interface ClockInterface {
    currentTime: Date;
    setTime(d: Date);
}

class Clock implements ClockInterface {
    currentTime: Date;
    setTime(d: Date) {
        this.currentTime = d;
    }
    constructor(h: number, m: number) { }
}
```

接口描述了类的公共部分，而不是公共和私有两部分。 它不会帮你检查类是否具有某些私有成员。

## 2.2类的静态部分和实例部分

当你操作类和接口的时候，你要知道类是具有两个类型的：静态部分的类型和实例的类型。 你会注意到，当你用构造器签名去定义一个接口并试图定义一个类去实现这个接口时会得到一个错误：

```typescript
interface clockInterface {
  new (hour: number, minute: number)
}

class clock implements clockInterface {
  time: Date;
  constructor(h: number, m: number);//报错 
}
```





## 2.3继承接口

和类一样，接口也可以相互继承。 这让我们能够从一个接口里复制成员到另一个接口里，可以更灵活地将接口分割到可重用的模块里。

```typescript
interface Shape {
  color: string;
}

interface Square extends Shape {
  sildLength: number;
}
let square = <Square>{};
square.color= 'green';
```

一个接口可以继承多个接口，创建出多个接口的合成接口。

```typescript
interface Shape {
  color: string;
}
interface PenStroke {
  width: number;
}

interface Square extends Shape, PenStroke {
  sildLength: number;
}
let square = <Square>{};
square.color = 'green';
square.width = 1;
square.sildLength = 1;

```

混合类型

为什么有混合类型

语法怎么写 个对象可以同时做为函数和对象使用，并带有额外的属性

```

```



## 2.3接口继承类

当接口继承了一个类类型时，它会继承类的成员但不包括其实现。 就好像接口声明了所有类中存在的成员，但并没有提供具体实现一样。 接口同样会继承到类的private和protected成员。 这意味着当你创建了一个接口继承了一个拥有私有或受保护的成员的类时，这个接口类型只能被这个类或其子类所实现（implement）。

```typescript
class Control {
  private state: any;
}
interface SelectableControl extends Control {
  select() :void;
}

class Button extends Control implements SelectableControl {
  select() {}
}

class TextBox extends Control {
  select(){}
}

class Image implements SelectableControl {
  select() {}//缺少state
}

```



