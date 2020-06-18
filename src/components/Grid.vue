<template>
  <div class="grid">
  </div>
</template>

<script>
export default {
  name: 'Grid',
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
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
