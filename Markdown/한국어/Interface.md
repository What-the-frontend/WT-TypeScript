Interface
===
TypeScript의 핵심법칙중 하나는 값이 가지고 있는 모양(형태)에 기반하여 타입체킹을 한다는 점이다. 이는 종종 "duck typing" 또는 "structural subtyping" 이라고 불린다. 타입스크립트에서는, 인터페이스는 이러한 타입의 이름을 지정하는 역할을 담당하며, 코드 외부에서 코드를 사용하여 조건을 정의하는 강력한 방법이다.

Our First Interface
---
인터페이스의 작동 방식을 보는 가장 쉬운 방법은 간단한 예제로 시작하는 것이다.
```typescript
function printLabel(labelledObj: { label: string }) {
  console.log(labelledObj.label);
}

let myObj = { size: 10, label: "Size 10 Object" };
printLabel(myObj);
```
type-checker는 `printLabel` 를 호출하기 위해서 타입을 체크한다. `printLabel` 함수는 스트링 타입의 `label` 프로퍼티를 가진 객체를 파라미터 하나를 전달받는다. 사실 우리가 넘겨준 객체는 이것보다 더 많은 프로퍼티들을 갖고있지만, 컴파일러는 단지 적어도 필요한 것들이 존재하고, 필요한 타입과 일치하는지만을 확인한다. 하지만, TypeScript가 관대하지 않은 몇몇 경우가 존재한다.

이번엔 문자열의 `label` 프로퍼티를 필요로한다는걸 명시해놓은 인터페이스를 사용하는 방법으로 같은 예제코드를 작성할 수 있다.
```typescript
interface LabelledValue {
  label: string;
}

function printLabel(labelledObj: LabelledValue) {
  console.log(labelledObj.label);
}

let myObj = { size: 10, label: "Size 10 Object" };
printLabel(myObj);
```
`LabelledValue` 인터페이스 이전 예제의 요구사항(parameter)을 설명하는데 사용할 수 있는 이름이다. 이는 여전히 문자열 타입의 `label` 프로퍼티를 나타내며, 명시적으로 `printLabel` 함수에서 인터페이스를 구현하겠다고 다른 언어(Java)와 달리 명시적으로 나타낼 필요가 없었다. TypeScript에서의 인터페이스는 단순히 형태에 불과하며, 객체가 나열한 요구사항을 충족하면 됩니다.

type-checker가 순서에 맞게 정렬될 필요없이, 단지 인터페이스에서 요구한 해당 프로퍼티가 제공되고 요구한 타입이 있는지 충족하기만 된다는 점을 지적해야한다.

Optional Properties
---
인터페이스의 모든 프로퍼티가 제공되어야만 하는건 아닐것이다. 일부 조건하에 존재하거나, 전혀 없을수도 있다. Optional Properties는 오직 한쌍의 프로퍼티를 전달받는 함수에 전달하는 객체에서 "option bags" 와 같은 패턴을 만들때 많이 사용된다.

이 패턴에 대한 예제이다.
```typescript
interface SquareConfig {
  color?: string,
  width?: number
}

function createSquare(config: SquareConfig): { color: string; area: number } {
  let newSquare = { color: "white", area: 100 };
  if (config.color)
    newSquare.color = config.color;
  if (config.width)
    newSquare.area = config.width * config.width;
  return newSquare;
}

let mySquare = createSquare({ color: "black" });
```
optional properties를 가진 인터페이스도 선언내부의 각각의 optional property가 프로퍼티 이름의 마지막에 `?` 표시가 된채로 다른 인터페이스와 비슷하게 작성된다.

optional properties의 장점은 여전히 사용가능한 프로퍼티를 나타낼 수 있지만, 인터페이스의 일부가 아닌 프로퍼티의 사용을 방지할 수 있다는 것이다. 예를 들어서, `createSquare` 안에 `color` 라는 이름의 프로퍼티의 타입을 정해주지 않으면, 에러를 발생시킨다.
```typescript
interface SquareConfig {
  color?: string;
  width?: number;
}

function createSquare(config: SquareConfig): { color: string; area: number } {
  let newSquare = { color: "white", area: 100 };
  if (config.clor)
    // Error: Property 'color' does not exist on type 'SquareConfig'
    newSquare.color = config.clor;
  if (config.width)
    newSquare.area = config.width * config.width;
  return newSquare;
}

let mySquare = createSquare({ color: "black" });
```