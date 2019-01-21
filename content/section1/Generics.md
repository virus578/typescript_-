泛型

1. 组件不仅能够支持当前的数据类型，同时也能支持未来的数据类型，这在创建大型系统时为你提供了十分灵活的功能。

2. 在像C#和Java这样的语言中，可以使用`泛型`来创建可重用的组件，一个组件可以支持多种类型的数据。 这样用户就可以以自己的数据类型来使用组件。

   创建第一个使用泛型的例子：identity函数。 这个函数会返回任何传入它的值。 你可以把这个函数当成是 `echo`命令。

   ```typescript
   function identity(arg: number): number {
       return arg
   }
   ```

   ```typescript
   function identity (params: any): any {
       return arg
   }
   ```

   我能期望传入的数据和返回的数据类型应该相同

   ```typescript
   function indentity<T> (arg: T): T { //泛型函数
     return arg;
   }
   ```

   我们给identity添加了类型变量`T`。 `T`帮助我们捕获用户传入的类型（比如：`number`），之后我们就可以使用这个类型。 之后我们再次使用了 `T`当做返回值类型。现在我们可以知道参数类型与返回值类型是相同的了。 这允许我们跟踪函数里使用的类型的信息。

   我们把这个版本的`identity`函数叫做泛型，因为它可以适用于多个类型。 不同于使用 `any`，它不会丢失信息，像第一个例子那像保持准确性，传入数值类型并返回数值类型。

   泛型函数的两种用法

   1. 传入所有的参数，包含类型参数

      ```typescript
      let output = indentity<string>('mystr');
      ```

   2. 类型推断 编译器会根据传入的参数自动地帮助我们确定T的类型

      ```typescript
      let input = indentity('mystr')
      ```

      注意我们没必要使用尖括号（`<>`）来明确地传入类型；编译器可以查看`myString`的值，然后把`T`设置为它的类型。 类型推论帮助我们保持代码精简和高可读性。如果编译器不能够自动地推断出类型的话，只能像上面那样明确的传入T的类型，在一些复杂的情况下，这是可能出现的。

      泛型变量

      ```typescript
      function log<T>(arg: T): T{
          console.log(arg.length) //数字没有.length属性
          return arg;
      }
      ```

      ```
      
      ```

      泛型类型

      泛型约束

      泛型类


