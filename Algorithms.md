# JavaScript Algorithms

Functions Insectarium

## Depth First Search function
----------------------
[!NOTE]
Giving a map of 2D array identify and count the islands with DFS:
const grid = [
    ['1', '1', '0', '0', '0'],
    ['1', '1', '0', '0', '0'],
    ['0', '0', '1', '0', '0'],
    ['0', '0', '0', '1', '1']
];
```javascript
// Function to calculate the number of islands in a given grid
function numIslands(grid) {
    // If the grid is null or empty, return 0 islands
    if (!grid || grid.length === 0) {
        return 0;
    }

    // Define the number of rows and columns of the grid
    const rows = grid.length;
    const cols = grid[0].length;

    // Variable to store the number of found islands
    let count = 0;

    // Iterate through the grid
    for (let r = 0; r < rows; r++) {
        for (let c = 0; c < cols; c++) {
            // If a land cell (denoted by '1') is found, traverse the island and increase the count
            if (grid[r][c] === '1') {
                dfs(grid, r, c);
                count++;
            }
        }
    }

    // Return the total number of islands
    return count;
}

// Depth First Search function to traverse and mark an island
function dfs(grid, r, c) {
    // If the current cell is out of boundary or is water, stop the traversal
    if (r < 0 || c < 0 || r >= grid.length || c >= grid[0].length || grid[r][c] === '0') {
        return;
    }

    // Mark the current cell as visited by setting it to '0'
    grid[r][c] = '0';

    // Visit all the adjacent cells (up, down, left, right)
    dfs(grid, r - 1, c); // Traverse upwards
    dfs(grid, r + 1, c); // Traverse downwards
    dfs(grid, r, c - 1); // Traverse left
    dfs(grid, r, c + 1); // Traverse right
}

// Example usage of the code
const grid = [
    ['1', '1', '0', '0', '0'],
    ['1', '1', '0', '0', '0'],
    ['0', '0', '1', '0', '0'],
    ['0', '0', '0', '1', '1']
];
console.log(numIslands(grid));  // Expected output: 3

```

## Breadth First Search function
----------------------
[!NOTE]
Giving a map of 2D array identify and count the islands with BFS:
const grid = [
    ['1', '1', '0', '0', '0'],
    ['1', '1', '0', '0', '0'],
    ['0', '0', '1', '0', '0'],
    ['0', '0', '0', '1', '1']
];

```javascript
function numIslands(grid) {
    if (!grid || grid.length === 0) {
        return 0;
    }

    const rows = grid.length;
    const cols = grid[0].length;
    let count = 0;

    for (let r = 0; r < rows; r++) {
        for (let c = 0; c < cols; c++) {
            if (grid[r][c] === '1') {
                bfs(grid, r, c);
                count++;
            }
        }
    }

    return count;
}
// Breadth First Search function to traverse and mark an island
function bfs(grid, r, c) {
    const rows = grid.length;
    const cols = grid[0].length;

    // Define the directions to explore from a cell (up, right, down, left)
    const directions = [[-1, 0], [0, 1], [1, 0], [0, -1]];

    // Initialize a queue for BFS
    const queue = [];
    queue.push([row, column]);
    grid[row][column] = '0'; // Mark the starting cell as visited

    while (queue.length) {
        const [currentRow, currentColumn] = queue.shift();  // Dequeue the front cell

        for (let i = 0; i < directions.length; i++) {
            const [directionRow, directionColumn] = directions[i];
            const newRow = currentRow + directionRow;
            const newColumn = currentColumn + directionColumn;

            // If the neighboring cell is within the grid and is land, enqueue it for BFS
            if (newRow >= 0 && newRow < rows && newColumn >= 0 && newColumn < cols && grid[newRow][newColumn] === '1') {
                queue.push([newRow, newColumn]);
                grid[newRow][newColumn] = '0'; // Mark neighboring cell as visited
            }
        }
    }
}

// Example usage of the code
const grid = [
    ['1', '1', '0', '0', '0'],
    ['1', '1', '0', '0', '0'],
    ['0', '0', '1', '0', '0'],
    ['0', '0', '0', '1', '1']
];
console.log(numIslands(grid));  // Expected output: 3

```


## Sliding Window Algorithm
----------------------
[!NOTE]
Giving an array and a number k where k is smaller then array.length. Identify and count first k elements and the next k elements until the last k elements from the array with SWA then sum all those small :
const grid = [1, 2, 3, 4, 5, 6]; const K = 3;

### 1) Initialization:
    - Start by selecting the first k elements from the array: 1,2,3.
    - This selection is termed as the centerArray.
    - Sum the elements of the centerArray to get a result (in this case, 6).

### 2) Caching the Result:   
    - Store the summed result in an array called sumArray. So, sumArray initially becomes: [6].
    
### 3) Sliding the Window:
    - Subtract the first element of the current centerArray from the last sum (e.g., 6 - 1 = 5).
    - Add the value of the next unprocessed element outside of centerArray (in this case, 4).
    - The new sum becomes 5 + 4 = 9.
    - Cache this sum as well into the sumArray, making it: [6, 9].
    
### 4) Updating the centerArray:
    - Remove the first element from the centerArray.
    - Add the next unprocessed element from the main array to the centerArray.
    - In this example, after the first slide, the centerArray updates to: 2,3,4.
    
### 5) Continue the Processes 2, 3 and 4 with the new centerArray:
    - Continue the process of sliding the window and updating the centerArray until there are no elements left in the main array to be added to centerArray.
    
```javascript
/**
 * Computes the sliding window sum of k consecutive elements from an array.
 * @param {number[]} grid - The input array.
 * @param {number} k - The size of the sliding window.
 * @returns {number[]} - An array of sums for each window of size k.
 */
function slidingWindowSum(grid, k) {
    const n = grid.length;
    if (!grid || n < k) return [];

    // Step 1: Initialize
    let windowSum = 0;
    for (let i = 0; i < k; i++) {
        windowSum += grid[i];
    }

    const result = [windowSum];  // This will store the sums of each window

    // Step 3: Sliding the Window
    for (let i = k; i < n; i++) {
        // Subtract element going out of window and add element now being included
        windowSum = windowSum - grid[i - k] + grid[i];
        result.push(windowSum);
    }

    return result;
}

/**
 * Sums all values of an array.
 * @param {number[]} array - The input array.
 * @returns {number} - The sum of all elements.
 */
function sumArray(array) {
    return array.reduce((acc, val) => acc + val, 0);
}

// Example usage
const grid = [1, 2, 3, 4, 5, 6];
const K = 3;
const slidingSums = slidingWindowSum(grid, K);
console.log(slidingSums);  // Expected output: [6, 9, 12, 15]

// Sum all sliding window sums
const total = sumArray(slidingSums);
console.log(total);  // Expected output: 42

```
