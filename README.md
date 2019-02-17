# 代码整洁的 TypeScript [![Tweet](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/intent/tweet?text=Clean%20Code%20Typescript&url=https://github.com/labs42io/clean-code-typescript)

Clean Code concepts adapted for TypeScript.  
Inspired from [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript).

将代码整洁的理念适配至 TypeScript ， 灵感来自于[代码整洁的 JavaScript ](https://github.com/ryanmcdermott/clean-code-javascript)。

## Table of Contents

  1. [Introduction](#introduction)
  2. [Variables](#variables)
  3. [Functions](#functions)
  4. [Objects and Data Structures](#objects-and-data-structures)
  5. [Classes](#classes)
  6. [SOLID](#solid)
  7. [Testing](#testing)
  8. [Concurrency](#concurrency)
  9. [Error Handling](#error-handling)
  10. [Formatting](#formatting)
  11. [Comments](#comments)
  12. [Translations](#translations)

## 目录

  1. [简介](#简介)
  2. [变量](#变量)
  3. [函数](#函数)
  4. [对象和数据结构](#对象和数据结构)
  5. [类](#类)
  6. [SOLID](#solid)
  7. [测试](#测试)
  8. [并发](#并发)
  9. [错误处理](#错误处理)
  10. [格式化](#格式化)
  11. [注释](#注释)
  12. [翻译](#翻译)

## Introduction

## 简介

![Humorous image of software quality estimation as a count of how many expletives
you shout when reading code](https://www.osnews.com/images/comics/wtfm.jpg)

Software engineering principles, from Robert C. Martin's book
[*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882),
adapted for TypeScript. This is not a style guide. It's a guide to producing
[readable, reusable, and refactorable](https://github.com/ryanmcdermott/3rs-of-software-architecture) software in TypeScript.

Not every principle herein has to be strictly followed, and even fewer will be
universally agreed upon. These are guidelines and nothing more, but they are
ones codified over many years of collective experience by the authors of
*Clean Code*.

Our craft of software engineering is just a bit over 50 years old, and we are
still learning a lot. When software architecture is as old as architecture
itself, maybe then we will have harder rules to follow. For now, let these
guidelines serve as a touchstone by which to assess the quality of the
TypeScript code that you and your team produce.

One more thing: knowing these won't immediately make you a better software
developer, and working with them for many years doesn't mean you won't make
mistakes. Every piece of code starts as a first draft, like wet clay getting
shaped into its final form. Finally, we chisel away the imperfections when
we review it with our peers. Don't beat yourself up for first drafts that need
improvement. Beat up the code instead!

![一张用你阅读代码时吐槽的数量来评估软件质量的搞笑图片](https://www.osnews.com/images/comics/wtfm.jpg)

将源自 Robert C. Martin 的 [*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)
的软件工程原则适配到 TypeScript 。 这不是一个代码风格指南， 它是一个使用 TypeScript 来生产
可读的， 可重用的， 以及可重构的软件的指南。

这里的每一项原则都不是必须遵守的， 甚至只有更少的能够被广泛认可。 这些仅仅是指南而已， 但是却是
*Clean Code* 作者多年经验的结晶。

我们的软件工程行业只有短短的 50 年， 依然有很多要我们去学习。 当软件架构与建筑架构一样古老时，
也许我们将会有硬性的规则去遵守。 而现在， 让这些指南做为你和你的团队生产的 TypeScript 代码的
质量的标准。

还有一件事： 知道这些指南并不能马上让你成为一个更加出色的软件开发者， 并且使用它们工作多年也并
不意味着你不再会犯错误。 每一段代码最开始都是草稿， 像湿粘土一样被打造成最终的形态。 最后当我们
和搭档们一起审查代码时清除那些不完善之处, 不要因为最初需要改善的草稿代码而自责， 而是对那些代
码下手。

**[⬆ 返回目录](#目录)**

## Variables

## 变量

### Use meaningful variable names

### 使用有意义的变量名称

Distinguish names in such a way that the reader knows what the differences offer.

使用可以区分的名称， 让读者知道他们的区别是什么。

**不好的：**

```ts
function between<T>(a1: T, a2: T, a3: T): boolean {
  return a2 <= a1 && a1 <= a3;
}

```

**好的：**

```ts
function between<T>(value: T, left: T, right: T): boolean {
  return left <= value && value <= right;
}
```

**[⬆ 返回目录](#目录)**

### Use pronounceable variable names

### 使用可拼读的变量名称

If you can’t pronounce it, you can’t discuss it without sounding like an idiot.

如果你不能把它读出来， 那你就不能和同事讨论它， 这看起来像块纱布。

**不好的：**

```ts
type DtaRcrd102 = {
  genymdhms: Date;
  modymdhms: Date;
  pszqint: number;
}
```

**好的：**

```ts
type Customer = {
  generationTimestamp: Date;
  modificationTimestamp: Date;
  recordId: number;
}
```

**[⬆ 返回目录](#目录)**

### Use the same vocabulary for the same type of variable

### 为相同类型的变量使用相同的词汇

**不好的：**

```ts
function getUserInfo(): User;
function getUserDetails(): User;
function getUserData(): User;
```

**好的：**

```ts
function getUser(): User;
```

**[⬆ 返回目录](#目录)**

### 使用可搜索的名称

We will read more code than we will ever write. It's important that the code we do write is readable and searchable. By *not* naming variables that end up being meaningful for understanding our program, we hurt our readers. Make your names searchable. Tools like [TSLint](https://palantir.github.io/tslint/rules/no-magic-numbers/) can help identify unnamed constants.


我们要阅读的代码比要写的代码多得多， 所以我们写出的代码的可读性和可搜索性是很重要的。 使用没有
意义的变量名将会导致我们的程序难于理解， 将会伤害我们的读者， 所以请使用可搜索的变量名。 类似 [TSLint](https://palantir.github.io/tslint/rules/no-magic-numbers/)
的工具可以帮助我们找到未命名的常量。

**不好的：**

```ts
// What the heck is 86400000 for?
// 艹， 86400000 是什么鬼？
setTimeout(restart, 86400000);
```

**好的：**

```ts
// Declare them as capitalized named constants.
// 将他们声明为大写的变量
const MILLISECONDS_IN_A_DAY = 24 * 60 * 60 * 1000;

setTimeout(restart, MILLISECONDS_IN_A_DAY);
```

**[⬆ 返回目录](#目录)**

### Use explanatory variables

### 使用解释性的变量

**不好的：**

```ts
declare const users: Map<string, User>;

for (const keyValue of users) {
  // iterate through users map
}
```

**好的：**

```ts
declare const users: Map<string, User>;

for (const [id, user] of users) {
  // iterate through users map
}
```

**[⬆ 返回目录](#目录)**

### Avoid Mental Mapping

### 避免心理映射

Explicit is better than implicit.  
*Clarity is king.*

显示比隐式更好。 *清晰为王!*

**不好的：**

```ts
const u = getUser();
const s = getSubscription();
const t = charge(u, s);
```

**好的：**

```ts
const user = getUser();
const subscription = getSubscription();
const transaction = charge(user, subscription);
```

**[⬆ 返回目录](#目录)**

### Don't add unneeded context

### 不添加不必要的上下文

If your class/type/object name tells you something, don't repeat that in your variable name.

如果你的类/类型/对象名有意义， 不必在变量名上再重复。

**不好的：**

```ts
type Car = {
  carMake: string;
  carModel: string;
  carColor: string;
}

function print(car: Car): void {
  console.log(`${car.carMake} ${car.carModel} (${car.carColor})`);
}
```

**好的：**

```ts
type Car = {
  make: string;
  model: string;
  color: string;
}

function print(car: Car): void {
  console.log(`${car.make} ${car.model} (${car.color})`);
}
```

**[⬆ 返回目录](#目录)**

### Use default arguments instead of short circuiting or conditionals

### 使用默认变量替代短路运算或条件

Default arguments are often cleaner than short circuiting.

默认参数通常比短路运算更清晰。

**不好的：**

```ts
function loadPages(count?: number) {
  const loadCount = count !== undefined ? count : 10;
  // ...
}
```

**好的：**

```ts
function loadPages(count: number = 10) {
  // ...
}
```

**[⬆ 返回目录](#目录)**

## Functions

## 函数

### Function arguments (2 or fewer ideally)

### 函数参数 (两个以下最理想)

Limiting the amount of function parameters is incredibly important because it makes testing your function easier.
Having more than three leads to a combinatorial explosion where you have to test tons of different cases with each separate argument.  

限制函数参数的个数是非常重要的， 因为这样将使你的函数容易进行测试。 一旦超过三个参数将会导致组
合爆炸， 因为你不得不编写大量针对每个参数的测试用例。

One or two arguments is the ideal case, and three should be avoided if possible. Anything more than that should be consolidated.
Usually, if you have more than two arguments then your function is trying to do too much.
In cases where it's not, most of the time a higher-level object will suffice as an argument.  

一个或者两个参数是理想状况， 如果可能的话， 三个参数的情况应该避免， 超过三个应该被重构。 通常，
如果你有一个超过两个函数的参数， 那就意味着你的函数尝试做太多的事情。 如果不是， 多数情况下一个
更高级对象可能会满足需求。

Consider using object literals if you are finding yourself needing a lot of arguments.  

当你发现你自己需要大量的参数时， 考虑使用一个对象。

To make it obvious what properties the function expects, you can use the [destructuring](https://basarat.gitbooks.io/typescript/docs/destructuring.html) syntax.
This has a few advantages:

1. When someone looks at the function signature, it's immediately clear what properties are being used.

2. Destructuring also clones the specified primitive values of the argument object passed into the function. This can help prevent side effects. Note: objects and arrays that are destructured from the argument object are NOT cloned.

3. TypeScript warns you about unused properties, which would be impossible without destructuring.

为了让函数需要的属性更明显， 可以使用[解构](https://basarat.gitbooks.io/typescript/docs/destructuring.html)语法。 它有三个优点：

1. 当有人查看函数签名时， 会立刻清楚用到了哪些属性。

2. 解构还克隆传递给函数的参数对象的指定原始值。 这有助于预防副作用。 注意：不会克隆参数对象中解构的对象和数组。

3. TypeScript 会警告您未使用的属性，如果没有解构，这将是不可能的。

**不好的：**

```ts
function createMenu(title: string, body: string, buttonText: string, cancellable: boolean) {
  // ...
}

createMenu('Foo', 'Bar', 'Baz', true);
```

**好的：**

```ts
function createMenu(options: { title: string, body: string, buttonText: string, cancellable: boolean }) {
  // ...
}

createMenu({
  title: 'Foo',
  body: 'Bar',
  buttonText: 'Baz',
  cancellable: true
});
```

You can further improve readability by using [type aliases](https://www.typescriptlang.org/docs/handbook/advanced-types.html#type-aliases):

你可以通过[类型别名](https://www.typescriptlang.org/docs/handbook/advanced-types.html#type-aliases)来显著提高可读性：

```ts

type MenuOptions = { title: string, body: string, buttonText: string, cancellable: boolean };

function createMenu(options: MenuOptions) {
  // ...
}

createMenu({
  title: 'Foo',
  body: 'Bar',
  buttonText: 'Baz',
  cancellable: true
});
```

**[⬆ 返回目录](#目录)**

### Functions should do one thing

### 函数应当只做一件事情

This is by far the most important rule in software engineering. When functions do more than one thing, they are harder to compose, test, and reason about. When you can isolate a function to just one action, they can be refactored easily and your code will read much cleaner. If you take nothing else away from this guide other than this, you'll be ahead of many developers.


这是软件工程中最重要的一条规则， 当函数需要做更多的事情时， 它们将会更难进行编写、 测试和推理。
当你能将一个函数隔离到只有一个动作， 他们将能够被容易的进行重构并且你的代码将会更容易阅读。 如
果你严格遵守本指南中的这一条， 你将会领先于许多开发者。

**不好的：**

```ts
function emailClients(clients: Client) {
  clients.forEach((client) => {
    const clientRecord = database.lookup(client);
    if (clientRecord.isActive()) {
      email(client);
    }
  });
}
```

**好的：**

```ts
function emailClients(clients: Client) {
  clients.filter(isActiveClient).forEach(email);
}

function isActiveClient(client: Client) {
  const clientRecord = database.lookup(client);
  return clientRecord.isActive();
}
```

**[⬆ 返回目录](#目录)**

### Function names should say what they do

### 函数名称应该说明它要做什么

**不好的：**

```ts
function addToDate(date: Date, month: number): Date {
  // ...
}

const date = new Date();

// It's hard to tell from the function name what is added
// 很难从函数名看出加了什么
addToDate(date, 1);
```

**好的：**

```ts
function addMonthToDate(date: Date, month: number): Date {
  // ...
}

const date = new Date();
addMonthToDate(date, 1);
```

**[⬆ 返回目录](#目录)**

### Functions should only be one level of abstraction

### 函数应该只有一个抽象级别

When you have more than one level of abstraction your function is usually doing too much. Splitting up functions leads to reusability and easier testing.

当在你的函数中有多于一个抽象级别时， 你的函数通常做了太多事情。 拆分函数将会提升重用性和测试性。

**不好的：**

```ts
function parseCode(code: string) {
  const REGEXES = [ /* ... */ ];
  const statements = code.split(' ');
  const tokens = [];

  REGEXES.forEach((regex) => {
    statements.forEach((statement) => {
      // ...
    });
  });

  const ast = [];
  tokens.forEach((token) => {
    // lex...
  });

  ast.forEach((node) => {
    // parse...
  });
}
```

**好的：**

```ts
const REGEXES = [ /* ... */ ];

function parseCode(code: string) {
  const tokens = tokenize(code);
  const syntaxTree = parse(tokens);

  syntaxTree.forEach((node) => {
    // parse...
  });
}

function tokenize(code: string): Token[] {
  const statements = code.split(' ');
  const tokens: Token[] = [];

  REGEXES.forEach((regex) => {
    statements.forEach((statement) => {
      tokens.push( /* ... */ );
    });
  });

  return tokens;
}

function parse(tokens: Token[]): SyntaxTree {
  const syntaxTree: SyntaxTree[] = [];
  tokens.forEach((token) => {
    syntaxTree.push( /* ... */ );
  });

  return syntaxTree;
}
```

**[⬆ 返回目录](#目录)**

### Remove duplicate code

### 移除冗余代码

Do your absolute best to avoid duplicate code.
Duplicate code is bad because it means that there's more than one place to alter something if you need to change some logic.  

竭尽你的全力去避免冗余代码。 冗余代码是不好的， 因为它意味着当你需要修改一些逻辑时会有多个地方
需要修改。

Imagine if you run a restaurant and you keep track of your inventory: all your tomatoes, onions, garlic, spices, etc.
If you have multiple lists that you keep this on, then all have to be updated when you serve a dish with tomatoes in them.
If you only have one list, there's only one place to update!  

想象一下你在经营一家餐馆， 你需要记录所有的库存西红柿， 洋葱， 大蒜， 各种香料等等。 如果你有多
个记录列表， 当你用西红柿做一道菜时你得更新多个列表。 如果你只有一个列表， 就只有一个地方需要更
新！


Oftentimes you have duplicate code because you have two or more slightly different things, that share a lot in common, but their differences force you to have two or more separate functions that do much of the same things. Removing duplicate code means creating an abstraction that can handle this set of different things with just one function/module/class.  

你有冗余代码通常是因为你有两个或多个稍微不同的东西， 它们共享大部分， 但是它们的不同之处迫使你使
用两个或更多独立的函数来处理大部分相同的东西。 移除冗余代码意味着创建一个可以处理这些不同之处的
抽象的函数/模块/类。

Getting the abstraction right is critical, that's why you should follow the [SOLID](#solid) principles. Bad abstractions can be worse than duplicate code, so be careful! Having said this, if you can make a good abstraction, do it! Don't repeat yourself, otherwise you'll find yourself updating multiple places anytime you want to change one thing.

让这个抽象正确是关键的， 这是为什么要你遵循 *Classes* 那一章的 SOLID 的原因。 不好的抽象比冗
余代码更差， 所以要谨慎行事。 既然已经这么说了， 如果你能够做出一个好的抽象， 才去做。 不要重复
你自己， 否则你会发现当你要修改一个东西时时刻需要修改多个地方。

**不好的：**

```ts
function showDeveloperList(developers: Developer[]) {
  developers.forEach((developer) => {
    const expectedSalary = developer.calculateExpectedSalary();
    const experience = developer.getExperience();
    const githubLink = developer.getGithubLink();

    const data = {
      expectedSalary,
      experience,
      githubLink
    };

    render(data);
  });
}

function showManagerList(managers: Manager[]) {
  managers.forEach((manager) => {
    const expectedSalary = manager.calculateExpectedSalary();
    const experience = manager.getExperience();
    const portfolio = manager.getMBAProjects();

    const data = {
      expectedSalary,
      experience,
      portfolio
    };

    render(data);
  });
}
```

**好的：**

```ts
class Developer {
  // ...
  getExtraDetails() {
    return {
      githubLink: this.githubLink,
    }
  }
}

class Manager {
  // ...
  getExtraDetails() {
    return {
      portfolio: this.portfolio,
    }
  }
}

function showEmployeeList(employee: Developer | Manager) {
  employee.forEach((employee) => {
    const expectedSalary = employee.calculateExpectedSalary();
    const experience = employee.getExperience();
    const extra = employee.getExtraDetails();

    const data = {
      expectedSalary,
      experience,
      extra,
    };

    render(data);
  });
}
```

You should be critical about code duplication. Sometimes there is a tradeoff between duplicated code and increased complexity by introducing unnecessary abstraction. When two implementations from two different modules look similar but live in different domains, duplication might be acceptable and preferred over extracting the common code. The extracted common code in this case introduces an indirect dependency between the two modules.

您应该对代码冗余持批判的态度。 有时需要在冗余代码和通过因不必要的抽象而增加的复杂性之间做权衡。 当来自两个不同模块的两个实现看起来相似但存在于不同的域中时，冗余(可能)是可接受的并且优于提取公共代码。 在这种情况下，提取的公共代码引入了两个模块之间的间接依赖关系。

**[⬆ 返回目录](#目录)**

### Set default objects with Object.assign or destructuring

### 使用 Object.assign 设置默认对象或者解构

**不好的：**

```ts
type MenuConfig = { title?: string, body?: string, buttonText?: string, cancellable?: boolean };

function createMenu(config: MenuConfig) {
  config.title = config.title || 'Foo';
  config.body = config.body || 'Bar';
  config.buttonText = config.buttonText || 'Baz';
  config.cancellable = config.cancellable !== undefined ? config.cancellable : true;

  // ...
}

createMenu({ body: 'Bar' });
```

**好的：**

```ts
type MenuConfig = { title?: string, body?: string, buttonText?: string, cancellable?: boolean };

function createMenu(config: MenuConfig) {
  const menuConfig = Object.assign({
    title: 'Foo',
    body: 'Bar',
    buttonText: 'Baz',
    cancellable: true
  }, config);

  // ...
}

createMenu({ body: 'Bar' });
```

Alternatively, you can use destructuring with default values:

另外， 也可以使用解构来处理默认值：

```ts
type MenuConfig = { title?: string, body?: string, buttonText?: string, cancellable?: boolean };

function createMenu({ title = 'Foo', body = 'Bar', buttonText = 'Baz', cancellable = true }: MenuConfig) {
  // ...
}

createMenu({ body: 'Bar' });
```

To avoid any side effects and unexpected behavior by passing in explicitly the `undefined` or `null` value, you can tell the TypeScript compiler to not allow it.
See [`--strictNullChecks`](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html#--strictnullchecks) option in TypeScript.

要避免显示传递 `undefined` 或者 `null` 值产生的负面影响或异常行为， 可以设置 TypeScript 编译器来禁止。 请查看 TypeScript 的 [`--strictNullChecks`](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html#--strictnullchecks) 选项。

**[⬆ 返回目录](#目录)**

### Don't use flags as function parameters

### 不要使用标记位做为函数参数

Flags tell your user that this function does more than one thing.
Functions should do one thing. Split out your functions if they are following different code paths based on a boolean.

标记位是告诉你的用户这个函数做了不只一件事情。 函数应该只做一件事情。 如果你的函数因为一个布尔值
出现不同的代码路径， 请拆分它们。

**不好的：**

```ts
function createFile(name: string, temp: boolean) {
  if (temp) {
    fs.create(`./temp/${name}`);
  } else {
    fs.create(name);
  }
}
```

**好的：**

```ts
function createTempFile(name: string) {
  createFile(`./temp/${name}`);
}

function createFile(name: string) {
  fs.create(name);
}
```

**[⬆ 返回目录](#目录)**

### Avoid Side Effects (part 1)

### 避免副作用（第 1 部分）

A function produces a side effect if it does anything other than take a value in and return another value or values.
A side effect could be writing to a file, modifying some global variable, or accidentally wiring all your money to a stranger.  

如果一个函数做了除接受一个值然后返回一个值或多个值之外的任何事情， 它将会产生副作用， 它可能是
写入一个文件， 修改一个全局变量， 或者意外的把你所有的钱连接到一个陌生人那里。

Now, you do need to have side effects in a program on occasion. Like the previous example, you might need to write to a file.
What you want to do is to centralize where you are doing this. Don't have several functions and classes that write to a particular file.
Have one service that does it. One and only one.  

现在在你的程序中确实偶尔需要副作用， 就像上面的代码， 你也许需要写入到一个文件， 你需要做的是集
中化你要做的事情， 不要让多个函数或者类写入一个特定的文件， 用一个服务来实现它， 一个并且只有一
个。

The main point is to avoid common pitfalls like sharing state between objects without any structure, using mutable data types that can be written to by anything, and not centralizing where your side effects occur. If you can do this, you will be happier than the vast majority of other programmers.

重点是避免这些常见的易犯的错误， 比如在对象之间共享状态而不使用任何结构， 使用任何地方都可以写入
的可变的数据类型， 没有集中化导致副作用。 如果你能做到这些， 那么你将会比其它的码农大军更加幸福。

**不好的：**

```ts
// Global variable referenced by following function.
// 全局变量被下面的函数引用
let name = 'Robert C. Martin';

function toBase64() {
  name = btoa(name);
}

toBase64();
// If we had another function that used this name, now it'd be a Base64 value
// 如果我们有另一个函数使用这个 name ， 现在它应该是一个 Base64 字符串值。

// expected to print 'Robert C. Martin' but instead 'Um9iZXJ0IEMuIE1hcnRpbg=='
// 期望打印出 'Robert C. Martin' 但是却是 'Um9iZXJ0IEMuIE1hcnRpbg=='
console.log(name);
```

**好的：**

```ts
const name = 'Robert C. Martin';

function toBase64(text: string): string {
  return btoa(text);
}

const encodedName = toBase64(name);
console.log(name);
```

**[⬆ 返回目录](#目录)**

### Avoid Side Effects (part 2)

### 避免副作用 （第 2 部分）

In JavaScript, primitives are passed by value and objects/arrays are passed by reference. In the case of objects and arrays, if your function makes a change in a shopping cart array, for example, by adding an item to purchase, then any other function that uses that `cart` array will be affected by this addition. That may be great, however it can be bad too. Let's imagine a bad situation:  

在 JavaScript 中， 基本类型通过值进行传递而对象/类通过引用传递。 以对象和数组为例， 如果你的函数对一个购物车数组做出了更改， 比如添加了一个要购买的东西， 那么其它使用这个购物车数组的任何函数都会受到影响。 这样貌似挺不错的， 不过也可能很糟糕。 让我们来想象一个糟糕的情况：

The user clicks the "Purchase", button which calls a `purchase` function that spawns a network request and sends the `cart` array to the server. Because of a bad network connection, the purchase function has to keep retrying the request. Now, what if in the meantime the user accidentally clicks "Add to Cart" button on an item they don't actually want before the network request begins? If that happens and the network request begins, then that purchase function will send the accidentally added item because it has a reference to a shopping cart array that the `addItemToCart` function modified by adding an unwanted item.  

用户点击“购买”按钮， 调用一个 `purchase` 函数， 发出一个网络请求， 经购物车数组发送到服务器。 由于网络情况比较差， `purchase` 函数只能尝试重新发送请求。 现在， 用户在网络请求开始之前， 突然点击了“添加到购物车”按钮， 添加了一项并不是真心想买的东西， 那么 `purchase` 函数将会发送这个突然被添加的项目， 因为它们引用了同一个购物车数组对象， 而这个对象 `addItemToCart` 函数修改了， 添加了一个不想要的项目。

A great solution would be for the `addItemToCart` to always clone the `cart`, edit it, and return the clone. This ensures that no other functions that are holding onto a reference of the shopping cart will be affected by any changes.  

一个好的方案应该是让 `addItemToCart` 始终克隆一个购物车副本， 编辑并返回副本。 这样能够保证它不会被其它任何函数引用， 也就不能进行修改。

Two caveats to mention to this approach:

这种方案下需要注意一下 2 个问题：

1. There might be cases where you actually want to modify the input object, but when you adopt this programming practice you will find that those cases are pretty rare. Most things can be refactored to have no side effects! (see [pure function](https://en.wikipedia.org/wiki/Pure_function))

2. Cloning big objects can be very expensive in terms of performance. Luckily, this isn't a big issue in practice because there are great libraries that allow this kind of programming approach to be fast and not as memory intensive as it would be for you to manually clone objects and arrays.

1. 可能在有些情况下确实需要修改输入对象， 但是当你采用这种编程实践之后， 你会发现这种情况是寥寥无几的。 很多东西可以被重构来消除负面影响。 （参考[纯函数](https://zh.wikipedia.org/wiki/%E7%BA%AF%E5%87%BD%E6%95%B0)/[Pure function](https://en.wikipedia.org/wiki/Pure_function)）

2. 克隆大对象可能比较消耗性能。 幸运的是， 在实际操作上， 并不是一个多大的问题， 因为有优秀的类库可以让这一操作变得非常快， 同时也比手工克隆这些对象和数组节省很多内存。

**不好的：**

```ts
function addItemToCart(cart: CartItem[], item: Item): void {
  cart.push({ item, date: Date.now() });
};
```

**好的：**

```ts
function addItemToCart(cart: CartItem[], item: Item): CartItem[] {
  return [...cart, { item, date: Date.now() }];
};
```

**[⬆ 返回目录](#目录)**

### Don't write to global functions

### 不要写入全局函数

Polluting globals is a bad practice in JavaScript because you could clash with another library and the user of your API would be none-the-wiser until they get an exception in production. Let's think about an example: what if you wanted to extend JavaScript's native Array method to have a `diff` method that could show the difference between two arrays? You could write your new function to the `Array.prototype`, but it could clash with another library that tried to do the same thing. What if that other library was just using `diff` to find the difference between the first and last elements of an array? This is why it would be much better to just use classes and simply extend the `Array` global.

污染全局在 JavaScript 中是一个不好的做法， 因为你可能会和另外一个类库冲突， 你的 API 的用户
可能不够聪明， 直到他们得到在生产环境得到一个异常。 让我们来考虑这样一个例子： 假设你要扩展
JavaScript 的 原生 `Array` ， 添加一个可以显示两个数组的不同之处的 `diff` 方法， 你可以在
`Array.prototype` 中写一个新的方法， 但是它可能会和尝试做相同事情的其它类库发生冲突。 如果有
另外一个类库仅仅使用 `diff` 方法来查找数组的第一个元素和最后一个元素之间的不同之处呢？ 这就是
为什么使用 ES2015/ES6 的类是一个更好的做法的原因， 只要简单的扩展全局的 `Array` 即可。

**不好的：**

```ts
declare global {
  interface Array<T> {
    diff(other: T[]): Array<T>;
  }
}

if (!Array.prototype.diff) {
  Array.prototype.diff = function <T>(other: T[]): T[] {
    const hash = new Set(other);
    return this.filter(elem => !hash.has(elem));
  };
}
```

**好的：**

```ts
class MyArray<T> extends Array<T> {
  diff(other: T[]): T[] {
    const hash = new Set(other);
    return this.filter(elem => !hash.has(elem));
  };
}
```

**[⬆ 返回目录](#目录)**

### Favor functional programming over imperative programming

### 函数式编程优于指令式编程

Favor this style of programming when you can.

当你可以使用函数式编程风格时请尽情使用。

**不好的：**

```ts
const contributions = [
  {
    name: 'Uncle Bobby',
    linesOfCode: 500
  }, {
    name: 'Suzie Q',
    linesOfCode: 1500
  }, {
    name: 'Jimmy Gosling',
    linesOfCode: 150
  }, {
    name: 'Gracie Hopper',
    linesOfCode: 1000
  }
];

let totalOutput = 0;

for (let i = 0; i < contributions.length; i++) {
  totalOutput += contributions[i].linesOfCode;
}
```

**好的：**

```ts
const contributions = [
  {
    name: 'Uncle Bobby',
    linesOfCode: 500
  }, {
    name: 'Suzie Q',
    linesOfCode: 1500
  }, {
    name: 'Jimmy Gosling',
    linesOfCode: 150
  }, {
    name: 'Gracie Hopper',
    linesOfCode: 1000
  }
];

const totalOutput = contributions
  .reduce((totalLines, output) => totalLines + output.linesOfCode, 0);
```

**[⬆ 返回目录](#目录)**

### Encapsulate conditionals

### 封装条件语句

**不好的：**

```ts
if (subscription.isTrial || account.balance > 0) {
  // ...
}
```

**好的：**

```ts
function canActivateService(subscription: Subscription, account: Account) {
  return subscription.isTrial || account.balance > 0
}

if (canActivateService(subscription, account)) {
  // ...
}
```

**[⬆ 返回目录](#目录)**

### Avoid negative conditionals

### 避免负面条件

**不好的：**

```ts
function isEmailNotUsed(email: string): boolean {
  // ...
}

if (isEmailNotUsed(email)) {
  // ...
}
```

**好的：**

```ts
function isEmailUsed(email): boolean {
  // ...
}

if (!isEmailUsed(node)) {
  // ...
}
```

**[⬆ 返回目录](#目录)**

### Avoid conditionals

### 避免条件语句

This seems like an impossible task. Upon first hearing this, most people say, "how am I supposed to do anything without an `if` statement?" The answer is that you can use polymorphism to achieve the same task in many cases. The second question is usually, "well that's great but why would I want to do that?" The answer is a previous clean code concept we learned: a function should only do one thing. When you have classes and functions that have `if` statements, you are telling your user that your function does more than one thing. Remember, just do one thing.

这看起来似乎是一个不可能的任务。 第一次听到这个时， 多数人会说： “没有 `if` 语句还能期望我干
啥呢”， 答案是多数情况下你可以使用多态来完成同样的任务。 第二个问题通常是 “好了， 那么做很棒，
但是我为什么想要那样做呢”， 答案是我们学到的上一条代码整洁之道的理念： 一个函数应当只做一件事情。
当你有使用 `if` 语句的类/函数是， 你在告诉你的用户你的函数做了不止一件事情。 记住： 只做一件
事情。

**不好的：**

```ts
class Airplane {
  private type: string;
  // ...

  getCruisingAltitude() {
    switch (this.type) {
      case '777':
        return this.getMaxAltitude() - this.getPassengerCount();
      case 'Air Force One':
        return this.getMaxAltitude();
      case 'Cessna':
        return this.getMaxAltitude() - this.getFuelExpenditure();
      default:
        throw new Error('Unknown airplane type.');
    }
  }

  private getMaxAltitude(): number {
    // ...
  }
}
```

**好的：**

```ts
abstract class Airplane {
  protected getMaxAltitude(): number {
    // shared logic with subclasses ...
  }

  // ...
}

class Boeing777 extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude() - this.getPassengerCount();
  }
}

class AirForceOne extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude();
  }
}

class Cessna extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude() - this.getFuelExpenditure();
  }
}
```

**[⬆ 返回目录](#目录)**

### Avoid type checking

### 避免类型检查

TypeScript is a strict syntactical superset of JavaScript and adds optional static type checking to the language.
Always prefer to specify types of variables, parameters and return values to leverage the full power of TypeScript features.
It makes refactoring more easier.

TypeScript 是 JavaScript 的一个严格语法的超急， 为这门语言增加了可选的静态类型检查。
始终倾向于给变量、 参数以及返回值定义类型一体现 TypeScript 的完整特征。
这将使重构变得更加容易。

**不好的**

```ts
function travelToTexas(vehicle: Bicycle | Car) {
  if (vehicle instanceof Bicycle) {
    vehicle.pedal(currentLocation, new Location('texas'));
  } else if (vehicle instanceof Car) {
    vehicle.drive(currentLocation, new Location('texas'));
  }
}
```

**好的**

```ts
type Vehicle = Bicycle | Car;

function travelToTexas(vehicle: Vehicle) {
  vehicle.move(currentLocation, new Location('texas'));
}
```

**[⬆ 返回目录](#目录)**

### Don't over-optimize

### 不要过度优化

Modern browsers do a lot of optimization under-the-hood at runtime. A lot of times, if you are optimizing then you are just wasting your time. There are good [resources](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers) for seeing where optimization is lacking. Target those in the meantime, until they are fixed if they can be.

现代化浏览器运行时在幕后做大量的优化， 在大多数的时间， 做优化就是在浪费你的时间。 [这些是好的
资源](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)， 用来
查看那些地方需要优化。 为这些而优化， 直到他们被修正。

**不好的：**

```ts
// On old browsers, each iteration with uncached `list.length` would be costly
// because of `list.length` recomputation. In modern browsers, this is optimized.
// 在旧的浏览器上， 每次循环 `list.length` 都没有被缓存， 会导致不必要的开销， 因为要重新计
// 算 `list.length` 。 在现代化浏览器上， 这个已经被优化了。
for (let i = 0, len = list.length; i < len; i++) {
  // ...
}
```

**好的：**

```ts
for (let i = 0; i < list.length; i++) {
  // ...
}
```

**[⬆ 返回目录](#目录)**

### 移除僵尸代码

Dead code is just as bad as duplicate code. There's no reason to keep it in your codebase.
If it's not being called, get rid of it! It will still be safe in your version history if you still need it.

僵死代码和冗余代码同样糟糕。 没有理由在代码库中保存它。 如果它不会被调用， 就删掉它。 当你需要
它时， 它依然保存在版本历史记录中。

**不好的：**

```ts
function oldRequestModule(url: string) {
  // ...
}

function requestModule(url: string) {
  // ...
}

const req = requestModule;
inventoryTracker('apples', req, 'www.inventory-awesome.io');
```

**好的：**

```ts
function requestModule(url: string) {
  // ...
}

const req = requestModule;
inventoryTracker('apples', req, 'www.inventory-awesome.io');
```

**[⬆ 返回目录](#目录)**

### Use iterators and generators

### 使用枚举器和生成器

Use generators and iterables when working with collections of data used like a stream.  
There are some good reasons:

- decouples the callee from the generator implementation in a sense that callee decides how many
items to access
- lazy execution, items are streamed on demand
- built-in support for iterating items using the `for-of` syntax
- iterables allow to implement optimized iterator patterns

当像流一样处理数据集时， 使用生成器和枚举器。 这样做的好处是：

- 被调用者与生成器解耦， 这样被调用者可以决定处理多少项；
- 延迟执行， 元素按流式按需处理；
- 允许为枚举模式实现进行优化；

**不好的：**

```ts
function fibonacci(n: number): number[] {
  if (n === 1) return [0];
  if (n === 2) return [0, 1];

  const items: number[] = [0, 1];
  while (items.length < n) {
    items.push(items[items.length - 2] + items[items.length - 1]);
  }

  return items;
}

function print(n: number) {
  fibonacci(n).forEach(fib => console.log(fib));
}

// Print first 10 Fibonacci numbers.
print(10);
```

**好的：**

```ts
// Generates an infinite stream of Fibonacci numbers.
// The generator doesn't keep the array of all numbers.
// 生成一个无限长的斐波那契数字流， 生成器并没有保存数字数组。
function* fibonacci(): IterableIterator<number> {
  let [a, b] = [0, 1];

  while (true) {
    yield a;
    [a, b] = [b, a + b];
  }
}

function print(n: number) {
  let i = 0;
  for (const fib in fibonacci()) {
    if (i++ === n) break;  
    console.log(fib);
  }  
}

// Print first 10 Fibonacci numbers.
print(10);
```

There are libraries that allow working with iterables in a similar way as with native arrays, by
chaining methods like `map`, `slice`, `forEach` etc. See [itiriri](https://www.npmjs.com/package/itiriri) for
an example of advanced manipulation with iterables (or [itiriri-async](https://www.npmjs.com/package/itiriri-async) for manipulation of async iterables).

一些类库可以与原生数组类似的方式使用枚举， 将 `map`， `slice`， `forEach` 等方法串联到一起。 请参考 [itiriri](https://www.npmjs.com/package/itiriri) 的高级枚举处理示例（或者 [itiriri-async](https://www.npmjs.com/package/itiriri-async) 的异步枚举处理）。

```ts
import itiriri from 'itiriri';

function* fibonacci(): IterableIterator<number> {
  let [a, b] = [0, 1];
 
  while (true) {
    yield a;
    [a, b] = [b, a + b];
  }
}

itiriri(fibonacci())
  .take(10)
  .forEach(fib => console.log(fib));
```

**[⬆ 返回目录](#目录)**

## Objects and Data Structures

## 对象和数据结构

### Use getters and setters

### 使用 getter 和 setter

TypeScript supports getter/setter syntax.
Using getters and setters to access data from objects that encapsulate behavior could be better that simply looking for a property on an object.
"Why?" you might ask. Well, here's a list of reasons:

- When you want to do more beyond getting an object property, you don't have to look up and change every accessor in your codebase.
- Makes adding validation simple when doing a `set`.
- Encapsulates the internal representation.
- Easy to add logging and error handling when getting and setting.
- You can lazy load your object's properties, let's say getting it from a server.

TypeScript 支持 getter/setter 语法。 正因为如此， 使用 getters 和 setters 来访问对象上的数据比简单的在一个对象上查找属性
要好得多。 “为什么？” 你可能会问， 好吧， 原因请看下面的列表：

* 当你想在获取一个对象属性的背后做更多的事情时， 你不需要在代码库中查找和修改每一处访问；
* 使用 `set` 可以让添加验证变得容易；
* 封装内部实现；
* 使用 getting 和 setting 时， 容易添加日志和错误处理；
* 你可以延迟加载对象的属性， 比如说从服务器获取。

**不好的：**

```ts
type BankAccount = {
  balance: number;
  // ...
}

const value = 100;
const account: BankAccount = {
  balance: 0,
  // ...
};

if (value < 0) {
  throw new Error('Cannot set negative balance.');
}

account.balance = value;
```

**好的：**

```ts
class BankAccount {
  private accountBalance: number = 0;

  get balance(): number {
    return this.accountBalance;
  }

  set balance(value: number) {
    if (value < 0) {
      throw new Error('Cannot set negative balance.');
    }

    this.accountBalance = value;
  }

  // ...
}

// Now `BankAccount` encapsulates the validation logic.
// If one day the specifications change, and we need extra validation rule,
// we would have to alter only the `setter` implementation,
// leaving all dependent code unchanged.
// 现在 `BankAccount` 封装了验证逻辑， 如果某一天需求变化了， 需要添加额外的验证规则， 我们只需要修改 `setter` 即可， 其它依赖性代码则无需修改。
const account = new BankAccount();
account.balance = 100;
```

**[⬆ 返回目录](#目录)**

### Make objects have private/protected members

### 让对象拥有私有的/受保护的成员

TypeScript supports `public` *(default)*, `protected` and `private` accessors on class members.  

TypeScript 支持在类成员上添加 `public` *(默认)* ， `protected` 和 `private` 修饰符。

**不好的：**

```ts
class Circle {
  radius: number;
  
  constructor(radius: number) {
    this.radius = radius;
  }

  perimeter() {
    return 2 * Math.PI * this.radius;
  }

  surface() {
    return Math.PI * this.radius * this.radius;
  }
}
```

**好的：**

```ts
class Circle {
  constructor(private readonly radius: number) {
  }

  perimeter() {
    return 2 * Math.PI * this.radius;
  }

  surface() {
    return Math.PI * this.radius * this.radius;
  }
}
```

**[⬆ 返回目录](#目录)**

### Prefer immutability

### 倾向于不可变性

TypeScript's type system allows you to mark individual properties on an interface / class as *readonly*. This allows you to work in a functional way (unexpected mutation is bad).  
For more advanced scenarios there is a built-in type `Readonly` that takes a type `T` and marks all of its properties as readonly using mapped types (see [mapped types](https://www.typescriptlang.org/docs/handbook/advanced-types.html#mapped-types)).

TypeScript 的类型系统允许将类/接口的某些属性标记为 *只读* 。 这允许你在一个很舒适的方式下工作（不需要考虑意外的变化）。 针对更加高级的场景， 有一个内置的 `Readonly` 类型， 它接受一个类型 `T` ， 实用类型映射， 将类型 `T` 的全部属性统统标记为只读（参考 [mapped types](https://www.typescriptlang.org/docs/handbook/advanced-types.html#mapped-types)）。

**不好的：**

```ts
interface Config {
  host: string;
  port: string;
  db: string;
}
```

**好的：**

```ts
interface Config {
  readonly host: string;
  readonly port: string;
  readonly db: string;
}
```

**[⬆ 返回目录](#目录)**

### type vs. interface

### 类型 vs. 接口

Use type when you might need a union or intersection. Use interface when you want `extends` or `implements`. There is no strict rule however, use the one that works for you.  
For a more detailed explanation refer to this [answer](https://stackoverflow.com/questions/37233735/typescript-interfaces-vs-types/54101543#54101543) about the differences between `type` and `interface` in TypeScript.

当需要并集或者交集时， 实用类型。 当需要扩展或实现时， 实用接口。 然而并没有严格的规则， 哪个适合就用哪个。 若需要一个更加详细的解释， 请参考关于 TypeScript 的类型和接口之间的不同的这个[答案](https://stackoverflow.com/questions/37233735/typescript-interfaces-vs-types/54101543#54101543)。

**不好的：**

```ts
interface EmailConfig {
  // ...
}

interface DbConfig {
  // ...
}

interface Config {
  // ...
}

//...

type Shape = {
  // ...
}
```

**好的：**

```ts

type EmailConfig = {
  // ...
}

type DbConfig = {
  // ...
}

type Config  = EmailConfig | DbConfig;

// ...

interface Shape {
  // ...
}

class Circle implements Shape {
  // ...
}

class Square implements Shape {
  // ...
}
```

**[⬆ 返回目录](#目录)**

## Classes

## 类

### Classes should be small

### 类应当小

The class' size is measured by it's responsibility. Following the *Single Responsibility principle* a class should be small.

类的大小由它的职责衡量。 根据 *单一职责原则* 一个类应该小。

**不好的：**

```ts
class Dashboard {
  getLanguage(): string { /* ... */ }
  setLanguage(language: string): void { /* ... */ }
  showProgress(): void { /* ... */ }
  hideProgress(): void { /* ... */ }
  isDirty(): boolean { /* ... */ }
  disable(): void { /* ... */ }
  enable(): void { /* ... */ }
  addSubscription(subscription: Subscription): void { /* ... */ }
  removeSubscription(subscription: Subscription): void { /* ... */ }
  addUser(user: User): void { /* ... */ }
  removeUser(user: User): void { /* ... */ }
  goToHomePage(): void { /* ... */ }
  updateProfile(details: UserDetails): void { /* ... */ }
  getVersion(): string { /* ... */ }
  // ...
}

```

**好的：**

```ts
class Dashboard {
  disable(): void { /* ... */ }
  enable(): void { /* ... */ }
  getVersion(): string { /* ... */ }
}

// split the responsibilities by moving the remaining methods to other classes
// 将其它方法移到其它类以拆分职责
// ...
```

**[⬆ 返回目录](#目录)**

### High cohesion and low coupling

### 高内聚和低耦合

Cohesion defines the degree to which class members are related to each other. Ideally, all fields within a class should be used by each method.
We then say that the class is *maximally cohesive*. In practice, this however is not always possible, nor even advisable. You should however prefer cohesion to be high.  

Coupling refers to how related or dependent are two classes toward each other. Classes are said to be low coupled if changes in one of them doesn't affect the other one.  
  
Good software design has **high cohesion** and **low coupling**.

内聚定义了类成员彼此相关的程度。 理想情况下，每个方法都应使用类中的所有字段。
然后我们说这个类是*最高内聚*。 实际上， 这并非总是可行， 甚至不可取。 但是你应该更喜欢高内聚。

耦合指的是两个类相互依赖或相互依赖的程度。 如果其中一个类中的更改不影响其它的， 则称这些类是低耦合的。

好的软件设计拥有 **高内聚** 和 **低耦合** 。

**不好的：**

```ts
class UserManager {
  // Bad: each private variable is used by one or another group of methods.
  // It makes clear evidence that the class is holding more than a single responsibility.
  // If I need only to create the service to get the transactions for a user,
  // I'm still forced to pass and instance of `emailSender`.
  // 不好的： 每一个私有变量仅仅被一组或另一组方法使用， 这很明显说明这个类在兼负多个职责。 当我仅仅需要一个服务来获取用户事务时， 还得传递另外一个 `emailSender` 的实例。
  constructor(
    private readonly db: Database,
    private readonly emailSender: EmailSender) {
  }

  async getUser(id: number): Promise<User> {
    return await db.users.findOne({ id });
  }

  async getTransactions(userId: number): Promise<Transaction[]> {
    return await db.transactions.find({ userId });
  }

  async sendGreeting(): Promise<void> {
    await emailSender.send('Welcome!');
  }

  async sendNotification(text: string): Promise<void> {
    await emailSender.send(text);
  }

  async sendNewsletter(): Promise<void> {
    // ...
  }
}
```

**好的：**

```ts
class UserService {
  constructor(private readonly db: Database) {
  }

  async getUser(id: number): Promise<User> {
    return await this.db.users.findOne({ id });
  }

  async getTransactions(userId: number): Promise<Transaction[]> {
    return await this.db.transactions.find({ userId });
  }
}

class UserNotifier {
  constructor(private readonly emailSender: EmailSender) {
  }

  async sendGreeting(): Promise<void> {
    await this.emailSender.send('Welcome!');
  }

  async sendNotification(text: string): Promise<void> {
    await this.emailSender.send(text);
  }

  async sendNewsletter(): Promise<void> {
    // ...
  }
}
```

**[⬆ 返回目录](#目录)**

### Prefer composition over inheritance

### 组合优先于继承

As stated famously in [Design Patterns](https://en.wikipedia.org/wiki/Design_Patterns) by the Gang of Four, you should *prefer composition over inheritance* where you can. There are lots of good reasons to use inheritance and lots of good reasons to use composition. The main point for this maxim is that if your mind instinctively goes for inheritance, try to think if composition could model your problem better. In some cases it can.  
  
You might be wondering then, "when should I use inheritance?" It depends on your problem at hand, but this is a decent list of when inheritance makes more sense than composition:

1. Your inheritance represents an "is-a" relationship and not a "has-a" relationship (Human->Animal vs. User->UserDetails).

2. You can reuse code from the base classes (Humans can move like all animals).

3. You want to make global changes to derived classes by changing a base class. (Change the caloric expenditure of all animals when they move).

正如[*设计模式四人帮*](https://en.wikipedia.org/wiki/Design_Patterns)所述， 如果可能，
你应该优先使用组合而不是继承。 有许多好的理由去使用继承， 也有许多好的理由去使用组合。这个格言
的重点是， 如果你本能的观点是继承， 那么请想一下组合能否更好的为你的问题建模。 很多情况下它真的
可以。

那么你也许会这样想， “我什么时候改使用继承？” 这取决于你手上的问题， 不过这儿有一个像样的列表说
明什么时候继承比组合更好用：

1. 你的继承表示"是一个"的关系而不是"有一个"的关系（人类->动物 vs 用户->用户详情）；
2. 你可以重用来自基类的代码（人可以像所有动物一样行动）；
3. 你想通过基类对子类进行全局的修改（改变所有动物行动时的热量消耗）；

**不好的：**

```ts
class Employee {
  constructor(
    private readonly name: string,
    private readonly email: string) {
  }

  // ...
}

// Bad because Employees "have" tax data. EmployeeTaxData is not a type of Employee
// 不好是因为雇员“有”税率数据， EmployeeTaxData 不是一个 Employee 类型。
class EmployeeTaxData extends Employee {
  constructor(
    name: string,
    email: string,
    private readonly ssn: string,
    private readonly salary: number) {
    super(name, email);
  }

  // ...
}
```

**不好的：**

```ts
class Employee {
  private taxData: EmployeeTaxData;

  constructor(
    private readonly name: string,
    private readonly email: string) {
  }

  setTaxData(ssn: string, salary: number): Employee {
    this.taxData = new EmployeeTaxData(ssn, salary);
    return this;
  }

  // ...
}

class EmployeeTaxData {
  constructor(
    public readonly ssn: string,
    public readonly salary: number) {
  }

  // ...
}
```

**[⬆ 返回目录](#目录)**

### Use method chaining

### 使用方法链

This pattern is very useful and commonly used in many libraries. It allows your code to be expressive, and less verbose. For that reason, use method chaining and take a look at how clean your code will be.

这个模式在 JavaScript 中是非常有用的， 并且在许多类库使用。 它使你的代码变得富有表现力， 并减少啰嗦。 因为这个原因， 我说， 使用方法链然后再看看你的代码会变得多么简洁。

**不好的：**

```ts
class QueryBuilder {
  private collection: string;
  private pageNumber: number = 1;
  private itemsPerPage: number = 100;
  private orderByFields: string[] = [];

  from(collection: string): void {
    this.collection = collection;
  }

  page(number: number, itemsPerPage: number = 100): void {
    this.pageNumber = number;
    this.itemsPerPage = itemsPerPage;
  }

  orderBy(...fields: string[]): void {
    this.orderByFields = fields;
  }

  build(): Query {
    // ...
  }
}

// ...

const queryBuilder = new QueryBuilder();
queryBuilder.from('users');
queryBuilder.page(1, 100);
queryBuilder.orderBy('firstName', 'lastName');

const query = queryBuilder.build();
```

**好的：**

```ts
class QueryBuilder {
  private collection: string;
  private pageNumber: number = 1;
  private itemsPerPage: number = 100;
  private orderByFields: string[] = [];

  from(collection: string): this {
    this.collection = collection;
    return this;
  }

  page(number: number, itemsPerPage: number = 100): this {
    this.pageNumber = number;
    this.itemsPerPage = itemsPerPage;
    return this;
  }

  orderBy(...fields: string[]): this {
    this.orderByFields = fields;
    return this;
  }

  build(): Query {
    // ...
  }
}

// ...

const query = new QueryBuilder()
  .from('users')
  .page(1, 100)
  .orderBy('firstName', 'lastName')
  .build();
```

**[⬆ 返回目录](#目录)**

## SOLID

### Single Responsibility Principle (SRP)

### 单一职责原则 (SRP)

As stated in Clean Code, "There should never be more than one reason for a class to change". It's tempting to jam-pack a class with a lot of functionality, like when you can only take one suitcase on your flight. The issue with this is that your class won't be conceptually cohesive and it will give it many reasons to change. Minimizing the amount of times you need to change a class is important. It's important because if too much functionality is in one class and you modify a piece of it, it can be difficult to understand how that will affect other dependent modules in your codebase.

正如代码整洁之道所述， “永远不要有超过一个理由来修改一个类”。 给一个类塞满许多功能， 就像你在航
班上只能带一个行李箱一样， 这样做的问题你的类不会有理想的内聚性， 将会有太多的理由来对它进行修改。
最小化需要修改一个类的次数时很重要的， 因为如果一个类拥有太多的功能， 一旦你修改它的一小部分，
将会很难弄清楚会对代码库中的其它模块造成什么影响。

**不好的：**

```ts
class UserSettings {
  constructor(private readonly user: User) {
  }

  changeSettings(settings: UserSettings) {
    if (this.verifyCredentials()) {
      // ...
    }
  }

  verifyCredentials() {
    // ...
  }
}
```

**好的：**

```ts
class UserAuth {
  constructor(private readonly user: User) {
  }

  verifyCredentials() {
    // ...
  }
}


class UserSettings {
  private readonly auth: UserAuth;

  constructor(private readonly user: User) {
    this.auth = new UserAuth(user);
  }

  changeSettings(settings: UserSettings) {
    if (this.auth.verifyCredentials()) {
      // ...
    }
  }
}
```

**[⬆ 返回目录](#目录)**

### Open/Closed Principle (OCP)

### 开闭原则 (OCP)

As stated by Bertrand Meyer, "software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification." What does that mean though? This principle basically states that you should allow users to add new functionalities without changing existing code.

Bertrand Meyer 说过， “软件实体 (类， 模块， 函数等) 应该为扩展开放， 但是为修改关闭。” 这
是什么意思呢？ 这个原则基本上说明了你应该允许用户添加功能而不必修改现有的代码。

**不好的：**

```ts
class AjaxAdapter extends Adapter {
  constructor() {
    super();
  }

  // ...
}

class NodeAdapter extends Adapter {
  constructor() {
    super();
  }

  // ...
}

class HttpRequester {
  constructor(private readonly adapter: Adapter) {
  }

  async fetch<T>(url: string): Promise<T> {
    if (this.adapter instanceof AjaxAdapter) {
      const response = await makeAjaxCall<T>(url);
      // transform response and return
    } else if (this.adapter instanceof NodeAdapter) {
      const response = await makeHttpCall<T>(url);
      // transform response and return
    }
  }
}

function makeAjaxCall<T>(url: string): Promise<T> {
  // request and return promise
}

function makeHttpCall<T>(url: string): Promise<T> {
  // request and return promise
}
```

**好的：**

```ts
abstract class Adapter {
  abstract async request<T>(url: string): Promise<T>;

  // code shared to subclasses ...
}

class AjaxAdapter extends Adapter {
  constructor() {
    super();
  }

  async request<T>(url: string): Promise<T>{
    // request and return promise
  }

  // ...
}

class NodeAdapter extends Adapter {
  constructor() {
    super();
  }

  async request<T>(url: string): Promise<T>{
    // request and return promise
  }

  // ...
}

class HttpRequester {
  constructor(private readonly adapter: Adapter) {
  }

  async fetch<T>(url: string): Promise<T> {
    const response = await this.adapter.request<T>(url);
    // transform response and return
  }
}
```

**[⬆ 返回目录](#目录)**

### Liskov Substitution Principle (LSP)

### 里氏代换原则 (LSP)

This is a scary term for a very simple concept. It's formally defined as "If S is a subtype of T, then objects of type T may be replaced with objects of type S (i.e., objects of type S may substitute objects of type T) without altering any of the desirable properties of that program (correctness, task performed, etc.)." That's an even scarier definition.  
  
The best explanation for this is if you have a parent class and a child class, then the base class and child class can be used interchangeably without getting incorrect results. This might still be confusing, so let's take a look at the classic Square-Rectangle example. Mathematically, a square is a rectangle, but if you model it using the "is-a" relationship via inheritance, you quickly get into trouble.

这是针对一个非常简单的里面的一个恐怖意图， 它的正式定义是： “如果 S 是 T 的一个子类型， 那么类
型为 T 的对象可以被类型为 S 的对象替换（例如， 类型为 S 的对象可作为类型为 T 的替代品）儿不需
要修改目标程序的期望性质 （正确性、 任务执行性等）。” 这甚至是个恐怖的定义。

最好的解释是， 如果你又一个基类和一个子类， 那个基类和字类可以互换而不会产生不正确的结果。 这可
能还有有些疑惑， 让我们来看一下这个经典的正方形与矩形的例子。 从数学上说， 一个正方形是一个矩形，
但是你用 "is-a" 的关系用继承来实现， 你将很快遇到麻烦。

**不好的：**

```ts
class Rectangle {
  constructor(
    protected width: number = 0,
    protected height: number = 0) {

  }

  setColor(color: string): this {
    // ...
  }

  render(area: number) {
    // ...
  }

  setWidth(width: number): this {
    this.width = width;
    return this;
  }

  setHeight(height: number): this {
    this.height = height;
    return this;
  }

  getArea(): number {
    return this.width * this.height;
  }
}

class Square extends Rectangle {
  setWidth(width: number): this {
    this.width = width;
    this.height = width;
    return this;
  }

  setHeight(height: number): this {
    this.width = height;
    this.height = height;
    return this;
  }
}

function renderLargeRectangles(rectangles: Rectangle[]) {
  rectangles.forEach((rectangle) => {
    const area = rectangle
      .setWidth(4)
      .setHeight(5)
      .getArea(); // BAD: Returns 25 for Square. Should be 20.
    rectangle.render(area);
  });
}

const rectangles = [new Rectangle(), new Rectangle(), new Square()];
renderLargeRectangles(rectangles);
```

**好的：**

```ts
abstract class Shape {
  setColor(color: string): this {
    // ...
  }

  render(area: number) {
    // ...
  }

  abstract getArea(): number;
}

class Rectangle extends Shape {
  constructor(
    private readonly width = 0,
    private readonly height = 0) {
    super();
  }

  getArea(): number {
    return this.width * this.height;
  }
}

class Square extends Shape {
  constructor(private readonly length: number) {
    super();
  }

  getArea(): number {
    return this.length * this.length;
  }
}

function renderLargeShapes(shapes: Shape[]) {
  shapes.forEach((shape) => {
    const area = shape.getArea();
    shape.render(area);
  });
}

const shapes = [new Rectangle(4, 5), new Rectangle(4, 5), new Square(5)];
renderLargeShapes(shapes);
```

**[⬆ 返回目录](#目录)**

### Interface Segregation Principle (ISP)

### 接口隔离原则 (ISP)

ISP states that "Clients should not be forced to depend upon interfaces that they do not use.". This principle is very much related to the Single Responsibility Principle.
What it really means is that you should always design your abstractions in a way that the clients that are using the exposed methods do not get the whole pie instead. That also include imposing the clients with the burden of implementing methods that they don’t actually need.

接口隔离原则说的是 “客户端不应该强制依赖他们不需要的接口。” 这个原则与单一职责原则紧密相关。

它的真正含义是你应该总是设计一种抽象的方式，使用部分方法的客户端不会得到全部实现。 这还包括禁止客户端实现他们不需要的方法。

**不好的：**

```ts
interface SmartPrinter {
  print();
  fax();
  scan();
}

class AllInOnePrinter implements SmartPrinter {
  print() {
    // ...
  }  
  
  fax() {
    // ...
  }

  scan() {
    // ...
  }
}

class EconomicPrinter implements SmartPrinter {
  print() {
    // ...
  }  
  
  fax() {
    throw new Error('Fax not supported.');
  }

  scan() {
    throw new Error('Scan not supported.');
  }
}
```

**好的：**

```ts
interface Printer {
  print();
}

interface Fax {
  fax();
}

interface Scanner {
  scan();
}

class AllInOnePrinter implements Printer, Fax, Scanner {
  print() {
    // ...
  }  
  
  fax() {
    // ...
  }

  scan() {
    // ...
  }
}

class EconomicPrinter implements Printer {
  print() {
    // ...
  }
}
```

**[⬆ 返回目录](#目录)**

### Dependency Inversion Principle (DIP)

### 依赖反转原则 (DIP)

This principle states two essential things:

1. High-level modules should not depend on low-level modules. Both should depend on abstractions.

2. Abstractions should not depend upon details. Details should depend on abstractions.

这个原则阐述了两个重要的事情：

1. 高级模块不应该依赖于低级模块， 两者都应该依赖与抽象；
2. 抽象不应当依赖于具体实现， 具体实现应当依赖于抽象。

This can be hard to understand at first, but if you've worked with Angular, you've seen an implementation of this principle in the form of Dependency Injection (DI). While they are not identical concepts, DIP keeps high-level modules from knowing the details of its low-level modules and setting them up. It can accomplish this through DI. A huge benefit of this is that it reduces the coupling between modules. Coupling is a very bad development pattern because it makes your code hard to refactor.  

这个一开始会很难理解， 但是如果你使用过 Angular.js ， 你应该已经看到过通过依赖注入来实现的这个原则， 虽然他们不是相同的概念， 依赖反转原则让高级模块远离低级模块的细节和创建， 可以通过 DI 来实现。 这样做的巨大益处是降低模块间的耦合。 耦合是一个非常糟糕的开发模式， 因为会导致代码难于重构。

DIP is usually achieved by a using an inversion of control (IoC) container. An example of a powerful IoC container for TypeScript is [InversifyJs](https://www.npmjs.com/package/inversify)

DIP 通常通过使用控制反转 (IoC) 容器来达到。 [InversifyJs](https://www.npmjs.com/package/inversify) 是 TypeScript 下的一个强大的 IoC 容器示例。

**不好的：**

```ts
import { readFile as readFileCb } from 'fs';
import { promisify } from 'util';

const readFile = promisify(readFileCb);

type ReportData = {
  // ..
}

class XmlFormatter {
  parse<T>(content: string): T {
    // Converts an XML string to an object T
  }
}

class ReportReader {

  // BAD: We have created a dependency on a specific request implementation.
  // We should just have ReportReader depend on a parse method: `parse`
  private readonly formatter = new XmlFormatter();

  async read(path: string): Promise<ReportData> {
    const text = await readFile(path, 'UTF8');
    return this.formatter.parse<ReportData>(text);
  }
}

// ...
const reader = new ReportReader();
await report = await reader.read('report.xml');
```

**好的：**

```ts
import { readFile as readFileCb } from 'fs';
import { promisify } from 'util';

const readFile = promisify(readFileCb);

type ReportData = {
  // ..
}

interface Formatter {
  parse<T>(content: string): T;
}

class XmlFormatter implements Formatter {
  parse<T>(content: string): T {
    // Converts an XML string to an object T
  }
}


class JsonFormatter implements Formatter {
  parse<T>(content: string): T {
    // Converts a JSON string to an object T
  }
}

class ReportReader {
  constructor(private readonly formatter: Formatter) {
  }

  async read(path: string): Promise<ReportData> {
    const text = await readFile(path, 'UTF8');
    return this.formatter.parse<ReportData>(text);
  }
}

// ...
const reader = new ReportReader(new XmlFormatter());
await report = await reader.read('report.xml');

// or if we had to read a json report
const reader = new ReportReader(new JsonFormatter());
await report = await reader.read('report.json');
```

**[⬆ 返回目录](#目录)**

## Testing

## 测试

Testing is more important than shipping. If you have no tests or an inadequate amount, then every time you ship code you won't be sure that you didn't break anything.
Deciding on what constitutes an adequate amount is up to your team, but having 100% coverage (all statements and branches)
is how you achieve very high confidence and developer peace of mind. This means that in addition to having a great testing framework, you also need to use a good [coverage tool](https://github.com/gotwarlost/istanbul).

There's no excuse to not write tests. There are [plenty of good JS test frameworks](http://jstherightway.org/#testing-tools) with typings support for TypeScript, so find one that your team prefers. When you find one that works for your team, then aim to always write tests for every new feature/module you introduce. If your preferred method is Test Driven Development (TDD), that is great, but the main point is to just make sure you are reaching your coverage goals before launching any feature, or refactoring an existing one.  

测试比发布更加重要。 如果你没有测试或者测试不够充分， 每次发布时你就不能确认没有破坏任何事情。
测试的量由你的团队决定， 但是拥有 100% 的覆盖率(包括所有的语句和分支)是你为什么能达到高度自信
和内心的平静。 这意味着需要一个额外的伟大的测试框架， 也需要一个好的[覆盖率工具](http://gotwarlost.github.io/istanbul/)。

没有理由不写测试。 这里有[大量的优秀的 JS 测试框架](http://jstherightway.org/#testing-tools)，
选一个适合你的团队的即可。 当为团队选择了测试框架之后， 接下来的目标是为生产的每一个新的功能／模
块编写测试。 如果你倾向于测试驱动开发(TDD)， 那就太棒了， 但是要点是确认你在上线任何功能或者重
构一个现有功能之前， 达到了需要的目标覆盖率。

### The three laws of TDD

### TDD 的三大纪律

1. You are not allowed to write any production code unless it is to make a failing unit test pass.

2. You are not allowed to write any more of a unit test than is sufficient to fail; and compilation failures are failures.

3. You are not allowed to write any more production code than is sufficient to pass the one failing unit test.

1. 不得写任何生产代码， 除非是修复了一个失败的单元测试；
2. 出现任何失败， 不得继续编写任何单元测试； 编译失败也是失败；
3. 只要有失败的单元测试， 不得继续编写任何生产代码；

**[⬆ 返回目录](#目录)**

### F.I.R.S.T. rules

### F.I.R.S.T. 规则

Clean tests should follow the rules:

- **Fast** tests should be fast because we want to run them frequently.

- **Independent** tests should not depend on each other. They should provide same output whether run independently or all together in any order.

- **Repeatable** tests should be repeatable in any environment and there should be no excuse for why they fail.

- **Self-Validating** a test should answer with either *Passed* or *Failed*. You don't need to compare log files to answer if a test passed.

- **Timely** unit tests should be written before the production code. If you write tests after the production code, you might find writing tests too hard.

简洁测试应当遵循的规则：

- **快速 (Fast)** 测试应当很快， 因为我们希望经常运行他们。

- **独立 (Independent)** 测试不应当相互依赖。 不管是单独运行还是一起以任意顺序运行， 应当有相同的输出。

- **重复 (Repeatable)** 测试应当是在任何环境下可重复的， 测试失败不应有任何理由。

- **自验证 (Self-Validating)** 一个测试的结果应该是 *通过* 或者 *失败* 。 不需要去比较日志文件来判断测试是否通过。

- **及时 (Timely)** 单元测试应该在产品代码之前编写。 如果你在产品代码之后编写测试， 就会发现写测试太难了。

**[⬆ 返回目录](#目录)**

### Single concept per test

### 每个测试单个概念

Tests should also follow the *Single Responsibility Principle*. Make only one assert per unit test.

单元测试也应当遵守 *单一职责原则* 。 让每个单元测试只包含一个断言。

**不好的：**

```ts
import { assert } from 'chai';

describe('AwesomeDate', () => {
  it('handles date boundaries', () => {
    let date: AwesomeDate;

    date = new AwesomeDate('1/1/2015');
    assert.equal('1/31/2015', date.addDays(30));

    date = new AwesomeDate('2/1/2016');
    assert.equal('2/29/2016', date.addDays(28));

    date = new AwesomeDate('2/1/2015');
    assert.equal('3/1/2015', date.addDays(28));
  });
});
```

**好的：**

```ts
import { assert } from 'chai';

describe('AwesomeDate', () => {
  it('handles 30-day months', () => {
    const date = new AwesomeDate('1/1/2015');
    assert.equal('1/31/2015', date.addDays(30));
  });

  it('handles leap year', () => {
    const date = new AwesomeDate('2/1/2016');
    assert.equal('2/29/2016', date.addDays(28));
  });

  it('handles non-leap year', () => {
    const date = new AwesomeDate('2/1/2015');
    assert.equal('3/1/2015', date.addDays(28));
  });
});
```

**[⬆ 返回目录](#目录)**

### The name of the test should reveal it's intention

### 测试的名称应当揭示它的动机

When a test fail, it's name is the first indication of what may have gone wrong.

当测试失败时， 它的名称就是错误的第一指示。

**不好的：**

```ts
describe('Calendar', () => {
  it('2/29/2020', () => {
    // ...
  });

  it('throws', () => {
    // ...
  });
});
```

**好的：**

```ts
describe('Calendar', () => {
  it('should handle leap year', () => {
    // ...
  });

  it('should throw when format is invalid', () => {
    // ...
  });
});
```

**[⬆ 返回目录](#目录)**

## Concurrency

## 并发

### Prefer promises vs callbacks

### 倾向于 Promise 而不是回调

Callbacks aren't clean, and they cause excessive amounts of nesting *(the callback hell)*.  
There are utilities that transform existing functions using the callback style to a version that returns promises
(for Node.js see [`util.promisify`](https://nodejs.org/dist/latest-v8.x/docs/api/util.html#util_util_promisify_original), for general purpose see [pify](https://www.npmjs.com/package/pify), [es6-promisify](https://www.npmjs.com/package/es6-promisify))

回调不够简洁， 因为他们会产生过多的嵌套 *（回调地狱）* 。 这些工具可以将使用回调函数转换成返回 Promise 的函数 （对于 Node.js ， 参考 [`util.promisify`](https://nodejs.org/dist/latest-v8.x/docs/api/util.html#util_util_promisify_original) ， 而对于更加通用的场景， 参考  [pify](https://www.npmjs.com/package/pify), [es6-promisify](https://www.npmjs.com/package/es6-promisify) ）。

**不好的：**

```ts
import { get } from 'request';
import { writeFile } from 'fs';

function downloadPage(url: string, saveTo: string, callback: (error: Error, content?: string) => void) {
  get(url, (error, response) => {
    if (error) {
      callback(error);
    } else {
      writeFile(saveTo, response.body, (error) => {
        if (error) {
          callback(error);
        } else {
          callback(null, response.body);
        }
      });
    }
  });
}

downloadPage('https://en.wikipedia.org/wiki/Robert_Cecil_Martin', 'article.html', (error, content) => {
  if (error) {
    console.error(error);
  } else {
    console.log(content);
  }
});
```

**好的：**

```ts
import { get } from 'request';
import { writeFile } from 'fs';
import { promisify } from 'util';

const write = promisify(writeFile);

function downloadPage(url: string, saveTo: string): Promise<string> {
  return get(url)
    .then(response => write(saveTo, response));
}

downloadPage('https://en.wikipedia.org/wiki/Robert_Cecil_Martin', 'article.html')
  .then(content => console.log(content))
  .catch(error => console.error(error));  
```

Promises supports a few helper methods that help make code more conscise:  

Promise 提供了一些帮助方法来让代码变得更加简洁：

| Pattern                  | Description                                |  
| ------------------------ | -----------------------------------------  |  
| `Promise.resolve(value)` | Convert a value into a resolved promise.   |  
| `Promise.reject(error)`  | Convert an error into a rejected promise.  |  
| `Promise.all(promises)`  |Returns a new promise which is fulfilled with an array of fulfillment values for the passed promises or rejects with the reason of the first promise that rejects. |
| `Promise.race(promises)`|Returns a new promise which is fulfilled/rejected with the result/error of the first settled promise from the array of passed promises. |

| Pattern                  | Description                                |  
| ------------------------ | -----------------------------------------  |  
| `Promise.resolve(value)` | 将一个值转换为一个已解决的 Promise 。   |  
| `Promise.reject(error)`  | 将一个错误转换为一个已拒绝的 Promise 。 |  
| `Promise.all(promises)`  | 从一组 Promise 返回一个新的 Promise ， 如果这组 Promise 全部解决， 则解决新生成的 Promise ， 否则拒绝新生成的 Promise 。 |
| `Promise.race(promises)`| 从多个 Promise 生成一个新的 Promise ， 返回值由第一个解决或者拒绝的 Promise 决定。 |

`Promise.all` is especially useful when there is a need to run tasks in parallel. `Promise.race` makes it easier to implement things like timeouts for promises.

`Promise.all` 在需要并行运行任务时非常有用， 而 `Promise.race` 则可以比较容易的实现类似超时的 Promise 。

**[⬆ 返回目录](#目录)**

### Async/Await are even cleaner than Promises

### Async/Await 比 Promise 更加简洁

With `async`/`await` syntax you can write code that is far cleaner and more understandable that chained promises. Within a function prefixed with `async` keyword you have a way to tell the JavaScript runtime to pause the execution of code on the `await` keyword (when used on a promise).

使用`async` /`await`语法，您可以编写更清晰，更易理解的链接承诺的代码。 通过在方法前面标记 `async` 关键字， 可以让 JavaScript 运行时在遇到 `async` 关键字时暂停（当使用 Promise 时才能这样做）。

**不好的：**

```ts
import { get } from 'request';
import { writeFile } from 'fs';
import { promisify } from 'util';

const write = util.promisify(writeFile);

function downloadPage(url: string, saveTo: string): Promise<string> {
  return get(url).then(response => write(saveTo, response));
}

downloadPage('https://en.wikipedia.org/wiki/Robert_Cecil_Martin', 'article.html')
  .then(content => console.log(content))
  .catch(error => console.error(error));  
```

**Good:**

```ts
import { get } from 'request';
import { writeFile } from 'fs';
import { promisify } from 'util';

const write = promisify(writeFile);

async function downloadPage(url: string, saveTo: string): Promise<string> {
  const response = await get(url);
  await write(saveTo, response);
  return response;
}

// somewhere in an async function
try {
  const content = await downloadPage('https://en.wikipedia.org/wiki/Robert_Cecil_Martin', 'article.html');
  console.log(content);
} catch (error) {
  console.error(error);
}
```

**[⬆ 返回目录](#目录)**

## Error Handling

## 错误处理

Thrown errors are a good thing! They mean the runtime has successfully identified when something in your program has gone wrong and it's letting you know by stopping function
execution on the current stack, killing the process (in Node), and notifying you in the console with a stack trace.

抛出错误是件好事！ 他们意味着当程序出错时， 成功的通知运行时， 并通过停止执行当前堆栈上的函数， 终止进程（在 Node 中）， 并且在控制台打印错误堆栈信息以通知你。

### Always use Error for throwing or rejecting

### 始终使用为抛出或拒绝使用错误对象 (Error)

JavaScript as well as TypeScript allow you to `throw` any object. A Promise can also be rejected with any reason object.  
It is advisable to use the `throw` syntax with an `Error` type. This is because your error might be caught in higher level code with a `catch` syntax.
It would be very confusing to catch a string message there and would make
[debugging more painful](https://basarat.gitbooks.io/typescript/docs/types/exceptions.html#always-use-error).  
For the same reason you should reject promises with `Error` types.

JavaScript 以及 TypeScript 允许你 `抛出` 任意对象， 一个 Promise 也能够用任意对象进行拒绝。 使用 `抛出 (throw)` 语法和 `错误 (Error)` 类型是非常明智的， 这是因为错误消息可能会被更高级的语句用 `cache` 捕获到。 而捕获一个字符串可能会非常令人疑惑的， 同时也会让[调试更加痛苦](https://basarat.gitbooks.io/typescript/docs/types/exceptions.html#always-use-error)。 同样的理由， 拒绝 Promise 时， 也应该使用 `Error` 类型。

**不好的：**

```ts
function calculateTotal(items: Item[]): number {
  throw 'Not implemented.';
}

function get(): Promise<Item[]> {
  return Promise.reject('Not implemented.');
}
```

**好的：**

```ts
function calculateTotal(items: Item[]): number {
  throw new Error('Not implemented.');
}

function get(): Promise<Item[]> {
  return Promise.reject(new Error('Not implemented.'));
}

// or equivalent to:

async function get(): Promise<Item[]> {
  throw new Error('Not implemented.');
}
```

The benefit of using `Error` types is that it is supported by the syntax `try/catch/finally` and implicitly all errors have the `stack` property which
is very powerful for debugging.  
There are also another alternatives, not to use the `throw` syntax and instead always return custom error objects. TypeScript makes this even easier.
Consider following example:

使用 `Error` 类型的好处是它被 `try/catch/finally` 支持， 并且所有的 Error 对象都有一个隐式属性 `stack` ， 在调试时很有用。 还有一个选择， 那就是不使用 `throw` 语法， 始终返回自定义的错误对象。 TypeScript 下更加容易， 参看下面的例子：

```ts
type Result<R> = { isError: false, value: R };
type Failure<E> = { isError: true, error: E };
type Failable<R, E> = Result<R> | Failure<E>;

function calculateTotal(items: Item[]): Failable<number, 'empty'> {
  if (items.length === 0) {
    return { isError: true, error: 'empty' };
  }

  // ...
  return { isError: false, value: 42 };
}
```

For the detailed explanation of this idea refer to the [original post](https://medium.com/@dhruvrajvanshi/making-exceptions-type-safe-in-typescript-c4d200ee78e9).

要查看这个主意的更详细说明， 请参考[原帖](https://medium.com/@dhruvrajvanshi/making-exceptions-type-safe-in-typescript-c4d200ee78e9)。

**[⬆ 返回目录](#目录)**

### Don't ignore caught errors

### 不要忽略捕获到的错误

Doing nothing with a caught error doesn't give you the ability to ever fix or react to said error. Logging the error to the console (`console.log`) isn't much better as often times it can get lost in a sea of things printed to the console. If you wrap any bit of code in a `try/catch` it means you think an error may occur there and therefore you should have a plan, or create a code path, for when it occurs.

捕获到错误后，什么都不做， 既不能让你修复错误， 也不能让你响应错误。 使用 `console.log` 将错误输出到控制台并不是十分高明， 因为经常会有大量的内容被打印输出到控制台， 很难再被找到。 一旦你在 `try/catch` 中包括了任何一点儿代码， 这就意味着你认为这里可能会有错误发生， 你应当针对它有一个计划， 或者一段代码来进行处理。

**不好的：**

```ts
try {
  functionThatMightThrow();
} catch (error) {
  console.log(error);
}

// or even worse
// 更糟糕的是

try {
  functionThatMightThrow();
} catch (error) {
  // ignore error
  // 完全忽略错误
}
```

**好的：**

```ts
import { logger } from './logging'

try {
  functionThatMightThrow();
} catch (error) {
  logger.log(error);
}
```

**[⬆ 返回目录](#目录)**

### Don't ignore rejected promises

### 不要忽略被拒绝的 Promise

For the same reason you shouldn't ignore caught errors from `try/catch`.

由于同样的原因， 你不应该忽略由 `try/catch` 捕获到的错误。

**不好的：**

```ts
getUser()
  .then((user: User) => {
    return sendEmail(user.email, 'Welcome!');
  })
  .catch((error) => {
    console.log(error);
  });
```

**好的：**

```ts
import { logger } from './logging'

getUser()
  .then((user: User) => {
    return sendEmail(user.email, 'Welcome!');
  })
  .catch((error) => {
    logger.log(error);
  });

// or using the async/await syntax:
// 或者使用 async/await 语法：

try {
  const user = await getUser();
  await sendEmail(user.email, 'Welcome!');
} catch (error) {
  logger.log(error);
}
```

**[⬆ 返回目录](#目录)**

## Formatting

## 格式化

Formatting is subjective. Like many rules herein, there is no hard and fast rule that you must follow. The main point is *DO NOT ARGUE* over formatting. There are tons of tools to automate this. Use one! It's a waste of time and money for engineers to argue over formatting. The general rule to follow is *keep consistent formatting rules*.  

格式化是主观的。 就像其它规则一样， 没有必须让你遵守的硬性规则。 重点是不要因为格式去争论， 有大量的工具来自动格式化， 使用其中的一个即可！ 因为做为工程师去争论格式化就是在浪费时间和金钱。 要遵守的通用规则是 *保持一致的格式化规则* 。

For TypeScript there is a powerful tool called [TSLint](https://palantir.github.io/tslint/). It's a static analysis tool that can help you improve dramatically the readability and maintainability of your code. There are ready to use TSLint configurations that you can reference in your projects:

- [TSLint Config Standard](https://www.npmjs.com/package/tslint-config-standard) - standard style rules

- [TSLint Config Airbnb](https://www.npmjs.com/package/tslint-config-airbnb) - Airbnb style guide

- [TSLint Clean Code](https://www.npmjs.com/package/tslint-clean-code) - TSLint rules inspired by the [Clean Code: A Handbook of Agile Software Craftsmanship](https://www.amazon.ca/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)

- [TSLint react](https://www.npmjs.com/package/tslint-react) - lint rules related to React & JSX

- [TSLint + Prettier](https://www.npmjs.com/package/tslint-config-prettier) - lint rules for [Prettier](https://github.com/prettier/prettier) code formatter

- [ESLint rules for TSLint](https://www.npmjs.com/package/tslint-eslint-rules) - ESLint rules for TypeScript

- [Immutable](https://www.npmjs.com/package/tslint-immutable) - rules to disable mutation in TypeScript

Refer also to this great [TypeScript StyleGuide and Coding Conventions](https://basarat.gitbooks.io/typescript/docs/styleguide/styleguide.html) source.

对 TypeScript 来说， 有一个强大的工具叫做 [TSLint](https://palantir.github.io/tslint/) 。 它是一个可以显著提高代码的可读性和可维护性的静态分析工具。 也已经有一些可用的 TSLint 配置供你在项目中参考：

- [标准的 TSLint 配置](https://www.npmjs.com/package/tslint-config-standard) - 标准风格规则

- [Airbnb 的 TSLint 配置](https://www.npmjs.com/package/tslint-config-airbnb) - Airbnb 风格指南

- [简洁代码的 TSLint 配置](https://www.npmjs.com/package/tslint-clean-code) - 受 [Clean Code: A Handbook of Agile Software Craftsmanship](https://www.amazon.ca/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) 影响的 TSLint 规则

- [React 的 TSLint 配置](https://www.npmjs.com/package/tslint-react) - React & JSX 相关的 TSLint 配置

- [TSLint + Prettier](https://www.npmjs.com/package/tslint-config-prettier) - [Prettier](https://github.com/prettier/prettier) 的代码检查规则

- [TypeScript 的 ESLint 规则](https://www.npmjs.com/package/tslint-eslint-rules) - TypeScript 的 ESLint 规则

- [Immutable](https://www.npmjs.com/package/tslint-immutable) - TypeScript 中禁止突变的规则

也请参考这个伟大的 [TypeScript 风格指南和编码约定](https://basarat.gitbooks.io/typescript/docs/styleguide/styleguide.html) 。

### 使用一致的大小写

Capitalization tells you a lot about your variables, functions, etc. These rules are subjective, so your team can choose whatever they want. The point is, no matter what you all choose, just *be consistent*.

大小写可以告诉你很多关于你的变量， 函数等等。 这些规则是主观的， 所以你的团队可以选择他们想要的任何东西。 关键是， 无论你选择什么， 只要 *保持一致* 即可。

**不好的：**

```ts
const DAYS_IN_WEEK = 7;
const daysInMonth = 30;

const songs = ['Back In Black', 'Stairway to Heaven', 'Hey Jude'];
const Artists = ['ACDC', 'Led Zeppelin', 'The Beatles'];

function eraseDatabase() {}
function restore_database() {}

type animal = { /* ... */ }
type Container = { /* ... */ }
```

**好的：**

```ts
const DAYS_IN_WEEK = 7;
const DAYS_IN_MONTH = 30;

const SONGS = ['Back In Black', 'Stairway to Heaven', 'Hey Jude'];
const ARTISTS = ['ACDC', 'Led Zeppelin', 'The Beatles'];

function eraseDatabase() {}
function restoreDatabase() {}

type Animal = { /* ... */ }
type Container = { /* ... */ }
```

Prefer using `PascalCase` for class, interface, type and namespace names.  
Prefer using `camelCase` for variables, functions and class members.

建议类、 接口、 类型和命名空间使用 `PascalCase` 风格， 变量、 函数和类成员使用 `camelCase` 风格。

**[⬆ 返回目录](#目录)**

### Function callers and callees should be close

### 函数的调用方与被调用方应该靠近

If a function calls another, keep those functions vertically close in the source file. Ideally, keep the caller right above the callee.
We tend to read code from top-to-bottom, like a newspaper. Because of this, make your code read that way.

如果一个函数调用另一个， 则在代码中这两个函数的竖直位置应该靠近。 理想情况下，保持被调用函数在被调用函数的正上方。 我们倾向于从上到下阅读代码， 就像读一章报纸。 由于这个原因， 保持你的代码可
以按照这种方式阅读。

**不好的：**

```ts
class PerformanceReview {
  constructor(private readonly employee: Employee) {
  }

  private lookupPeers() {
    return db.lookup(this.employee.id, 'peers');
  }

  private lookupManager() {
    return db.lookup(this.employee, 'manager');
  }

  private getPeerReviews() {
    const peers = this.lookupPeers();
    // ...
  }

  review() {
    this.getPeerReviews();
    this.getManagerReview();
    this.getSelfReview();

    // ...
  }

  private getManagerReview() {
    const manager = this.lookupManager();
  }

  private getSelfReview() {
    // ...
  }
}

const review = new PerformanceReview(employee);
review.review();
```

**好的：**

```ts
class PerformanceReview {
  constructor(private readonly employee: Employee) {
  }

  review() {
    this.getPeerReviews();
    this.getManagerReview();
    this.getSelfReview();

    // ...
  }

  private getPeerReviews() {
    const peers = this.lookupPeers();
    // ...
  }

  private lookupPeers() {
    return db.lookup(this.employee.id, 'peers');
  }

  private getManagerReview() {
    const manager = this.lookupManager();
  }

  private lookupManager() {
    return db.lookup(this.employee, 'manager');
  }

  private getSelfReview() {
    // ...
  }
}

const review = new PerformanceReview(employee);
review.review();
```

**[⬆ 返回目录](#目录)**

### Organize imports

### 组织导入

With clean and easy to read import statements you can quickly see the dependencies of current code. Make sure you apply following good practices for `import` statements:

- Import statements should be alphabetized and grouped.
- Unused imports should be removed.
- Named imports must be alphabetized (i.e. `import {A, B, C} from 'foo';`)
- Import sources must be alphabetized within groups, i.e.: `import * as foo from 'a'; import * as bar from 'b';`
- Groups of imports are delineated by blank lines.
- Groups must respect following order:
  - Polyfills (i.e. `import 'reflect-metadata';`)
  - Node builtin modules (i.e. `import fs from 'fs';`)
  - external modules (i.e. `import { query } from 'itiriri';`)
  - internal modules (i.e `import { UserService } from 'src/services/userService';`)
  - modules from a parent directory (i.e. `import foo from '../foo'; import qux from '../../foo/qux';`)
  - modules from the same or a sibling's directory (i.e. `import bar from './bar'; import baz from './bar/baz';`)

使用简洁易读的 import 语句， 您可以快速查看当前代码的依赖关系。 确保对 `import` 语句应用以下良好实践：

- 导入应当排序并分组；
- 未使用的导入应当删除；
- 命名导入应当排序 (比如： `import {A, B, C} from 'foo';`)
- 导入源应当在分组内排序， 比如： `import * as foo from 'a'; import * as bar from 'b';`
- 分组导入之间保留一个空行；
- 分组之间应当遵守下面的顺序：
  - 兼容性填充 (比如： `import 'reflect-metadata';`)
  - Node 内置模块 (比如： `import fs from 'fs';`)
  - 外部模块 (比如： `import { query } from 'itiriri';`)
  - 内部模块 (i.e `import { UserService } from 'src/services/userService';`)
  - 来自父目录的模块 (比如： `import foo from '../foo'; import qux from '../../foo/qux';`)
  - 来自相同目录或同级目录的模块 (比如： `import bar from './bar'; import baz from './bar/baz';`)

**不好的：**

```ts
import { TypeDefinition } from '../types/typeDefinition';
import { AttributeTypes } from '../model/attribute';
import { ApiCredentials, Adapters } from './common/api/authorization';
import fs from 'fs';
import { ConfigPlugin } from './plugins/config/configPlugin';
import { BindingScopeEnum, Container } from 'inversify';
import 'reflect-metadata';
```

**好的：**

```ts
import 'reflect-metadata';

import fs from 'fs';
import { BindingScopeEnum, Container } from 'inversify';

import { AttributeTypes } from '../model/attribute';
import { TypeDefinition } from '../types/typeDefinition';

import { ApiCredentials, Adapters } from './common/api/authorization';
import { ConfigPlugin } from './plugins/config/configPlugin';
```

**[⬆ 返回目录](#目录)**

### Use typescript aliases

### 使用 TypeScript 别名

Create prettier imports by defining the paths and baseUrl properties in the compilerOptions section in the `tsconfig.json`

This will avoid long relative paths when doing imports.

通过在 `tsconfig.json` 文件中的 compilerOptions 对象内定义路径和基础路径， 可以创建更漂亮的导入。

这将避免导入时出现太长的相对路径。

**不好的：**

```ts
import { UserService } from '../../../services/UserService';
```

**好的：**

```ts
import { UserService } from '@services/UserService';
```

```js
// tsconfig.json
...
  "compilerOptions": {
    ...
    "baseUrl": "src",
    "paths": {
      "@services": ["services/*"]
    }
    ...
  }
...
```

**[⬆ 返回目录](#目录)**

## Comments

## 注释

The use of a comments is an indication of failure to express without them. Code should be the only source of truth.
  
> Don’t comment bad code—rewrite it.  
> — *Brian W. Kernighan and P. J. Plaugher*

使用注释就意味着代码的表达失败。 代码应该是唯一的事实来源。

> 不是为烂代码添加注释， 而是重写它们。  
> - *Brian W. Kernighan 和 P. J. Plaugher*

### Prefer self explanatory code instead of comments

### 倾向于自描述的代码而不是注释

Comments are an apology, not a requirement. Good code *mostly* documents itself.

评论是代码的辩解， 不是要求。 多数情况下， 好的代码就是文档。

**不好的：**

```ts
// Check if subscription is active.
if (subscription.endDate > Date.now) {  }
```

**好的：**

```ts
const isSubscriptionActive = subscription.endDate > Date.now;
if (isSubscriptionActive) { /* ... */ }
```

**[⬆ 返回目录](#目录)**

### Don't leave commented out code in your codebase

### 不要在代码库中保存注释掉的代码

Version control exists for a reason. Leave old code in your history.

因为有版本控制， 把旧的代码留在历史记录即可

**不好的：**

```ts
type User = {
  name: string;
  email: string;
  // age: number;
  // jobPosition: string;
}
```

**好的：**

```ts
type User = {
  name: string;
  email: string;
}
```

**[⬆ 返回目录](#目录)**

### Don't have journal comments

### 不要有日志式的注释

Remember, use version control! There's no need for dead code, commented code, and especially journal comments. Use `git log` to get history!

记住， 使用版本控制！ 不需要僵尸代码， 注释掉的代码， 尤其是日志式的评论。 使用 `git log` 来
获取历史记录。

**不好的：**

```ts
/**
 * 2016-12-20: Removed monads, didn't understand them (RM)
 * 2016-10-01: Improved using special monads (JP)
 * 2016-02-03: Added type-checking (LI)
 * 2015-03-14: Implemented combine (JR)
 */
function combine(a: number, b: number): number {
  return a + b;
}
```

**好的：**

```ts
function combine(a: number, b: number): number {
  return a + b;
}
```

**[⬆ 返回目录](#目录)**

### Avoid positional markers

### 避免占位符

They usually just add noise. Let the functions and variable names along with the proper indentation and formatting give the visual structure to your code.  
Most IDE support code folding feature that allows you to collapse/expand blocks of code (see Visual Studio Code [folding regions](https://code.visualstudio.com/updates/v1_17#_folding-regions)).

它们仅仅添加了干扰。 让函数和变量名称与合适的缩进和格式化为你的代码提供视觉结构。  
绝大多数 IDE 支持代码折叠， 允许你展开/关闭代码段 （查看 Visual Studio Code [folding regions](https://code.visualstudio.com/updates/v1_17#_folding-regions) ） 。

**不好的：**

```ts
////////////////////////////////////////////////////////////////////////////////
// Client class
////////////////////////////////////////////////////////////////////////////////
class Client {
  id: number;
  name: string;
  address: Address;
  contact: Contact;

  ////////////////////////////////////////////////////////////////////////////////
  // public methods
  ////////////////////////////////////////////////////////////////////////////////
  public describe(): string {
    // ...
  }

  ////////////////////////////////////////////////////////////////////////////////
  // private methods
  ////////////////////////////////////////////////////////////////////////////////
  private describeAddress(): string {
    // ...
  }

  private describeContact(): string {
    // ...
  }
};
```

**好的：**

```ts
class Client {
  id: number;
  name: string;
  address: Address;
  contact: Contact;

  public describe(): string {
    // ...
  }

  private describeAddress(): string {
    // ...
  }

  private describeContact(): string {
    // ...
  }
};
```

**[⬆ 返回目录](#目录)**

### TODO comments

### TODO 注释

When you find yourself that you need to leave notes in the code for some later improvements,
do that using `// TODO` comments. Most IDE have special support for those kind of comments so that
you can quickly go over the entire list of todos.  

Keep in mind however that a *TODO* comment is not an excuse for bad code. 

当你发现你需要在代码中做一些后期改进是， 请使用 `// TODO` 注释。 大多数 IDE 对这种类型的注释有着特殊的支持， 你可以快速的发现全部的 TODO 列表。

记住， *TODO* 注视并不是烂代码的借口。

**不好的：**

```ts
function getActiveSubscriptions(): Promise<Subscription[]> {
  // ensure `dueDate` is indexed.
  return db.subscriptions.find({ dueDate: { $lte: new Date() } });
}
```

**好的：**

```ts
function getActiveSubscriptions(): Promise<Subscription[]> {
  // TODO: ensure `dueDate` is indexed.
  return db.subscriptions.find({ dueDate: { $lte: new Date() } });
}
```

**[⬆ 返回目录](#目录)**

## Translations

## 翻译

This is also available in other languages:
- ![br](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Brazilian Portuguese**: [vitorfreitas/clean-code-typescript](https://github.com/vitorfreitas/clean-code-typescript)

本文也有其它语言版本：

- ![br](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **巴西葡萄牙语**: [vitorfreitas/clean-code-typescript](https://github.com/vitorfreitas/clean-code-typescript)

There is work in progress for translating this to other languages:

- ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) Chinese
- ![ja](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) Japanese
- ![kr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) Korean

还有一些语言的版本也正在翻译中：

- ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) 中文
- ![ja](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) 日语
- ![kr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) 韩语

References will be added once translations are completed.  
Check this [discussion](https://github.com/labs42io/clean-code-typescript/issues/15) for more details and progress.
You can make an indispensable contribution to *Clean Code* community by translating this to your language.

一旦翻译完成， 就会在这里添加链接。 关注这个[讨论](https://github.com/labs42io/clean-code-typescript/issues/15)以获得更多的详情以及进度。 您可以通过将其翻译成您的语言，为* Clean Code *社区做出不可或缺的贡献。
