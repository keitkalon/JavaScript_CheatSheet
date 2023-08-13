# JavaScript Functional Programming

Functions Insectarium

## FETCHING 
----------------------
[!NOTE]
Get Create Update Delete by  fetching

```javascript
const buttons = document.querySelectorAll("button");
const output = document.querySelector("#result");

buttons.forEach((button) => button.addEventListener("click", processButton));

const api = {
    post: async function (url, payload) {
        const req = await fetch(url, {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(payload),
        });
        if (req.ok) {
            const res = await req.json();
            return res.result;
        }
    },
    put: async function (url, payload) {
        const req = await fetch(url, {
            method: "PUT",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(payload),
        });
        if (req.ok) {
            const res = await req.json();
            return res.result;
        }
    },
    delete: async function (url, payload) {
        const req = await fetch(url, {
            method: "DELETE",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(payload),
        });
        if (req.ok) {
            const res = await req.json();
            return res.result;
        }
    },
};

async function processButton(e) {
    e.preventDefault();

    const func = e.target.dataset.function;
    const val = e.target.dataset.id;
    let message = "";

    if (func === "add") {
        message = await api.post("/add", { item: val });
    }
    if (func === "edit") {
        message = await api.put("/edit", { item: val });
    }
    if (func === "delete") {
        message = await api.delete("/delete", { item: val });
    }

    output.innerText = message;
}
```

## FETCHING data and then use it in DOM
----------------------
[!NOTE]
fetch data from an end point and display it on a table

```javascript
const getActorApi = async function(year){
   try{
      const req = await fetch(`/actor-from-year/${year}`, {
          method: "GET",
          headers: {"Content-Type": "application/json"}
      });
      if(req.ok) {
          const res =await res.json();
          return res
      }
   }catch(err){
      console.error(err)
   }
}

async function loadActors(year){
    const actors = await getActorsApi(year)
    const lines = document.querySelectorAll("td")
    lines.forEach(line, index) => {
        if(actors[index].actor_age - actors[index].show_year > actors[index].show_year){
            line.style.backgroundColor = "yellow";        
        }
    }
}

document.querylector("#input_year").addEventListener("change", () => {
    document.location.href = `/actors-from-year/${document.querySelector("#input_year").value}`
})
loadActors(document.querySelector("table").id)
```

## CallBack
----------------------
[!NOTE]
Callbacks is when you return a call of a function that previously was received as parameter. They are commonly used in event handling, asynchronous operations, array methods like map, filter, and reduce, and anywhere you want to inject custom behavior into a function or method. 

```javascript
// Callback function definition
function raiseToPowerOf3UsingCallback(number, callback) {
    return callback(number) * number;
}

// Function used as a callback
function raiseAtPowerOf2(number) {
    return number * number;
}

// Using the functions
console.log(raiseToPowerOf3UsingCallback(5, raiseAtPowerOf2));  // Expected Output: 125, which is 5^3
}
```

## Closure Callback
------------------------
[!NOTE]
Closures can lead to unintended memory leaks if not used carefully. Since they retain access to their outer function's scope, they might keep references to objects longer than necessary, preventing those objects from being garbage collected.
```javascript
// Closure Callback function definition
function raiseToPowerOf3UsingClosure(number) {
    // Closure: Inner function that accesses the outer function's variables
    function raiseAtPowerOf2(num) {
        return num * num;
    }

    return raiseAtPowerOf2(number) * number;
}

// Using the function with a closure
console.log(raiseToPowerOf3UsingClosure(5));  // Expected Output: 125, which is 5^3
}
```

## Closure Memoization
------------------------
[!NOTE]
Memoization is an optimization technique where you cache the results of expensive function calls and return the cached result when the same inputs occur again. Increase memory usage to save computation usage.
```javascript
// Closure Memoization function definition
function memoizeRaiseToPowerOf3() {
    let memo = {};

    function raiseAtPowerOf2(num) {
        return num * num;
    }

    return function(number) {
        if (memo[number] !== undefined) {
            console.log('Fetching from cache:', number);
            return memo[number];
        }

        console.log('Calculating result for:', number);
        let result = raiseAtPowerOf2(number) * number;
        memo[number] = result;
        return result;
    };
}

const memoizedPowerOf3 = memoizeRaiseToPowerOf3();

console.log(memoizedPowerOf3(5));  // Expected Output: 125, which is 5^3, logs "Calculating result for: 5"
console.log(memoizedPowerOf3(5));  // Expected Output: 125, fetches from cache, logs "Fetching from cache: 5"
console.log(memoizedPowerOf3(6));  // Expected Output: 216, which is 6^3, logs "Calculating result for: 6"
```

