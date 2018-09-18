Destructuring
===
객체나 배열의 멤버에 접근할때 유용한 방식이다. ES2015부터 지원되는 문법이다. 우선 객체의 경우 어떻게 사용되는지 설명하도록 하겠다.

객체 비구조화 할당
---
```javascript
const foo = {
  name: 'bar',
  say: 'Hello World'
}
const fooName = foo.name;
const fooSay = foo.say;
```
이렇게 단순히 객체의 속성을 각각 변수에 할당해줘야하는 경우에 귀찮다. 만약 위의 코드와 달리 변수에 값을 할당할때, 객체의 속성을 일일이 검사하거나, 초기화를 시켜줘야하는 경우에 얼마나 더 귀찮겠는가. 무엇보다도 코드가 더러워진다.
```javascript
const foo = {
  name: 'bar',
  say: 'Hello World'
}
const { name: fooName, say: fooSay } = foo;
```
반면에 Object destructuring 방법을 사용하면 얼마나 깔끔하고 단순한가. 예제는 단순히 할당에 불과했지만, 다른 작업들도 수행가능하다.

1. 변수값 초기할당

    ```javascript
    const foo = { name: '' }
    const { name = 'bar', say = 'Hello World' } = foo;
    ```
2. 매개변수

    ```javascript
    const foo = { name: 'bar', say: 'Hello World' };
    
    function test({ name, say }) {
      console.log(`foo's name is ${name}. and he say, "${say}"`);
    }
    ```

타입스크립트에서는 위의 문법을 사용하기위해서 `type` (or `interface`) 키워드를 사용한다.
```typescript
type Foo = {
  name: string,
  say: string
};
const { name, say } = ({ name: 'bar', say: 'Hello World' }: Foo);
```

배열 비구조화 할당
---
배열 또한 비구조화 할당이 가능하다. 객체는 Key값을 기준으로 Value를 할당했다고 한다면, 배열은 인덱스, 즉 순서를 통해서 할당한다.
```javascript
const arr = [1, 2, 3];
const one = arr[0];
const two = arr[1];
const three = arr[3];
```
일반적으로 우리가 사용하던 할당 방법이다. 하지만 이는 위와 같은 이유를 갖는다(귀찮고, 깔끔하지않다).
```javascript
const [one, two, three] = arr;
// one = 1, two = 2, three = 3
```
정말 단순하다. 변수선언 키워드 뒤에 대괄호로 할당될 변수들을 인덱스 순서대로 나열해놓으면 된다. 에를 들어서 다음과 같은 상황에서도 사용할 수 있다.
```javascript
const birth = '2000/04/29';
const [birthYear, birthMonth, birthDay] = birth.split('/');
// birthYear = 2000, birthMonth = 04, birthDay = 29
```
이를 타입스크립트에서 사용할땐, 객체 비구조화 할당과 같다.
```typescript
type Num = [number, number, number];
const [one, two, three]: Num = [1, 2, 3];
```