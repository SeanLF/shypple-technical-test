# Shypple Technical Test

## Problem

Create a 50x50 grid.
Whenever you click on a cell in this grid, 1 is added to all cells in the same row and column.
If a cell was empty, set it to 1.
Every change to a cell should cause the cell to briefly light up yellow.
If at least 5 successive numbers in the cells form a part of a Fibonacci sequence, shortly light these cells up green and then empty these cells.
Use any framework or programming language you like.

### Assumptions

- The 5 successive numbers of a Fibonacci sequence must be consecutive (aside from nulls).
- Rows and columns should be considered. Diagonals should not be considered.
- Sequences overflowing into the next row or column should be considered.
- Reverse sequences (row/column) should not be considered.

### Implementation

This problem requires client interactivity, therefore web technologies are a good candidate for implementing the solution.

- [Vue.js](https://vuejs.org/) is used to handle DOM manipulation, even though a solution could be implemented in vanilla Javascript.
- [GSAP](https://greensock.com/gsap/) is used to animate state transitions, as Vue.js' method was not optimal.

#### Finding the cells to increment

Take all cells from the row the user clicked on, then iterate through the other rows and take the cell from the column the user clicked on.

#### Finding Fibonacci sequences

To simplify the task, the grid was flattened. This increases the space complexity, while increasing code legibility.
Options with this simplification in mind include:

- Dynamically search outwards from the updated cells if their neighbours are part of a Fibonacci sequence.
- Filter out all non-Fibonacci numbers from the grid, and check if a sequence of cells form a sub-sequence (of at least length 5) of the cached Fibonacci sequence.
- Filter out all null cells in the grid, then check that the last two cells, and their sum is a Fibonacci number, and that the sum is equal to the current cell. If at least 5 consecutive cells satisfy this condition, remember this sequence of cells.

The last option was implemented, and searching is possible by row, by column, and their reverse.

### File structure

- `./public/index.html` Vue.js mount point
- `./src/`
  - `App.vue`
  - `components/`
    - `Grid.vue`
    - `Row.vue`
    - `Cell.vue`

## Project setup

```bash
yarn install
```

### Compiles and hot-reloads for development

```bash
yarn serve
```

### Compiles and minifies for production

```bash
yarn build
```

### Lints and fixes files

```bash
yarn lint
```
