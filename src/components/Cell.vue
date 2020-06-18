<template>
  <div class='cell' :style="style">
    <span class='value'>{{ cell.count }}</span>
  </div>
</template>

<script>
export default {
  name: 'Cell',
  props: {
    cell: Object,
    gridSize: Number,
  },
  computed: {
    style() {
      return `width: calc(${100 / this.gridSize}% - 2px`;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cell {
  height: 1rem;
  width: 1rem;
  border: 1px solid #eee;
  justify-content: center;
  user-select: none;
}
.value {
  text-align: center;
}
</style>
