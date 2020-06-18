<template>
  <div class='row'>
    <div class="cells">
      <Cell
        v-for="cell in row"
        :key="cell.index"
        :cell="cell"
        @clicked="clicked"
      ></Cell>
    </div>
  </div>
</template>

<script>
import Cell from './Cell.vue';

export default {
  name: 'Row',
  components: {
    Cell,
  },
  props: {
    row: Array,
  },
  methods: {
    clicked(row, column) {
      this.$emit('clicked', row, column);
    },
  },
};
</script>

<style>
.row, .cells {
  display: flex;
  justify-content: center;
}
</style>
