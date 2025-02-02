# Iterator Drill: Reduce

## Learning Goals

* Define how the `reduce()` method works
* Demonstrate `reduce()`
* Use `reduce()` to create a single aggregate of all items in a list

## Introduction

In the world of programming, we often work with lists. Sometimes we want to
transform elements in that list to another value — but other times, we want to
**aggregate** a result. In other words, we want to _reduce_ a list to a single
value — it could be, for example, a string, a number, a boolean. For example,
our friend has a driver's license and a vehicle, but is very bad at keeping an
eye on the parking meter. They've got dozens of parking tickets with fees.
Wouldn't it be great if we could _reduce_ all of those parking fees to a _single_
total value? 

## Define How the `reduce()` Method Works

To illustrate how `reduce()` works, we'll make up some store data, we're interested in
getting a total price of all products in our basket. The store data looks like this:

```js
const products = [
  { name: 'Shampoo', price: 4.99 },
  { name: 'Donuts', price: 7.99 },
  { name: 'Cookies', price: 6.49 },
  { name: 'Bath Gel', price: 13.99 }
];
```

We're going to reduce the array of products to a _single value_— in this case the total
price of all products in the basket. Let's create a function that has an initial value,
then iterates the given products and adds their price to the total price. When the loop
has finished, we return our `totalPrice` result:

```js
function getTotalAmountForProducts(products) {
  let totalPrice = 0;

  products.forEach(product => {
    totalPrice += product.price;
  });

  return totalPrice;
}

console.log(getTotalAmountForProducts(products)); // prints 33.46
```

This is a very basic way to manually add together the prices of the products we want to buy. 

To abstract this further, let's count the number of coupons we have lying around the house:

```js
const couponLocations = [
  { room: 'Living room', amount: 5 },
  { room: 'Kitchen', amount: 2 },
  { room: 'Bathroom', amount: 1 },
  { room: 'Master bedroom', amount: 7 }
];

function couponCounter(totalAmount, location) {
  return totalAmount + location.amount;
}

console.log(reduce(couponLocations, couponCounter, 0)); // prints 15
```

What if we already have three coupons in our hand? We can easily account for that by adjusting
the initial value:

```js
console.log(reduce(couponLocations, couponCounter, 3)); // prints 18
```

## Demonstrate `reduce`

With JavaScript’s `reduce()` method, we don't need to write out all that code. The `reduce()` method
is when we want to get something useful out of each element in the collection and gather that
information into a final summary object or value. Let's take the native implementation with our
previous example for a spin:

```js
console.log(couponLocations.reduce(couponCounter, 0)); // also prints 15!
```

Another simple numerical example:

```js
let doubledAndSummed = [1, 2, 3].reduce( (total, element) => element * 2 + total, 0)
// => 12
```

Here, for each element, JavaScript passes it and the running total (initialized
to 0, in the second argument to `reduce()`) into the function. The function
multiplies the element by `2` and adds that to the current total.

That sum (`2 * element + total`) is the return value of the function and
becomes the new `total` for the next iteration. When there's nothing left to
iterate, the total is returned.

The initialization value can be left out but it might lead to a real surprise.
If _no_ initial value is supplied, the first element is used _without having
been used in the function_:

```js
let doubledAndSummed = [1, 2, 3].reduce( (total, element) => element * 2 + total)
// => 11
```

The initialization value can be changed:

```js
let doubledAndSummedFromTen = [1, 2, 3].reduce( (total, element) => element * 2 + total, 10)
// => 22
```

For more powerful uses, we could use:

```js

let hogwarts_houses = {
  "Slytherin": [],
  "Gryffindor": [],
  "Hufflepuff": [],
  "Ravenclaw": []
}

/*

Assume sorting_hat.assign() returns a String ("Slytherin", "Gryffindor",
"Hufflepuff", "Ravenclaw") based on the argument passed in.

*/

incoming_students.reduce( (houses, student) => houses[sorting_hat.assign(student)].push(student) , hogwarts_houses)
```

Here we iterate a collection of students and assign each one to a pre-existing
accumulator `Object`. We ask the `Object` to look up an `Array` keyed by the
name of the houses. We then `push()` the student into that `Array`. Later in
the code:

```js
hogwarts_houses["Gryffindor"] //=> [hermioneGranger, ronWeasley, harryPotter]
```

## Use `reduce()` to Create a Single Aggregate of All Items in a List.

Let's say we are hard at work in the battery factory. We've assembled several
batches of batteries today. Let's count how many assembled batteries we ended
up with.

* Create a new variable called `totalBatteries` which is the sum of all of the
battery amounts in the `batteryBatches` array. Naturally, use `reduce()` for this!

## Conclusion

With `reduce()`, like many other enumerators in the JavaScript library, we are able
to quickly get a minimized list or a total sum from a set of values, including values
that we might have filtered out of a list. With this, we can greatly cut down the
amount of time spent recreating common functionality, or building out helper methods
for commonly used functionality from scratch.

## Resources

* [MDN: Array.prototype.reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
