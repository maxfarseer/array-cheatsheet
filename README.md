# `Array<T>`

Некоторые полезные методы для работы с массивами в JS.

Обозначения:

* ✏️ метод изменяет `this` -  изменяет/модифицирует исходный массив
* 🔒 метод не меняет `this`. - не меняет исходный массив / возвращает новый массив на базе исходного


`Array<T>.prototype.*`:

* `concat(...items: Array<T[] | T>): T[]` 🔒 <sup>ES3</sup>

    Метод возвращает новый массив, который образуется от слияния исходного массива (`this`) и массивов, переданных в метод в качестве параметров. Параметры без массива обрабатываются так, как если бы они были массивами с 1 элементом.

  ```repl
  > ['a'].concat('b', ['c', 'd'])
  [ 'a', 'b', 'c', 'd' ]
  ```

* `copyWithin(target: number, start: number, end=this.length): this` ✏️ <sup>ES6</sup>

  Copies the elements whose indices range from `start` to (excl.) `end` to indices starting with `target`. Overlapping is handled correctly.

  ```repl
  > ['a', 'b', 'c', 'd'].copyWithin(0, 2, 4)
  [ 'c', 'd', 'c', 'd' ]
  ```

* `entries(): Iterable<[number, T]>` 🔒 <sup>ES6</sup>

  Returns an iterable over [index, element] pairs.

  ```repl
  > Array.from(['a', 'b'].entries())
  [ [ 0, 'a' ], [ 1, 'b' ] ]
  ```

* `every(callback: (value: T, index: number, array: Array<T>) => boolean, thisArg?: any): boolean` 🔒 <sup>ES5</sup>

  Returns `true` if `callback` returns `true` for every element. Stops as soon as it receives `false`. Math: ∀

  ```repl
  > [1, 2, 3].every(x => x > 0)
  true
  > [1, -2, 3].every(x => x > 0)
  false
  ```

* `fill(value: T, start=0, end=this.length): this` ✏️ <sup>ES6</sup>

  Assigns `value` to every index.

  ```repl
  > [0, 1, 2].fill('a')
  [ 'a', 'a', 'a' ]
  ```

* `filter(callback: (value: T, index: number, array: Array<T>) => any, thisArg?: any): T[]` 🔒 <sup>ES5</sup>

  Returns an array with only those elements for which `callback` returns `true`.

  ```repl
  > [1, -2, 3].filter(x => x > 0)
  [ 1, 3 ]
  ```

* `find(predicate: (value: T, index: number, obj: T[]) => boolean, thisArg?: any): T | undefined` 🔒 <sup>ES6</sup>

  The result is the first element for which `predicate` returns `true`. If it never does, the result is `undefined`.

  ```repl
  > [1, -2, 3].find(x => x < 0)
  -2
  > [1, 2, 3].find(x => x < 0)
  undefined
  ```

* `findIndex(predicate: (value: T, index: number, obj: T[]) => boolean, thisArg?: any): number` 🔒 <sup>ES6</sup>

  The result is the index of the first element for which `predicate` returns `true`. If it never does, the result is `-1`.

  ```repl
  > [1, -2, 3].findIndex(x => x < 0)
  1
  > [1, 2, 3].findIndex(x => x < 0)
  -1
  ```

* `forEach(callback: (value: T, index: number, array: Array<T>) => void, thisArg?: any): void` 🔒 <sup>ES5</sup>

  Calls `callback` for each element.

  ```js
  ['a', 'b'].forEach((x, i) => console.log(x, i))
  // 'a' 0
  // 'b' 1
  ```

* `includes(searchElement: T, fromIndex=0): boolean` 🔒 <sup>ES2016</sup>

  Returns `true` if `searchElement` SameValueZero-equal to an element and `false`, otherwise. SameValueZero-equal means: strictly equal, but `NaN` is also equal to itself.

  ```repl
  > [0, 1, 2].includes(1)
  true
  > [0, 1, 2].includes(5)
  false
  ```

* `indexOf(searchElement: T, fromIndex=0): number` 🔒 <sup>ES5</sup>

  Returns the index of the first element that is strictly equal to `searchElement`. Returns `-1` if there is no such element. Starts searching at index `fromIndex`, visiting subsequent indices next.

  ```repl
  > ['a', 'b', 'a'].indexOf('a')
  0
  > ['a', 'b', 'a'].indexOf('a', 1)
  2
  > ['a', 'b', 'a'].indexOf('c')
  -1
  ```

* `join(separator = ','): string` 🔒 <sup>ES1</sup>

  Creates a string by concatenating string representations of all elements, separating by `separator`.

  ```repl
  > ['a', 'b', 'c'].join()
  'a,b,c'
  > ['a', 'b', 'c'].join('##')
  'a##b##c'
  ```

* `keys(): Iterable<number>` 🔒 <sup>ES6</sup>

  Returns an iterable over the keys of the array.

  ```repl
  > [...['a', 'b'].keys()]
  [ 0, 1 ]
  ```

* `lastIndexOf(searchElement: T, fromIndex=this.length-1): number` 🔒 <sup>ES5</sup>

  Returns the index of the last element that is strictly equal to `searchElement`. Returns `-1` if there is no such element. Starts searching at index `fromIndex`, visiting preceding indices next.

  ```repl
  > ['a', 'b', 'a'].lastIndexOf('a')
  2
  > ['a', 'b', 'a'].lastIndexOf('a', 1)
  0
  > ['a', 'b', 'a'].lastIndexOf('c')
  -1
  ```

