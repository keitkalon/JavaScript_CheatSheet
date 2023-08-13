# JavaScript_CheatSheet

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
