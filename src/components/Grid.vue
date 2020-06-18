<template>
  <div class="grid">
    <div class="cells">
      <Cell
        v-for="cell in flatGrid"
        :key="cell.index"
        :cell="cell"
        :gridSize="gridSize"
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
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cells {
  display: flex;
  flex-flow: row wrap;
}
</style>
