<template>
  <div class="grid">
    <div class="rows">
      <Row v-for="(row, index) in grid" :key="index" :row="row" @clicked="clicked"></Row>
    </div>
  </div>
</template>

<script>
import Row from './Row.vue';

const matrixColumn = (matrix, column) => matrix.map((row) => row[column]);

export default {
  name: 'Grid',
  components: {
    Row,
  },
  data: () => ({
    grid: null,
    fibonacciSequence: [1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233],
  }),
  props: {
    gridSize: Number,
  },
  watch: {
    gridSize: { // watch gridSize for changes
      immediate: true, // needed to create the grid on initial load
      handler() {
        this.grid = [...Array(this.gridSize).keys()].map((row) => (
          [...Array(this.gridSize).keys()].map((column) => ({
            index: row * this.gridSize + column,
            count: null,
            row,
            column,
          }))
        ));
      },
    },
  },
  // Computed caches results, and lazy loads
  computed: {
    // Flattens the grid
    flatGrid() {
      return this.grid.flat();
    },
    gridByColumn() {
      return this.grid.map((_, i, grid) => matrixColumn(grid, i));
    },
    flatGridByColumn() {
      return this.gridByColumn.flat();
    },
    // Counts the number of distinct Fibonacci numbers in the grid
    fibonacciUniqueCount() {
      return [...new Set(this.flatGrid.filter((cell) => this.isFibonacci(cell.count))
        .map((cell) => cell.count))].length;
    },
  },
  methods: {
    cellsInSameColumnOrRow(rowIndex, columnIndex) {
      // Use a set to prevent duplicate cell row and column intersection
      // Add the current row to the results
      const results = new Set(...[this.grid[rowIndex]]);
      // Iterate through the rows and add the column to the results set
      [...Array(this.gridSize).keys()].forEach((i) => {
        results.add(this.grid[i][columnIndex]);
      });
      // Return the unique cells as an array
      return [...results];
    },
    // Checks if a number is a valid Fibonacci number, and keeps it stored in data
    isFibonacci(n) {
      // skip nulls
      if (n === null) return false;

      let maxFibonacciNumber = Math.max(...this.fibonacciSequence);

      // If the number is in the range of stored fibonacci, is it in the list?
      if (n <= maxFibonacciNumber) return this.fibonacciSequence.includes(n);

      // The number is not in the range, compute the following fibonacci numbers until gte n
      while (maxFibonacciNumber <= n) {
        maxFibonacciNumber = this.fibonacciSequence.slice(-2).reduce((a, b) => a + b, 0);
        this.fibonacciSequence.push(maxFibonacciNumber);
      }
      return this.isFibonacci(n);
    },
    findFibonacciSequences(list = this.flatGrid) {
      // Filter out nulls
      const listNoNulls = list.filter((cell) => cell.count !== null);
      // Fibonacci sequences
      const toFlashGreen = [[]];
      // Iterate through all fibonacci numbers in the grid
      while (listNoNulls.length > 0) {
        // Current group to append to
        const currentGroup = toFlashGreen[toFlashGreen.length - 1];
        // Ensure current group has the last 2 elements to sum
        while (currentGroup.length < 2) currentGroup.push(listNoNulls.shift());
        // Current cell (starts at the 3rd cell in the grid)
        const cell = listNoNulls.shift();
        if (typeof cell === 'undefined') break;
        const [secondLast, last] = currentGroup.slice(-2).map((c) => c.count);
        const sumOfLastTwoElements = secondLast + last;
        /* If the last two elements equal the current cell count and is a fibonacci number, append
        *  Otherwise if currentGroup contains at least 5 elements, make a new group
        *  Otherwise clear currentGroup and add the current Fibonacci number to it
        */
        if (this.fibonacciSequence.includes(secondLast)
            && this.fibonacciSequence.includes(last)
            && this.fibonacciSequence.includes(sumOfLastTwoElements)
            && sumOfLastTwoElements === cell.count
        ) {
          currentGroup.push(cell);
        } else if (currentGroup.length >= 5) {
          const toPush = this.fibonacciSequence.includes(cell.count) ? [cell] : [];
          toFlashGreen.push(toPush);
        } else {
          const length = this.fibonacciSequence.includes(last) ? 1 : 0;
          while (currentGroup.length > length) currentGroup.shift();
          if (this.fibonacciSequence.includes(cell.count)) currentGroup.push(cell);
        }
      }
      // If the last group doesn't have at least 5 elements, get rid of it
      if (toFlashGreen[toFlashGreen.length - 1].length < 5) toFlashGreen.pop();
      // Flatten list of cells to clear and flash green
      return toFlashGreen.flat();
    },
    clicked(rowIndex, columnIndex) {
      // Get the cells in the same row and column and increment them each by 1
      const cellsToIncrement = this.cellsInSameColumnOrRow(rowIndex, columnIndex);
      for (let i = 0; i < cellsToIncrement.length; i += 1) {
        cellsToIncrement[i].count += 1;
      }
      // If the grid contains at least 4 distinct fibonacci numbers (two 1s)
      if (this.fibonacciUniqueCount >= 4) {
        // Find sequences of 5 or more consecutive fibonacci numbers
        let toFlashGreen = new Set(this.findFibonacciSequences());
        const forCol = this.findFibonacciSequences(this.flatGridByColumn);
        forCol.forEach((cell) => toFlashGreen.add(cell));
        toFlashGreen = [...toFlashGreen];
        // Clear their values, the cell component will handle the animation
        for (let idx = 0; idx < toFlashGreen.length; idx += 1) {
          toFlashGreen[idx].count = null;
        }
      }
    },
  },
};
</script>