## Predicate
------------------------
[!NOTE]
A function that return a boolean
```javascript
// Predicate function to check if a number is even
function isEven(number) {
    return number % 2 === 0;
}

const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const evenNumbers = numbers.filter(isEven);

console.log(evenNumbers); // Expected Output: [2, 4, 6, 8, 10]
```

## Filter
------------------------
[!NOTE]
A high order function that use a predicate as a callback
```javascript
const physicists = [
    { name: 'Max Planck', yearOfBirth: 1858, contribution: 'Quantum Theory' },
    { name: 'Niels Bohr', yearOfBirth: 1885, contribution: 'Atomic Model' },
    { name: 'Albert Einstein', yearOfBirth: 1879, contribution: 'Photoelectric Effect' },
    { name: 'Erwin Schrödinger', yearOfBirth: 1887, contribution: 'Wave Mechanics' },
    { name: 'Werner Heisenberg', yearOfBirth: 1901, contribution: 'Matrix Mechanics' },
    { name: 'Richard Feynman', yearOfBirth: 1918, contribution: 'Quantum Electrodynamics' }
];

function filterPhysicistsAfterYear(physicists, year) {
    return physicists.filter(physicist => physicist.yearOfBirth > year);
}

const physicistsBornAfter1900 = filterPhysicistsAfterYear(physicists, 1900);
console.log(physicistsBornAfter1900);

/* Expected Output:
[
    { name: 'Werner Heisenberg', yearOfBirth: 1901, contribution: 'Matrix Mechanics' },
    { name: 'Richard Feynman', yearOfBirth: 1918, contribution: 'Quantum Electrodynamics' }
]
*/
```

## Sort
------------------------
[!NOTE]
A high order function that use a function that returns 1 or -1 as a callback
```javascript
const fruits = [
    { name: 'apple', color: 'red', weight: 150 },
    { name: 'orange', color: 'orange', weight: 200 },
    { name: 'banana', color: 'yellow', weight: 120 },
    { name: 'grape', color: 'purple', weight: 5 },
    { name: 'cherry', color: 'red', weight: 5 },
    { name: 'watermelon', color: 'green', weight: 2000 }
];

fruits.sort((a, b) => {
    // Primary sorting by color
    if (a.color < b.color) return -1;
    if (a.color > b.color) return 1;

    // Secondary sorting by weight (in descending order)
    return b.weight - a.weight;
});

console.log(fruits);
/* Expected Output:
[
    { name: 'apple', color: 'red', weight: 150 },
    { name: 'cherry', color: 'red', weight: 5 },
    { name: 'watermelon', color: 'green', weight: 2000 },
    { name: 'grape', color: 'purple', weight: 5 },
    { name: 'orange', color: 'orange', weight: 200 },
    { name: 'banana', color: 'yellow', weight: 120 }
]
*/
```
the same sort method but with physicists
```javascript
const physicists = [
    { name: 'Max Planck', yearOfBirth: 1858, contribution: 'Quantum Theory' },
    { name: 'Niels Bohr', yearOfBirth: 1885, contribution: 'Atomic Model' },
    { name: 'Albert Einstein', yearOfBirth: 1879, contribution: 'Photoelectric Effect' },
    { name: 'Erwin Schrödinger', yearOfBirth: 1887, contribution: 'Wave Mechanics' },
    { name: 'Werner Heisenberg', yearOfBirth: 1901, contribution: 'Matrix Mechanics' },
    { name: 'Richard Feynman', yearOfBirth: 1918, contribution: 'Quantum Electrodynamics' }
];

function centuryOfBirth(year) {
    return Math.ceil(year / 100);
}

physicists.sort((a, b) => {
    const centuryA = centuryOfBirth(a.yearOfBirth);
    const centuryB = centuryOfBirth(b.yearOfBirth);

    if (centuryA !== centuryB) {
        return centuryA - centuryB;  // Sort by century of birth
    } else {
        return a.name.localeCompare(b.name);  // Sort by name if from the same century
    }
});

console.log(physicists);
/* Expected Output:
[
    { name: 'Albert Einstein', yearOfBirth: 1879, contribution: 'Photoelectric Effect' },
    { name: 'Max Planck', yearOfBirth: 1858, contribution: 'Quantum Theory' },
    { name: 'Niels Bohr', yearOfBirth: 1885, contribution: 'Atomic Model' },
    { name: 'Erwin Schrödinger', yearOfBirth: 1887, contribution: 'Wave Mechanics' },
    { name: 'Richard Feynman', yearOfBirth: 1918, contribution: 'Quantum Electrodynamics' },
    { name: 'Werner Heisenberg', yearOfBirth: 1901, contribution: 'Matrix Mechanics' }
]
*/
```

