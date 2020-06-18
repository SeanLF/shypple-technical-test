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
  computed: {
    flatGrid() {
      return this.grid.flat();
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
