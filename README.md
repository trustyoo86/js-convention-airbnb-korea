# Javascript convetion by airbnb - Korea

[airbnb javascript convention](https://github.com/airbnb/javascript)을 한국어 버전으로 번역하였습니다.
개인 사용 용도로 제작되어, 일부 오역이 있을 수 있습니다.

## TOC (Table-of-contents)
1. [Types](#types)
1. [Refrences](#references)

## Types
----
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

1.2 *Complex*: `Array`, `object`등의 유형에 엑세스할때 값에 대한 참조를 사용하도록 합니다.

- `object`
- `array`
- `function`

```javascript
const foo = [1, 2];
const bar = foo;

bar[0] = 9;

console.log(foo[0], bar[0]); // => 9, 9
```

**[⬆ back to top](##table-of-contents)**

## References
----
* 2.1 `var` 대신 모든 참조값은 `const`를 사용합니다. eslint: `prefer-const`, `no-const-assign`

> Why? const로 할당시 참조를 다시 할당할 수 없으므로, 버그 발생에 대한 캐치가 쉽습니다.

```javascript
// bad
var a = 1;
var b = 2;

// good
const a = 1;
const b = 2;
```

* 2.2 재할당 해야하는 참조값의 경우 `var` 대신 `let`을 사용합니다. eslint: `no-var`

> Why? `let`은 `block-scoped variable` 입니다. 이는 `function-scoped`를 가지고 있는 `var` 함수보다 변수 파악 및 오류를 줄일 수 있습니다.

```javascript
// bad
var count = 1;
if (true) {
  count += 1;
}

// good, use the let.
let count = 1;
if (true) {
  count += 1;
}
```

* 2.3 `let`과 `const`는 `block-scoped` 즉 block 기반의 변수임을 확인하세요.

```javascript
{
  let a = 1;
  const b = 1;
}

console.log(a); // ReferenceError
console.log(b); // ReferenceError
```

**[⬆ back to top](##table-of-contents)**