## Map
------------------------
[!NOTE]
A high order method that renurn a new array taht have tranforming computations on each member of the old array
```javascript
const physicists = [
    { name: 'Max Planck', yearOfBirth: 1858, contribution: 'Quantum Theory' },
    { name: 'Niels Bohr', yearOfBirth: 1885, contribution: 'Atomic Model' },
    { name: 'Albert Einstein', yearOfBirth: 1879, contribution: 'Photoelectric Effect' },
    { name: 'Erwin Schrödinger', yearOfBirth: 1887, contribution: 'Wave Mechanics' },
    { name: 'Werner Heisenberg', yearOfBirth: 1901, contribution: 'Matrix Mechanics' },
    { name: 'Richard Feynman', yearOfBirth: 1918, contribution: 'Quantum Electrodynamics' }
];

const currentYear = 2023;

const transformedPhysicists = physicists.map(physicist => {
    const yearsSince20 = currentYear - (physicist.yearOfBirth + 20);
    return {
        ...physicist,
        yearsSinceHis20: yearsSince20
    };
});

console.log(transformedPhysicists);

/*
Expected Result:
[
    { name: 'Max Planck', yearOfBirth: 1858, contribution: 'Quantum Theory', yearsSinceHis20: 145 },
    { name: 'Niels Bohr', yearOfBirth: 1885, contribution: 'Atomic Model', yearsSinceHis20: 118 },
    { name: 'Albert Einstein', yearOfBirth: 1879, contribution: 'Photoelectric Effect', yearsSinceHis20: 124 },
    { name: 'Erwin Schrödinger', yearOfBirth: 1887, contribution: 'Wave Mechanics', yearsSinceHis20: 116 },
    { name: 'Werner Heisenberg', yearOfBirth: 1901, contribution: 'Matrix Mechanics', yearsSinceHis20: 102 },
    { name: 'Richard Feynman', yearOfBirth: 1918, contribution: 'Quantum Electrodynamics', yearsSinceHis20: 85 }
]
*/
```

## Reduce Sum
------------------------
[!NOTE]
A function that return a boolean
a simple example compute extracted numbers from object
```javascript
const products = [
    { name: 'Laptop', price: 1000, quantitySold: 5 },
    { name: 'Mouse', price: 20, quantitySold: 100 },
    { name: 'Keyboard', price: 50, quantitySold: 50 },
    { name: 'Monitor', price: 200, quantitySold: 10 }
];

// Use the reduce method to compute the total revenue
const totalRevenue = products.reduce((accumulator, product) => {
    // For each product, compute the revenue by multiplying its price with the quantity sold
    // Then, add that revenue to the accumulator
    return accumulator + product.price * product.quantitySold;
}, 0);  // Initialize accumulator with 0

console.log(totalRevenue);  // Expected Output: 9200
```

## Reduce Flatten
------------------------
```javascript
const nestedArray = [1, [2, 3], [4, [5, 6]], 7];

// Use the reduce method to flatten the array
const flattenedArray = nestedArray.reduce((accumulator, currentValue) => {
    // Check if the currentValue is an array
    if (Array.isArray(currentValue)) {
        // If it is an array, concatenate it to the accumulator
        return accumulator.concat(currentValue);
    } else {
        // If it's not an array, just push the currentValue to the accumulator
        return [...accumulator, currentValue];
    }
}, []);  // Start with an empty array as the initial accumulator value

console.log(flattenedArray);  // Expected Output: [1, 2, 3, 4, 5, 6, 7]

```
another simpler example

```javascript
const products = [[0,1], [2,3], [4,5]];

const flatten = (stored, current) => storred.concat(current);

const flatenArray = array.reduce(flatten, [])

console.log(flattenArray)    // Expected Output: [0,1,2,3,4,5]
```

