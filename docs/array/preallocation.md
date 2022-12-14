# Preallocation

Preallocation is when you reserve memory space before using it.

This is specially useful when you know much much space you need, or you want to avoid expanding repeatedly the size of a collection over time.

## Initializing the values

If you want to preallocate an array with a initial value, you can use [`Array.from()`](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/from):

```js
const n = 5

// simple
[...Array(n).keys()] // [ 0, 1, 2, 3, 4 ]

// more powerful
Array.from({ length: n }, (value, index) => index) // [ 0, 1, 2, 3, 4 ]
```

## Reusing instances

It's typical to use an `Array` as a temporal container of data.

!> If you need to work with binary data, use a [Buffer](https://www.npmjs.com/package/buffer).

Instead of allocating a new `Array` every time, a good approach in terms of
performance is to reuse the same array instance.

To clean the elements of an `Array` the most evident approach is to use `.pop`
in a loop to remove them all.

```js
const array = [1, 2, 3, 4, 5]
while (array.length) array.pop()
console.log(array) // []
```

However, a better and simpler method is to use [`Array.prototype.length`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/length). This property is writable, and will remove all the elements if you set its value to `0`.

```js
const array = [1, 2, 3, 4, 5]
array.length = 0
console.log(array) // []
```
