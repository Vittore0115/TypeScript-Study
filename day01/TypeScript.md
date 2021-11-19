# TypeScript Day 01

``` bash
TypeScript编译器
npm i -y
```

``` bash
安装TypeScript
npm i -g typescript
```


- 泛型

用户不需要指定特定的类型，可以通过编程的方式，让程序自己能推导出应该是什么类型 的一种不确定的类型。

``` TypeScript
 //我们使用一个泛型Type
 function identity<Type>(arg: Type): Type {
   return arg;
 }
 // 当我们调用的时候传入Type的类型是number时，程序会规定arg以及函数返回的类型为number
 let res = identity<number>(1);
 //若不显式地指定类型，编译器也会进行推断
 let res = identity(1);
 // 我们可以把Type作为数组元素的类型，返回一个该类型的数组，而不是该类型。
 function loggingIdentity<Type>(arg: Array<Type>): Array<Type> {
   console.log(arg.length); // Array有.length,故不会报错
   return arg;
 }
```

- 通用类型

  定义通用接口,形成通用类型

``` TypeScript
 interface GenericIdentityFn {
   <Type>(arg: Type): Type;
 }
 //使Type可以看成是整个接口的参数
 //使得类型参数对接口的所有其他成员可见
 interface GenericIdentityFn<Type> {
   (arg: Type): Type;
 }
 function identity<Type>(arg: Type): Type {
   return arg;
 }
 let myIdentity: GenericIdentityFn = identity;

```

- 通用类

  泛型类和泛型接口很相似，泛型类<>在类名后面的 ( ) 中，包含了泛型类型的参数列表

``` TypeScript
 class GenericNumber<NumType> {
   zeroValue: NumType;
   add: (x: NumType, y: NumType) => NumType;
 }
 // NumType传number或string或者任意类型，就像接口一样，将类型参数放在类本身上可以确保类的所有属性都使用相同的类型。
```

- 通用约束

  当我们希望对用户传进来的Type有所约束时，我们可以通过extends来进行约束

``` TypeScript
 interface Lengthwise {
   length: number;
 }
 function loggingIdentity<Type extends Lengthwise>(arg: Type): Type {
   console.log(arg.length); 
   return arg;
 }
 //类型“number”不满足约束“Lengthwise”。
 loggingIdentity<number>(1);
 //ok
 loggingIdentity({ length: 10, value: 1 });
```


- Keyof 类型运算符
  
	TypeScript 允许我们遍历某种类型的属性，并通过 keyof 操作符提取其属性的名称。

``` TypeScript
 interface Person {
   name: string;
   age: number;
   sex: string;
 }
 type V1 = keyof Person; // "name" | "age" | " sex"
 type V2 = keyof Person[];  // number | "length" | "push" | "concat" | ...
 type V3 = keyof { [x: string]: Person };  // string | number

```




