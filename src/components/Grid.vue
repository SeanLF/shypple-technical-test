<template>
  <div class="grid">
    <div class="cells">
      <Cell
        v-for="cell in flatGrid"
        :key="cell.index"
        :cell="cell"
        :gridSize="gridSize"
        @clicked="clicked"
      ></Cell>
    </div>
  </div>
</template>

<script>
import Cell from './Cell.vue';

export default {
  name: 'Grid',
  components: {
    Cell,
  },
  data: () => ({
    grid: null,
    fibonacciSequence: [1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233],
  }),
  props: {
    gridSize: Number,
  },
  watch: {
    gridSize: {
      immediate: true,
      handler() {
        this.grid = [...Array(this.gridSize).keys()].map((row) => (
          [...Array(this.gridSize).keys()].map((column) => ({
            index: row * this.gridSize + column,
            count: null,
            row,
            column,
            color: 'yellow',
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
    // Cells in the grid that have a count that is a Fibonacci number
    fibonacciCells() {
      return this.flatGrid.filter(this.cellContainsFibonacci);
    },
    // Counts the number of distinct Fibonacci numbers in the grid
    fibonacciUniqueCount() {
      return [...new Set(this.fibonacciCells.map((cell) => cell.count))].length;
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
      if (n <= maxFibonacciNumber) return this.fibonacciSequence.indexOf(n) !== -1;

      // The number is not in the range, compute the following fibonacci numbers until gte n
      while (maxFibonacciNumber <= n) {
        maxFibonacciNumber = this.fibonacciSequence.slice(-2).reduce((a, b) => a + b, 0);
        this.fibonacciSequence.push(maxFibonacciNumber);
      }
      return this.isFibonacci(n);
    },
    cellContainsFibonacci(cell) {
      return this.isFibonacci(cell.count);
    },
    clicked(rowIndex, columnIndex) {
      // Get the cells in the same row and column and increment them each by 1
      const cellsToIncrement = this.cellsInSameColumnOrRow(rowIndex, columnIndex);
      for (let i = 0; i < cellsToIncrement.length; i += 1) {
        cellsToIncrement[i].count += 1;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cells {
  display: flex;
  flex-flow: row wrap;
}
</style>
