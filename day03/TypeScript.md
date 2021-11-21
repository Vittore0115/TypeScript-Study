# TypeScript Day 03

> 映射类型

映射类型建立在索引签名的语法之上，通常使用 keyof 创建迭代键

例如 ReadOnly<T> 和 Pick<T>

``` TypeScript

 	type ReadOnly<T> = {
 	 	readonly [K in keyof T]: T<K>
	}

	type Pick<T, K extends keyof T> = {
		[P in K]: T[K]
	}

```

> 映射修饰符

在映射类型中 可以使用 readonly 和 ? 修饰符，可以使用 + 来添加修饰符，或者 - 来去除修饰符， 如果没有 +/-，则默认为 +

语法大致如下

``` TypeScript
	type Show = {
		readonly readOnlyProperty: number
		optionalProperty?: number
	}

	type MyRequired<T> = {
		[P in keyof T]-?: T[P]
	}
```

> 类型重映射

类似于 Array.prototype.map()

下面是筛选 T 中 R 类型的键的工具类型

``` TypeScript

	type Person = {
		age: number
		name: string
		alive: boolean
	}

	type FilterByType<T, R> = {
		[K in keyof T as T[K] extends R ? K : never]: T[K]
	}

	// { age: number }
	type filterPerson = FilterByType<Person, number>

```

官方示例，用于创建新的属性名

``` TypeScript

	type Getters<Type> = {
		// Capitalize 为 首字母大写 的工具类型
		[P in keyof Type as `get${Capitalize<string & P>}`]: () => Type[P]
	}

	interface Person {
		name: string
		age: number
		location: string
	}

	// type LazyPerson = {
	// 	getName: () => string;
	// 	getAge: () => number;
	// 	getLocation: () => string;
	// }
	type LazyPerson = Getters<Person>
```

