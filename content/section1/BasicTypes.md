## 类型断言(强制类型装换)

当知道数据类型的时候,对数据进行强制类型装换

断言的两种写法 (有的情况他们想等哦)

1. 一种是"尖括号"  → (<type>variable)

   ```typescript
   let someValue :any = 'i am ts';
   let strLength: number = (<stirng>someValue).length;
   ```

2. as语法 → (variable as type)

   ```typescript
   let someValueL :any = 'i am as';
   let strLenth: number = (someValue as string).length;
   ```
