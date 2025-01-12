> ##### Index

- [What is Typescript :](#what-is-typescript-)
- [How to install TypeScript :](#how-to-install-typescript-)
- [Typescript Syntax :](#typescript-syntax-)

---

#### What is Typescript :

`Typescript` :  is a strongly typed programming language that builds on JavaScript, giving you better tooling at any scale.

Typescript files markable with extension `.ts`.

#### How to install TypeScript :

You can install `Typescript` on your operating system level using the following command.

```shell
npm install -g typescript 
```

> *__Note:__* it is required to install `Node.js` on your system environment variables to use it's package manager which is `npm` to install typescript.

You can check if the typescript installed successfully using the following command.

```shell
tsc --version
```

When you need to work with `typescript` on the browser you need to convert .`ts` file to a `.js` file and you can do that using the following command.

```shell
tsc --init
```

Then you will see `tsconfig.ts` file in the working directory. open it and use the shortcut
<kbd>Crtl</kbd>+ <kbd>f</kbd> in your editor `(VSCODE)` in my case or run the find functionality of your editor then set the variable `outDir` to the path of the `.js` files `./dist` in my case and then create that directory in `outDir` path. Next step is to set the default typescript `./src` directory to the variable `rootDir`. Now your folder structure should look like this.

```shell
-dist/
-src/
	-index.ts
-tsconfig.ts
```

now you can convert your `.ts` file using the following command.

```shell
//for the file
tsc index.ts

//for the ./dist directory
tsc
```

You should see the `index.js` file inside the `./dist` directory as follows.

```shell
-dist/
	-index.js
-src/
	-index.ts
-tsconfig.ts
```

You can make the `tsc` converter to observe every change you do on the `.ts` files using the following command.

```shell
tsc --watch
```

Another problem will face you while trying to use the runner of the editor, is that 
`typescript` needs an `npm` package called `ts-node` that will combine the command `tsc` and `node` together to be compatible with `.ts` while execution using `Node.js` as a runtime environment. You can install `ts-node` on the operating system using the following command.

```shell
npm install -g ts-node
```

Now, you shouldn't face any problems while running `.ts` files on your editor.

#### Typescript Syntax :

Typescript is a strongly typed language, Means that every unit of data in your source code should have a container type.

```typescript
// number type
let x:number = 10;

// string type
let firstName:string = 'Mustafa';

// boolean type
let isEven:boolean = true;

// array of number type
let array:number[] = [1, 2, 3];

// list of multiple types
let list:(number|string|boolean)[] = [firstName, isEven, x];

// varaible of multiple types
let dynamic:(number|string|boolean) = 'Ahmed';
dynamic = 10;
dynamic = false;

// variable of any type
let joker:any = 'Mustafa'
joker = new Error('This is an object!');
```

Also, functions in typescript has return types and parameter types as following.

```typescript
// default function
function getYourName(name:string): string {
  return name;
}

// variable function
const getYourName = (name:string) => {
  return name;
}

// anonymous function
(name:string = firstName) => {return name};

// variable function with function type
const printMyName:(yourName:string) => void = (yourName) => {
  console.log(yourName);
}
```

> *__Note:__* typescript use type inference to detect the return value of the variable function and anonymous function.

Typescript introduces new data-structure called `tuple`, it's like a record that holds finite number of values with specified types for each value. see the following syntax.

```typescript
// tuple data structure 
let tuple1:[string, number] = ['Mustafa', 20];

// tuple with multiple types per index
let tuple2:[string|boolean, number] = ['Ahmed', 54];
tuple2 = [true, 1];
```

> *__Note:__* the arrangement of tuple values is the most important rule to follow the syntax, that each value must match the corresponding index type. In the previous example `tuple[0]` must be a `string` value and `tuple[1]` must be a `number` value.

Typescript uses the union operator `|` between types to get either of them as a valid type for the variable that uses this definition `type 1|type 2|.....|type N`.

Typescript provides 3 ways to define new types and these ways are `classes`, `interfaces`, and `enums`. we start by `interfaces`. An `interface` in typescript is defined using the following syntax.

```typescript
// interface example
interface Token {
  type:string;
  value:any;
  
  getTokenType():string;
  getValueType():any;
} 

// token object implements the Token interface
const token:Token = {
  type: 'number',
  value: 10,
  
  getTokenType():string {
      return this.type;
  },
  getValueType():any {
      return this.value;
  },
}
```

Sometimes we need to define type `alias` for a combined collection of types like 
`string|number`, `[number|boolean, string[]]`, .....
Typescript provides you the `type` reserved keyword that defines your customized types in the program as the following syntax.

```typescript
// define a new type called [mytype]
type mytype = string|number;

let x:mytype = 10;
x = 'Mustafa';

x = true; //Compile Error!!

// define combined types as a global type called [dynamicArray]
type dynamicArray = [number|boolean, string[]];

let array:dynamicArray = [true, []];
array = [10, ['mustafa']];
```

We can define optional variables or fields in typescript using `?` operator as following syntax.

```typescript
// try to convert to optional types
type dynamicArray = [number|boolean, string[]?];

// valid syntax because string[] is an optional field 
let array:dynamicArray = [true];
```

> *__Note:__* the optional operator `?` means that the type is the default type you assigned or undefined, which is mean that `?` operator is equivalent to `(type|undefined)?`. 
> (ex: `string[]?` <=> `(string[]|undefined)?`).

You may be sure about some optional value at the runtime will have a value and no longer be `undefined`. You can use the `!` operator to tell the compiler of typescript that it doesn't need to check on this variable using the following syntax.

```typescript
// optional parameter not optional type
type Person = {
  name:string,
  age?:number
}

let boy:Person = {
  name: 'mustafa',
}

let age:number = boy.age!

console.log(age);
```

> *__Note:__*  the optional parameter means that it can have a value but it's can't be removed, which means that the parameter `age?:number` is equivalent to `age:(number|undefined)`.

We can solve the problem of the `undefined` value of the previous example using `??` operator as following syntax.

```typescript
// check if it's undefined or not
let age:number = boy.age ?? 10;
```

Typescript also provides another way to define constants of fixed types like `enum` as the following syntax.

```typescript
// create a new type of constants called MyEnum
enum MyEnum {
  value1 = "1",
  value2 = "2",
  value3 = "3",
  value4 = "4",
  value5 = "5"
}

console.log(MyEnum.value1);
```

Generally, `enum` is used for type safe usage and limiting the values of some state in your application to make it easier to use without any syntax or logical error.

Like wise all programming languages have classes and typescript doesn't implement `constructor overloading` concept, but we can do it using `Static Factory Method` design pattern as the following syntax.

```typescript
// create a person class with constructor overloading implementation
class Person {

  static objects:number = 0;

  name:string;
  ssn:string;
  age:number = 1;

  private constructor(name?:string, ssn?:string, age?:number) {
    this.name = name?? "person name";
    this.ssn = ssn?? "1234567891011";
    this.age = age?? this.age;
    Person.objects++;
  }

  static personWithName(name:string) : Person {
    return new Person(name);
  }

  static personWithNameAndSSN(name:string, ssn:string) : Person {
    return new Person(name, ssn);
  }

  static personWithNameAndSSNAndAge(name:string, ssn:string, age:number) : Person {
    return new Person(name, ssn, age);
  }

  sayHello(): void {
    console.log("hello!");
  }

}

let mustafa:Person = Person.personWithNameAndSSN("Mustafa Ahmed","30403312100411");

mustafa.sayHello();

console.log(mustafa);
```

We often deal with complex projects that consists of many separate files and modules that need to be imported into another files to be used for some purposes. Typescript makes any thing available to e used out of its source file using the `export` reserved word as following syntax.

```typescript 
// export.ts
// exporting a funtion to import.ts file 

// first way is to use export default
const sayHello: () => void = () => {
	console.log("Hello!");
};

export default sayHello;
// ----------------------------------------------- //
//second way it to use export
export const sayHello:() => void = () => {
	console.log("Hello!");
};
```

```typescript 
// import.ts
// importing a funtion from export.ts file

import sayHello from "./export.ts";
//or
import {sayHello} from "./export.ts";

sayHello();
```

> **Note:** when we use `export` only that means the global export object has a new property so we use destruction operator `{}` with the `import` statement to get the property we add and we can't use anything else `ex: import {sayHello} from "./export.ts";`, but when we use `export default` that means the file has only one thing to share with neighbor files and that doesn't need to use the destruction operator `{}` `ex: import sayHello from "./export.ts";`.

As all programming languages, typescript provides `Generics` allows for multiple types for a single item  `<T>` in the programming language as following syntax.

```typescript
// create generic class Data

class Data<V> {
  private value: V;

  constructor(value:V) {
    this.value = value;
  }
  
  printValue<V>() {
    console.log(this.value);
  }
}

const myName:Data<string> = new Data("Mustafa Ahmed");

myName.printValue();
```

In typescript you can even define an `Anonymous Object` type for your variable as the following syntax.

```typescript
// create anonymous type 
const mustafa:{name:string, age:number} = {
	name: "mustafa ahmed",
	age: 21
};

console.log(mustafa)
```

In JavaScript we can add properties in the anonymous object types, but typescript doesn't allow that syntax (ex: `mustafa.ssn` that will give you a syntax error since it doesn't match the anonymous object type `{name:string, age:number}`.

Typescript solves this problem using `Global Object` type, by defining array of many keys with any values as the following syntax.

```typescript
// create anonymous global object type 
const mustafa:{[key:string]:any} = {
	name: "mustafa ahmed",
	age: 21
};

mustafa.ssn = "1234567891011";

console.log(mustafa.ssn)
```

In the preceding code any property inside the object called `mustafa` will be of type `mustafa[string]:any` since we made global for any key in that object.

> **Note:** if we commented the line of the `ssn` assignment value then the code will print `undefined`. it means that the key `ssn` exist and defined in `mustafa` object but has a value `undefined` which is included in the `any` type.

Typescript also provides something called utilities which make types more flexible.

- `Omit<T, 'field1'|...|'fieldN'>` : is a utility makes you exclude some property fields in any object type that extends it.
- `Pick<T, 'field1'|...|'fieldN'>` : is a utility makes you include some property fields in any object type that extends it.
- `Required<T>` : is a utility that includes all property fields as required of some type even if it has some of them as optional fields.
- `Partial<T>` : is a utility that includes all property fields as optional of some type even if it has some of them as required fields.

See the following syntax.

```typescript
// using Typescript utilities

type person = {
  name: string;
  age: number;
  ssn: string;
}

type employee = {
  salary: number;
  empId: number;
}

// PersonWithoutSSN{name:string}
interface PersonWithoutSSNAndAge extends Omit<person, 'ssn' | 'age'> {}

// EmployeeWithSalaryOnly{salary:number, name:string, age:number, ssn:string}
interface EmployeeWithSalaryOnly extends Pick<employee, 'salary'>, Required<person> {}

//EmployeePerson{all properties in the two types}
type EmployeePerson = person & employee;

//OptionalEmployeeRequiredPerson{name:string, age:number, ssn:string, salary?:number, empId?:number}
type OptionalEmployeeRequiredPerson = Required<person> & Partial<employee>;
```

> **Note:** the preceding utilities are references to types or similar to an interface so if we need to use them with classes we will use the the `implements` reserved word.

```typescript
// using typescript utilties with classes.

type person = {
	name:string;
	age:number;
	ssn:string;
}

class MyPerson implements Omit<person, 'ssn'> {
  age: number;
  name: string;
  
  constructor(){
    this.name = "person name",
    this.age = 21
  }
}
```

---

