# Shypple Technical Test

## Problem

Create a 50x50 grid.
Whenever you click on a cell in this grid, 1 is added to all cells in the same row and column.
If a cell was empty, set it to 1.
Every change to a cell should cause the cell to briefly light up yellow.
If at least 5 successive numbers in the cells form a part of a Fibonacci sequence, shortly light these cells up green and then empty these cells.
Use any framework or programming language you like.

### Assumptions

- Underlying model contains 0 for "empty" cells
- The 5 successive numbers of a Fibonacci sequence must be consecutive.
- Diagonals will not be considered. Columns will not be considered.
- A sequence overflowing in the next row will be considered.

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