## Reduce Find
------------------------
```javascript
const arrays = [
    [1, 2, 3],
    [4, 5],
    [6, 7, 8, 9, 10],
    [11, 12, 13, 14],
    [15, 16, 17, 18, 19],
    [20, 21]
];

// Use the reduce method to find the sub-array(s) with the most items
const largestSubArrays = arrays.reduce((accumulator, currentValue) => {
    // Check if the current sub-array's length matches the first accumulator's length
    if (currentValue.length === accumulator[0].length) {
        // If yes, add the current sub-array to the accumulator
        return [...accumulator, currentValue];
    } 
    // If the current sub-array is larger than the accumulator's first sub-array
    else if (currentValue.length > accumulator[0].length) {
        // Replace the accumulator with a new array containing only the current sub-array
        return [currentValue];
    } else {
        // If no, continue with the accumulator unchanged
        return accumulator;
    }
}, [[]]);  // Initialize with an array containing an empty array

console.log(largestSubArrays);  
// Expected Output: [ [6, 7, 8, 9, 10], [15, 16, 17, 18, 19] ]
```

## Reduce Array of objects into a single dictionary
--------------------------
```javascript
const physicists = [
    { id: '1', name: 'Max Planck', yearOfBirth: 1858, contribution: 'Quantum Theory' },
    { id: '2', name: 'Albert Einstein', yearOfBirth: 1879, contribution: 'Theory of Relativity' },
    { id: '3', name: 'Niels Bohr', yearOfBirth: 1885, contribution: 'Atomic Model' },
    { id: '4', name: 'Richard Feynman', yearOfBirth: 1918, contribution: 'Quantum Electrodynamics' },
    { id: '5', name: 'Erwin Schrödinger', yearOfBirth: 1887, contribution: 'Wave Mechanics' }
];

// Use the reduce method to transform the collection
const transformedCollection = physicists.reduce((accumulator, physicist) => {
    accumulator[physicist.id] = physicist;
    return accumulator;
}, {});

console.log(transformedCollection);

/* Expected Output:
{
    '1': { id: '1', name: 'Max Planck', yearOfBirth: 1858, contribution: 'Quantum Theory' },
    '2': { id: '2', name: 'Albert Einstein', yearOfBirth: 1879, contribution: 'Theory of Relativity' },
    '3': { id: '3', name: 'Niels Bohr', yearOfBirth: 1885, contribution: 'Atomic Model' },
    '4': { id: '4', name: 'Richard Feynman', yearOfBirth: 1918, contribution: 'Quantum Electrodynamics' },
    '5': { id: '5', name: 'Erwin Schrödinger', yearOfBirth: 1887, contribution: 'Wave Mechanics' }
}
*/
```

## Compose
------------------------
[!NOTE]
Compose in functional programming is a function that takes any number of functions and returns a function that is the composition of those functions. The idea is that the return value of one function serves as the input for the next.
```javascript
// The compose function
function compose(...fns) {
    return (input) => fns.reduceRight((acc, fn) => fn(acc), input);
}

// Example collection of products
const products = [
    { id: 1, name: 'Laptop', price: 1000 },
    { id: 2, name: 'Mouse', price: 20 },
    { id: 3, name: 'Keyboard', price: 50 },
];

// Example functions to demonstrate composition:

// 1. Filter out products that are priced over $50
function filterExpensiveProducts(products) {
    return products.filter(product => product.price <= 50);
}

// 2. Convert the remaining products' names to uppercase
function productNamesToUppercase(products) {
    return products.map(product => ({ ...product, name: product.name.toUpperCase() }));
}

// Compose the functions
const composedFunction = compose(productNamesToUppercase, filterExpensiveProducts);

// Apply the composed function on the products collection
const transformedProducts = composedFunction(products);

console.log(transformedProducts);
// Expected Output:
// [
//     { id: 2, name: 'MOUSE', price: 20 },
//     { id: 3, name: 'KEYBOARD', price: 50 },
// ]

/*
Explanation:

- `compose` first applies `filterExpensiveProducts` which removes the 'Laptop' as it's priced over $50.
- Then it applies `productNamesToUppercase` which transforms the name of each product to uppercase.
*/
```

