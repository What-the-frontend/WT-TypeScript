Why TypeScript?
===
JavaScript is a loosely typed or a dynamic language. So, It doesn't have clear type system like C, C# and Java.
For example, When we declare variables in JavaScript, We use `var` keyword.(also `let` and `const` too.)
```javascript
var name = 'geni';    // string
var age = 19;   // number
var isEngineer = true;    // boolean
var address = {
  zipCode: 12345,
  detail: 'Seoul, Korea'
}   // object
var scores = ['high-school', 3, { english: 80 }, { math: 90 }];   // Array
var birth = new Date(2000, 3, 29);    // Date
var sayHello = function() {
  return 'Hello!';
}   // Function
```
There are so many case to declare variables. But, It has some problems.

1. Cannot catch type error at compile level.
2. Lower code readabilty.

TypeScript resolve this problem. It makes JavaScript, dynamic to static.
```typescript
var name: string = 'geni';
var age: number = 19;
var isEngineer: boolean = true;

interface addressObj {
  zipCode: number,
  detail: string
}

// implements interface
var address: addressObj = {
  zipCode: 12345,
  detail: 'Seoul, Korea'
}

var scores: any = ['high-school', 3, { english: 80 }, { math: 90 }];
var birth: Date = new Date(2000, 3, 29);
var sayHello = function(): string {
  return 'Hello!';
}
```