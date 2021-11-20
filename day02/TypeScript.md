# TypeScript Day 02

> 索引类型

``` TypeScript
 	type Person = { age: number; name: string; alive: boolean };

	// 获取 Person 中属性 age 的类型
	type Age = Person["age"];  // Age = number 

	// keyof 获取 Person 中的所有属性key
	type T2 = Person[keyof Person]; // T2 = string | number | boolean

	// 获取属性 "alive" | "name" 的 类型
	type AliveOrName = "alive" | "name";  //AliveOrName = "alive" | "name"
	
	type I3 = Person[AliveOrName]; // I3 = string | boolean

```

> 条件判断

``` TypeScript
	interface Animal {
		live(): void;
	}

	interface cat extends Animal {
		woof(): void;
	}

	// 条件语句， 如果 cat 继承 Animal的话，是number类型， 否则是 string
	type Example1 = cat extends Animal ? number : string; //Example1  = number

	interface IdLabel {
		id: number /* some fields */;
	}
	interface NameLabel {
		name: string /* other fields */;
	}
```

> 条件类型约束

``` TypeScript
	type MessageOf<T> = T["message"]; // 报错，message可能不存在在类型 T 中
	
	//这里可以对其进行约束,使用unknown 代表不知道是什么类型，等待推断

	type MessageOf1<T extends { message: unknown }> = T["message"];

	interface Email {
		message: string;
	}

	// 这里message 的类型就是string
	type EmailMessageContents = MessageOf<Email>;

```



> 模板文字类型

``` TypeScript
 	type PropEventSource<Type> = {
		on(
			eventName: `${string & keyof Type}Changed`,
			callback: (newValue: any) => void
		): void;
	};

	declare function makeWatchedObject<Type>(
		obj: Type
	): Type & PropEventSource<Type>;

	const person = makeWatchedObject({
		firstName: "Vittore",
		lastName: "yc",
		sex: 'boy',
	});

	person.on("firstNameChanged", (newValue) => {
		console.log(`firstName was changed to ${newValue}!`);
	});

	person.on("lastNameChanged", () => {})

	person.on("sexChange", () => {}) // 报错， 因为上面约束了 on 事件的名称 
```