## Pipe
------------------------
[!NOTE]
Pipe is often the counterpart to compose. While compose creates a new function by composing multiple functions from right to left, pipe composes functions from left to right.
```javascript
// Pipe function
function pipe(...fns) {
    return (input) => fns.reduce((acc, fn) => fn(acc), input);
}

// Example collection of products
const products = [
    { id: 1, name: 'Laptop', price: 1000 },
    { id: 2, name: 'Mouse', price: 20 },
    { id: 3, name: 'Keyboard', price: 50 },
];

// Example functions to demonstrate piping:

// 1. Convert product names to uppercase
function productNamesToUppercase(products) {
    return products.map(product => ({ ...product, name: product.name.toUpperCase() }));
}

// 2. Filter out products that are priced over $50
function filterExpensiveProducts(products) {
    return products.filter(product => product.price <= 50);
}

// Create a new function using pipe
const pipedFunction = pipe(productNamesToUppercase, filterExpensiveProducts);

// Apply the piped function on the products collection
const transformedProducts = pipedFunction(products);

console.log(transformedProducts);
// Expected Output:
// [
//     { id: 2, name: 'MOUSE', price: 20 },
//     { id: 3, name: 'KEYBOARD', price: 50 },
// ]

/*
Explanation:

- With `pipe`, we first apply `productNamesToUppercase` to transform all product names to uppercase.
- Then we apply `filterExpensiveProducts` to filter out products priced over $50.
- The order of function application is from left to right, as opposed to `compose` which would be from right to left.
*/
```

## Currying
------------------------
[!NOTE]
Currying is a technique in functional programming where a function that takes multiple arguments is transformed into a series of unary functions (functions that take one argument).
```javascript
// Curry function
function curry(fn) {
    return function curried(...args) {
        if (args.length >= fn.length) {
            return fn.apply(this, args);
        } else {
            return function (...args2) {
                return curried.apply(this, args.concat(args2));
            }
        }
    };
}

// Example collection of products
const products = [
    { id: 1, name: 'Laptop', price: 1000 },
    { id: 2, name: 'Mouse', price: 20 },
    { id: 3, name: 'Keyboard', price: 50 },
];

// A function to find products by a given field and value
function findProductBy(products, field, value) {
    return products.find(product => product[field] === value);
}

// Curry the function
const curriedFindProductBy = curry(findProductBy);

// Use the curried function
const findByPrice = curriedFindProductBy(products)('price');
const expensiveProduct = findByPrice(1000);

console.log(expensiveProduct);
// Expected Output:
// { id: 1, name: 'Laptop', price: 1000 }

/*
Explanation:

- We defined a currying function that transforms a multi-argument function into a series of unary functions.
- We defined a function `findProductBy` that takes three arguments: a product collection, a field, and a value to find a product by.
- Using currying, we then created a `curriedFindProductBy` function which takes one argument at a time.
- We partially applied the `products` argument first, then the 'price' field, and finally we searched for a product with a price of 1000.
*/
```
a more specific exampe
```javascript
// Curry function
function curry(fn) {
    return function curried(...args) {
        if (args.length >= fn.length) {
            return fn.apply(this, args);
        } else {
            return function (...args2) {
                return curried.apply(this, args.concat(args2));
            }
        }
    };
}

// Example collection of products
const products = [
    { id: 1, name: 'Laptop', price: 1000 },
    { id: 2, name: 'Mouse', price: 20 },
    { id: 3, name: 'Keyboard', price: 50 },
];

// Function to apply discount by role
function applyDiscount(product, role, discountMap) {
    if (!discountMap[role]) return product;

    const discount = discountMap[role];
    const discountedPrice = product.price * (1 - discount);

    return {
        ...product,
        price: discountedPrice
    };
}

const discounts = {
    student: 0.2, // students get 20% off
    employee: 0.5, // employees get 50% off
    affiliate: 0.1 // affiliates get 10% off
};

// Curry the function
const curriedApplyDiscount = curry(applyDiscount);

// Create specific discount functions for each role
const applyStudentDiscount = curriedApplyDiscount('student')(discounts);
const applyEmployeeDiscount = curriedApplyDiscount('employee')(discounts);
const applyAffiliateDiscount = curriedApplyDiscount('affiliate')(discounts);

// Test
console.log(applyStudentDiscount(products[0])); 
// Expected Output: { id: 1, name: 'Laptop', price: 800 }  (20% off 1000 is 800)

console.log(applyEmployeeDiscount(products[0]));
// Expected Output: { id: 1, name: 'Laptop', price: 500 }  (50% off 1000 is 500)

console.log(applyAffiliateDiscount(products[0]));
// Expected Output: { id: 1, name: 'Laptop', price: 900 }  (10% off 1000 is 900)

/*
Explanation:

- We have a `applyDiscount` function that takes a product, a role, and a map of discounts.
- Using currying, we first fix the role and the discount map. 
- This allows us to generate role-specific discount functions. 
- Each of these functions can now directly take a product and give the discounted product.

This pattern helps in generating specialized functions from more generic functions, making code more reusable and modular.
*/
```
