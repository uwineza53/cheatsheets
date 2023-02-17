# Arrays
Array has a lot of native methods and using boost productivity here we are going to experience some of them.

```javascript
const arr1 = new Array(); // not advisable, better use [] notation
const arr = ['jack', 'jim', 'nina'];
arr.push('Joe', 'John');
arr.concat(...arr1);

console.log(arr);
```

Working with array function you should have paying attention, because some of them has to affect your array values and structure.

- No side effect function
With no side effect function you have to save new returned to new variables if you are about to use it later on.

```javascript
console.log(arr.join(','));
console.log(`slice() => ${arr.slice(0, 1)}`);
console.log(`unshift() => ${arr.unshift('peter')}`); // return length of new array
```

- Side effects native methods

```javascript
console.log(`splice() => ${arr.splice(4, arr.length)}`);
console.log(`Pop() => ${arr.pop()}`);
console.log(`shift() => ${arr.shift()}`);

console.log(arr);
```

## Conditional native methods

```javascript
const numbers = [1, 2, 3, 4, 5, 7, 8, 9];
//Looking for values in array
console.log(numbers.find(n => n === 0)) // returns what you're looking for else undefined
console.log(numbers.findIndex(n => n === 6)) // returns index of what you're looking for else -1
console.log(numbers.includes(4))
```

## Array manipulation functions

```javascript
console.log(numbers.every(n => n < 100)) // check if every number is less than 100
console.log(numbers.some(n => n > 7)) // check if any number is greater than 7
console.log(numbers.flat())
console.log(numbers.filter(n => n % 2 === 0))
console.log(numbers.map(n => n*2))
console.log(numbers.reduce((acc, n) => acc + n, 0))

console.log(numbers)
```

## Array iteration

```javascript
numbers.forEach((n, key) => console.log(key, n))
```

## Array Clonning

```javascript
const numbersClone = Object.assign(numbers)

numbers.push(10)
numbersClone.push(20)

console.log(numbers)
console.log(numbersClone)
```