<template>
  <div class='cell' ref="cellEl" :style="style" @click="$emit('clicked', cell.row, cell.column)">
    <span class='value'>{{ cell.count }}</span>
  </div>
</template>

<script>
import { TimelineLite } from 'gsap';

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
  watch: {
    cell: {
      deep: true,
      handler(cell) {
        const { cellEl } = this.$refs;
        const timeline = new TimelineLite();
        timeline.to(cellEl, 0.5, { background: cell.count === null ? 'green' : 'yellow' });
        timeline.to(cellEl, 0.5, { background: 'initial' });
      },
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
