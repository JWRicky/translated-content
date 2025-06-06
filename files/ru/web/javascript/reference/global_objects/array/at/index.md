---
title: Array.prototype.at()
slug: Web/JavaScript/Reference/Global_Objects/Array/at
---

{{JSRef}}

Метод **`at()`** принимает значение в виде целого числа и возвращает элемент массива с данным индексом. В качестве аргумента метод принимает положительные и отрицательные числа. При отрицательном значении отсчёт происходит с конца массива.

{{InteractiveExample("JavaScript Demo: Array.at()")}}

```js interactive-example
const array1 = [5, 12, 8, 130, 44];

let index = 2;

console.log(`An index of ${index} returns ${array1.at(index)}`);
// Expected output: "An index of 2 returns 8"

index = -2;

console.log(`An index of ${index} returns ${array1.at(index)}`);
// Expected output: "An index of -2 returns 130"
```

## Синтаксис

```js-nolint
at(index)
```

### Параметры

- `index`
  - : Индекс (позиция) элемента возвращаемого элемента массива. При передаче отрицательного индекса применяется относительная индексация с конца массива; например, при использовании отрицательного числа, возвращаемый элемент находится путём обратного отсчёта с конца массива.

### Возвращаемое значение

Элемент массива, соответствующий переданному индексу. Если переданный индекс не может быть найден, возвращает {{jsxref('undefined')}}.

## Описание

Метод `at()` является эквивиалентом получения элементов массива с помощью квадратных скобок с использованием неотрицательного индекса. Например, `array[0]` и `array.at(0)` оба вернут первый элемент. Однако, при вычислении значения с конца массива, нельзя использовать `array[-1]` как в Python или R, потому что все значения внутри квадратных скобок трактуются буквально как строковые свойства. Из-за этого попытка обращения к -1 элементу будет прочитана как `array["-1"]`, что является нормальным строковым значением, а не индексом массива.

Обычной практикой является получении числа элементов массива {{jsxref("Array/length", "length")}} и последующее вычисление значения индекса — например, `array[array.length - 1]`. Метод `at()` разрешает относительную индексацию, поэтому может быть сокращено до `array.at(-1)`.

Метод `at()` — это [generic](/ru/docs/Web/JavaScript/Reference/Global_Objects/Array#generic_array_methods). Он ожидает только, что значение `this` будет иметь свойство `length` и свойства с числовыми ключом.

## Примеры

### Возврат последнего элемента массива

В следующем примере представлена функция, которая возвращает последний элемент переданного массива

```js
// Массив со значениями
const cart = ["apple", "banana", "pear"];

// Функция, которая возвращает последний элемент переданного массива
function returnLast(arr) {
  return arr.at(-1);
}

// Получить последний элемент нашего массива 'cart'
const item1 = returnLast(cart);
console.log(item1); // Выведет: 'pear'

// Добавить элемент в наш массив 'cart'
cart.push("orange");
const item2 = returnLast(cart);
console.log(item2); // Выведет: 'orange'
```

### Сравнение методов

В этом примере сравниваются разные способы выбора предпоследнего элемента {{jsxref('Array', 'массива')}}. Хотя все приведённые ниже способы являются допустимыми, наиболее кратким и наглядным является использование метода `at()`.

```js
// Наш массив с элементами
const colors = ["red", "green", "blue"];

// Использование свойства 'length'
const lengthWay = colors[colors.length - 2];
console.log(lengthWay); // Выведет: 'green'

// Использование метода slice(). Обратите внимание, что возвращается массив
const sliceWay = colors.slice(-2, -1);
console.log(sliceWay[0]); // Выведет: 'green'

// Использование метода at()
const atWay = colors.at(-2);
console.log(atWay); // Выведет: 'green'
```

### Вызов at() в массивоподобных объектах

Метод `at()` считывает свойство `length` для значения `this` и вычисляет индекс для обращения.

```js
const arrayLike = {
  length: 2,
  0: "a",
  1: "b",
};
console.log(Array.prototype.at.call(arrayLike, -1)); // "b"
```

## Спецификации

{{Specifications}}

## Совместимость с браузерами

{{Compat}}

## Смотрите также

- Полифил `Array.prototype.at` в библиотеке [`core-js`](https://github.com/zloirock/core-js#relative-indexing-method)
- [Полифил для метода at()](https://github.com/tc39/proposal-relative-indexing-method#polyfill).
- {{jsxref("Array.prototype.find()")}} – возвращает значение на основании проверки.
- {{jsxref("Array.prototype.includes()")}} – проверяет наличие значения в массиве.
- {{jsxref("Array.prototype.indexOf()")}} – возвращает индекс переданного элемента.
