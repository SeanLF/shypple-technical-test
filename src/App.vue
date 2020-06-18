<template>
  <div id="app">
    <header>
      <h1>Shypple Technical Test</h1>
    </header>
    <main>
      <div class="requirements">
        <h2>Instructions</h2>
        <p>
          Create a 50x50 grid. Whenever you click on a cell in this grid, 1 is added to all cells
          in the same row and column. If a cell was empty, set it to 1. Every change to a cell
          should cause the cell to briefly light up yellow. If at least 5 successive numbers in
          the cells form a part of a Fibonacci sequence, shortly light these cells up green and
          then empty these cells. Use any framework or programming language you like.
        </p>
      </div>
      <div class="parameters">
        <h2>Parameters</h2>
        <label for="grid-size">Grid size:</label>
        <input
          type="number"
          name="grid-size"
          id="grid-size"
          v-model.number="gridSize"
          min="0"
          max="100"
        />
      </div>
      <Grid :gridSize="gridSize"></Grid>
    </main>
  </div>
</template>

<script>
import Grid from './components/Grid.vue';

export default {
  name: 'App',
  data: () => ({
    gridSize: 50,
  }),
  components: {
    Grid,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
h2 {
  font-size: 1rem;
}
.requirements p {
  font-family: monospace;
  margin: auto 1rem;
  border-left: 0.3rem solid #aaa;
  padding-left: 0.5rem;
}
.parameters {
  margin: 1rem auto;
}
.parameters label::after {
  content: ' ';
  width: 0.1rem;
}
.parameters input {
  width: 3rem;
}
</style>