* `map<U>(callback: (value: T, index: number, array: ReadonlyArray<T>) => U, thisArg?: any): U[]` 🔒 <sup>ES5</sup>

  Returns a new array, in which every element is the result of `callback` being applied to the corresponding element of `this`.

  ```repl
  > [1, 2, 3].map(x => x * 2)
  [ 2, 4, 6 ]
  > ['a', 'b', 'c'].map((x, i) => i)
  [ 0, 1, 2 ]
  ```

* `pop(): T | undefined` ✏️ <sup>ES3</sup>

  Removes and returns the last element of the array. That is, it treats the end of the array as a stack.

  ```repl
  > const arr = ['a', 'b', 'c'];
  > arr.pop()
  'c'
  > arr
  [ 'a', 'b' ]
  ```

* `push(...items: T[]): number` ✏️ <sup>ES3</sup>

  Adds adds zero or more `items` to the end of the array. That is, it treats the end of the array as a stack. The return value is the length of `this` after the change.

  ```repl
  > const arr = ['a', 'b'];
  > arr.push('c', 'd')
  4
  > arr
  [ 'a', 'b', 'c', 'd' ]
  ```

* `reduce<U>(callback: (state: U, element: T, index: number, array: T[]) => U, firstState?: U): U` 🔒 <sup>ES5</sup>

  The `callback` computes the next state, given the current state and an `element` of the array. `.reduce()` feeds it the array elements, starting at index 0, going forward. If no `firstState` is provided, the array element at index 0 is used, instead. The last state is the result of `.reduce()`.

  ```repl
  > [1, 2, 3].reduce((state, x) => state + String(x), '')
  '123'
  > [1, 2, 3].reduce((state, x) => state + x, 0)
  6
  ```

* `reduceRight<U>(callback: (state: U, element: T, index: number, array: T[]) => U, firstState?: U): U` 🔒 <sup>ES5</sup>

  Works like `.reduce()`, but visits the array elements backward, starting with the last element.

  ```repl
  > [1, 2, 3].reduceRight((state, x) => state + String(x), '')
  '321'
  ```

* `reverse(): this` ✏️ <sup>ES1</sup>

  Rearranges the elements of the array so that they are in reverse order and then returns `this`.

  ```repl
  > const arr = ['a', 'b', 'c'];
  > arr.reverse()
  [ 'c', 'b', 'a' ]
  > arr
  [ 'c', 'b', 'a' ]
  ```

* `shift(): T | undefined` ✏️ <sup>ES3</sup>

  Removes and returns the first element of the array. The opposite of `.unshift()`.

  ```repl
  > const arr = ['a', 'b', 'c'];
  > arr.shift()
  'a'
  > arr
  [ 'b', 'c' ]
  ```

* `slice(start=0, end=this.length): T[]` 🔒 <sup>ES3</sup>

  Returns a new array, with the elements of `this` whose indices are between (incl.) `start` and (excl.) `end`.

  ```repl
  > ['a', 'b', 'c', 'd'].slice(1, 3)
  [ 'b', 'c' ]
  > ['a', 'b'].slice() // shallow copy
  [ 'a', 'b' ]
  ```

* `some(callback: (value: T, index: number, array: Array<T>) => boolean, thisArg?: any): boolean` 🔒 <sup>ES5</sup>

  Returns `true` if `callback` returns `true` for at least one element. Stops as soon as it receives `true`. Math: ∃

  ```repl
  > [1, 2, 3].some(x => x < 0)
  false
  > [1, -2, 3].some(x => x < 0)
  true
  ```

* `sort(compareFn?: (a: T, b: T) => number): this` ✏️ <sup>ES1</sup>

  Sorts the array and returns `this`. The order in which to sort is specified via `compareFn`, which returns a number that is:

    * Negative if `a < b` (mnemonic: negative = less than zero)
    * Zero if `a === b`
    * Positive if `a > b`

  ```repl
  > [3, 1, 2].sort((a, b) => a - b)
  [ 1, 2, 3 ]
  > ['b', 'a', 'c'].sort((a, b) => a < b ? -1 : a > b ? +1 : 0)
  [ 'a', 'b', 'c' ]
  ```

* `splice(start: number, deleteCount=this.length-start, ...items: T[]): T[]` ✏️ <sup>ES3</sup>

  At index `start`, it removes `deleteCount` elements and inserts the `items`. It returns the deleted elements.

  ```repl
  > const arr = ['a', 'b', 'c', 'd'];
  > arr.splice(1, 2, 'x', 'y')
  [ 'b', 'c' ]
  > arr
  [ 'a', 'x', 'y', 'd' ]
  ```

* `toString(): string` 🔒 <sup>ES1</sup>

  Returns a string with string versions of all elements, separated by commas.

  ```repl
  > [1, 2, 3].toString()
  '1,2,3'
  > ['a', 'b', 'c'].toString()
  'a,b,c'
  > [].toString()
  ''
  ```

* `unshift(...items: T[]): number` ✏️ <sup>ES3</sup>

  Inserts the `items` at the beginning of this array and returns the length of `this` after the modification.

  ```repl
  > const arr = ['c', 'd'];
  > arr.unshift('e', 'f')
  4
  > arr
  [ 'e', 'f', 'c', 'd' ]
  ```

## More information

* Array methods of various ECMAScript versions in detail: http://exploringjs.com
* Holes and array methods: Sect. “[Array operations and holes](http://exploringjs.com/es6/ch_arrays.html#_array-operations-and-holes)” in “Exploring ES6”.

<!-- TODO: @@iterable, constructor, .length -->

## Sources

* https://github.com/Microsoft/TypeScript/blob/master/lib/lib.es6.d.ts
* MDN
* ECMAScript spec
