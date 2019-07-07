# Javascript convetion by airbnb - Korea

[airbnb javascript convention](https://github.com/airbnb/javascript)을 한국어 버전으로 번역하였습니다.
개인 사용 용도로 제작되어, 일부 오역이 있을 수 있습니다.

## TOC (Table-of-contents)
1. [Types](#types)
1. [Refrences](#references)
1. [Objects](#objects)
1. [Arrays](#arrays)

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

* 3.5 Object 선언 시작부분에 shorthand 내용을 적용합니다.
> 이유: shorthand를 적용한 property에 대한 가독성을 높일 수 있습니다.

```javascript
const anakinSkywalker = 'Anakin Skywalker';
const lukeSkywalker = 'Luke Skywalker';

// bad
const obj = {
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  lukeSkywalker,
  episodeThree: 3,
  mayTheFourth: 4,
  anakinSkywalker,
};

// good
const obj = {
  lukeSkywalker,
  anakinSkywalker,
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  episodeThree: 3,
  mayTheFourth: 4,
};
```

* 3.6 유효하지 않은 property 내용에 경우에만 quote (')를 사용합니다. eslint: `quote-props`
> 이유: js엔진 최적화 및 가독성을 높일 수 있습니다.

```javascript
// bad
const bad = {
  'foo': 3,
  'bar': 4,
  'data-blah': 5,
};

// good
const good = {
  foo: 3,
  bar: 4,
  'data-blah': 5,
};
```

* 3.7 `Object.prototype` 메소드를 직접 사용하지 않습니다. - call, apply등을 통해서 사용합니다. (예를 들면 `hasOwnProperty`, `propertyIsEnumerable`, `isPrototypeOf` 등) eslint: `no-prototype-builtins`
> 이유: 위와같은 Object.prototype등의 메소드는 속성에따라 무시될 수 있습니다. 예를들면, `{hasOwnProperty: false}` 혹은 null객체가 될 수 있습니다. `(Object.create(null))`

```javascript
// bad
console.log(object.hasOwnProperty(key));

// good
console.log(Object.prototype.hasOwnProperty.call(object, key));

// best
const has = Object.prototype.hasOwnProperty; // cache the lookup once, in module scope.
/* or */
import has from 'has'; // https://www.npmjs.com/package/has
// ...
console.log(has.call(object, key));
```

* 3.8 얕은 객체 복사에 대해서는 `Object.assign` 보다 Object내 spread를 사용합니다. 객체내 정의되지 않은 새 개체를 추출할 경우 rest operator를 사용합니다.

```javascript
// very bad
const original = { a: 1, b: 2 };
const copy = Object.assign(original, { c: 3 }); // this mutates `original` ಠ_ಠ
delete copy.a; // so does this

// bad
const original = { a: 1, b: 2 };
const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

// good
const original = { a: 1, b: 2 };
const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
```

**[⬆ back to top](##table-of-contents)**

## Arrays

* 4.1 Array생성은 리터럴 구문을 사용합니다. eslint: `no-array-constructor`

```javascript
// bad
const items = new Array();

// good
const items = [];
```

* 4.2 Array내 아이템 삽입시 `Array.push`를 사용합니다.

```javascript
const someStack = [];

// bad
someStack[someStack.length] = 'abracadabra';

// good
someStack.push('abracadabra');
```

* 4.3 Array를 복사하기 위해서 spread구문 `...`을 사용합니다.

```javascript
// bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i += 1) {
  itemsCopy[i] = items[i];
}

// good
const itemsCopy = [...items];
```

* 4.4 반복가능한(iterable) object를 array로 변환하기 위해서 spread구문 `...`을 `Array.from` 대신 사용합니다.

```javascript
const foo = document.querySelectorAll('.foo');

// good
const nodes = Array.from(foo);

// best
const nodes = [...foo];
```

* 4.5 Array와 유사한 object 사용시에는 `array.from`을 사용합니다.

```javascript
const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };

// bad
const arr = Array.prototype.slice.call(arrLike);

// good
const arr = Array.from(arrLike);
```