![](./img/2011101914103257.jpg)
https://yangjh.oschina.io/gitbook/faq/Contents.html
**es5实现类**

```
//使用自调用函数 让变量私有化 伪造一个class(封闭空间)
var Greeter = /**@class */(function() {
  //使用组合构造函数模式和原型模式创建对象
  //构造函数
  function Greeter(message) {
    this.greeting = message;
  }
  //原型
  Greeter.prototype.greet = function () {
    return 'hello' + this.greeting;
  }
  return Greeter;
})();
var greeter = new Greeter('world')
// var button = document.getElementById('#button')
// button.onclick = function () {
//   alert(greeter.greet())
// }
// 类
//1.匿名函数
//2.构造函数
//3.构造函数原型链挂方法
//3.return 构造函数
//4.实例化一个对象

```

```
class Greeter1 {
  greeting: string;
  //constructor 为默认方法 通过new一个实例 自动调用该方法 
  // 一个类必须有constuctor 如果没有显示定时 那个一个空的construct会被添加
  constructor (message:string) {
    this.greeting = message;
  }
  greeter () {
    return `hello,${this.greeting}`
  }
 }
 let greeter1 = new Greeter('world')
```
//  1.class xxx{}
//  2.constcutor默认方法 写对象的属性 
//  3.getter为类的方法
//  4.new一个对象
// 1.extend继承
```
class Animal {
  public dogName: string;
  public constructor (name) {
    this.dogName = name 
  }
  public move (distacneInMeters:number = 50 ) {
      console.log(`Animal moved ${distacneInMeters}`)
  }
}

class Dog extends Animal {
  color: string
  constructor (x ,color) {
    super(x);
    this.color = color
  }
  public bark () {
    console.log('bark')
  }
}
const dog = new Dog('xxx',1);
dog.bark();
dog.move(10);
```
// extends 子类继承父类
// 公共 public
// 私有 private 
// 派生 protected protected成员在派生类中仍然可以访问。
//  派生类 利用继承机制，新的类可以从已有的类中派生。那些用于派生的类称为这些特别派生出的类的“基类”
// readonly 只读
```
class Octopus {
  readonly numberOfLegs: number = 8;
  constructor(readonly name: string) {
  }
}
```
// 存取器
// TypeScript支持通过getters/setters来截取对对象成员的访问。
```

let passcode = 'secret'
class Employee {
  private _fullName: string;
  get fullName(): string {
    //return 字符串
    return this._fullName;
  }
  set fullName(newName: string) {
    if (passcode && passcode == 'secret passcode') {
      this._fullName = newName;
    } else {
      console.log('error')
    }
  }
}
let employe = new Employee();
```
//实例属性/成员 用new标志服去实例化
//静态属性 类成员 static修饰的变量或方法
实例成员属于实例化对象到，只有(实例化)创建对象才能访问
类成员是属于类的  通过类名直接访问 但是类成员也能通过对象引用
// https://zhidao.baidu.com/question/39372375.html
// 静态成员再分配时只有一份地址空间，只用分一次就行，
// 以后都用这份空间。而实例成员再分配时是每次产生一个成员都要在再配一次空间。
```
class Grid {
  static origin  = { x:0, y:0 };
  //point
  calculateDistanceFromOrigin (point:{x: number, y: number}) {
    let xDist = (point.x - Grid.origin.x);
    let yDist = (point.y - Grid.origin.y);
    return Math.sqrt(xDist * xDist + yDist * yDist) / this.scale;
  }
  constructor (public scale: number) {}
}
let grid1 = new Grid(1.0)
let grid2 = new Grid(5.0)
console.log(grid1.calculateDistanceFromOrigin({x: 10, y: 10}));
console.log(grid2.calculateDistanceFromOrigin({x:10,y:20}));
```
// 6.抽象类
// 抽象类作为其他派生类的基类使用 他们一般不实例化 而且不同于接口 抽象类可以包含成员的细节,
// abstrac关键之用于定义抽象类内部定义抽象方法
// 抽象类中的抽象方法不包含具体实现并且在派生类中实现 抽象方法的语法和接口方法类似 都是定义方法签名但是不含具体方法,
// 区别 抽象类用anstract修饰符
// 方法签名由方法名加一个参数列表(方法的参数和顺序)
//类名也要加abstract修饰符
```
abstract class Department {
  constructor (public name: string) {
  }
  printName():void {
    console.log('xxxx' + this.name)
  }
abstract printMeeting (): void; //必须在派生类中实现
}
 class xxx extends Department {
  constructor (){
    super('xxxx')
  }
  printMeeting():void {
    console.log(1)
  }
  getxxx ():void {
    console.log(2)
  }
 }
 let department :Department //创建对抽象类型的应用
 //不能对抽象类的实例,但是能对抽象子类进行实例化和赋值
//  department = new Department() //不能创建抽象类的实例
department = new xxx()
department.getxxx() //方法在声明的抽象类不存在 抽象
department.printName();
department.printMeeting();
```
//7.高级技巧构造函数
// 类的定义会创建两个东西,类的实例类型和一个构造函数
//this在函数中使用
```
class Greeter3 {
  static standardGreeting = 'hello,'
  greeting: string;
  greet() {
    if(this.greeting) {
      return `xxx${this.greeting}`
    } else {
      return Greeter3.standarGreeting
    }
  }
}
let greeter3: Greeter3; //greeter3类的实例类型是Greeter
greeter3 = new Greeter3()

let greterMarke : typeof Greeter3 = Greeter3;
greterMarke.standardGreeting = "Hey there!";
let greeter4: Greeter3 = new greterMarke();
console.log(greeter4.greet())

```
//8.把类当接口用
// 因为类可以创建类型,所以你能够允许在接口的地方使用类
```
class point {
  x: number;
  y: number;
}
interface point3d extends point {
  z: number;
}
let point3d: point3d = { x: 1, y: 2, z: 3 }
```