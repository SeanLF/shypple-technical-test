<template>
  <div id="app">
    <h1>Shyyple Technical Test</h1>
    <div class="requirements">
      <ul>
        <li>Build a 50x50 grid</li>
        <li>
          Increment the cell count by 1 on click, as well as the cells in the same row and column
        </li>
        <li>Briefly flash a cell yellow if its content changes</li>
        <li>Briefly flash a cell green if it's in a fibonacci sequence of 5 or more</li>
      </ul>
    </div>
    <div class="parameters">
      <label for="grid_size">Grid length</label>
      <input type="number" name="grid_size" id="grid_size" v-bind:value="gridSize">
    </div>
    <Grid v-bind:gridSize="gridSize"></Grid>
  </div>
</template>

<script>
import Grid from './components/Grid.vue';

export default {
  name: 'App',
  components: {
    Grid,
  },
  data: () => ({
    gridSize: 3,
  }),
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
