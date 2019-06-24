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

## Objects
----

* 3.1 객체 생성은 리터럴 구문을 사용합니다. eslint: `no-new-object`

```javascript
// bad
const item = new Object();

// good
const item = {};
```

* 3.2 동적인 property의 이름을 사용하여 객체를 생성하는 경우, 프로그래밍된 property 이름을 사용합니다. (computed property name)

> 해당 기능을 사용하면 한곳에서 객체의 모든 속성을 정의할 수 있습니다.

```javascript
function getKey(k) {
  return `a key named ${k}`;
}

// bad
const obj = {
  id: 5,
  name: 'San Francisco',
};
obj[getKey('enabled')] = true;

// good
const obj = {
  id: 5,
  name: 'San Francisco',
  [getKey('enabled')]: true,
};
```

* 3.3 object내 method를 사용할시에는 shorthand 법칙을 사용합니다. eslint: `object-shorthand`

```javascript
// bad
const atom = {
  value: 1,

  addValue: function (value) {
    return atom.value + value;
  },
};

// good
const atom = {
  value: 1,

  addValue(value) {
    return atom.value + value;
  },
};
```

* 3.4 object내 property를 사용시, shorthand 법칙을 따릅니다. eslint: `object-shorthand`

```javascript
const lukeSkywalker = 'Luke Skywalker';

// bad
const obj = {
  lukeSkywalker: lukeSkywalker,
};

// good
const obj = {
  lukeSkywalker,
};
```