# TypeScript Day 04

> extends

- extends在ts中除用于conditional type之外，还具有继承

``` TypeScript
// Cat => { name: string; bark(): void }

interface Animal {
   kind: string;
}

interface Cat extends Animal {
 bark(): void;
}
```

> infer用法

- 表示在 extends 条件语句中待推断的类型变量

``` TypeScript
type ParamType<T> = T extends (...args: infer P) => any ? P : T;
```

- 又如以下两种写法意思相同
  
``` TypeScript
//使用索引访问
type Flatten<T> = T extends any[] ? T[number] : T;

//使用infer的写法
type Flatten<Type> = Type extends Array<infer Item> ? Item : Type;
```
