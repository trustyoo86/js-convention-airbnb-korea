# Javascript convetion by airbnb - Korea

airbnb javascript convention을 한국어 버전으로 번역하였습니다.
개인 사용 용도로 제작되어, 일부 오역이 있을 수 있습니다.

## TOC (Table-of-contents)
1. [Types](#types)

## Types
* 1.1 *Primitives*: privitive타입을 사용하는 경우 해당 value에 직접 접근이 가능합니다.

- `string`
- `number`
- `boolean`
- `null`
- `undefined`
- `symbol`

```javascript
const foo = 1;
let bar = foo;

bar = 9;

console.log(foo, bar); // => 1, 9
```

**[⬆ back to top](##table-of-contents)**