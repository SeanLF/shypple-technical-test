<template>
  <div id="app">
    <header>
      <h1>Shypple Technical Test</h1>
    </header>
    <main class="main">
      <aside class="aside">
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
          <div class="grid-size">
            <label for="grid-size">Grid size:</label>
            <input
              type="number"
              name="grid-size"
              id="grid-size"
              v-model.number="gridSize"
              min="5"
              max="100"
            />
          </div>
          <div class="search-params">
            <h3>Search:</h3>
            <div class="search-in-row">
              <label for="search-in-row">➡️</label>
              <input
                type="checkbox"
                name="search-in-row"
                id="search-in-row"
                v-model="searchInRow"
              />
            </div>
            <div class="search-in-column">
              <label for="search-in-column">⬇️</label>
              <input
                type="checkbox"
                name="search-in-column"
                id="search-in-column"
                v-model="searchInColumn"
              />
            </div>
            <div class="search-in-row-reverse">
              <label for="search-in-row-reverse">⬅️</label>
              <input
                type="checkbox"
                name="search-in-row-reverse"
                id="search-in-row-reverse"
                v-model="searchInRowReverse"
              />
            </div>
            <div class="search-in-column-reverse">
              <label for="search-in-column-reverse">⬆️</label>
              <input
                type="checkbox"
                name="search-in-column-reverse"
                id="search-in-column-reverse"
                v-model="searchInColumnReverse"
              />
            </div>
          </div>
        </div>
      </aside>
      <Grid
        :gridSize="gridSize"
        :searchInRow="searchInRow"
        :searchInColumn="searchInColumn"
        :searchInRowReverse="searchInRowReverse"
        :searchInColumnReverse="searchInColumnReverse"
      ></Grid>
    </main>
  </div>
</template>

<script>
import Grid from './components/Grid.vue';

export default {
  name: 'App',
  data: () => ({
    gridSize: 50,
    searchInRow: true,
    searchInColumn: true,
    searchInRowReverse: true,
    searchInColumnReverse: true,
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
@media only screen and (min-width: 1200px) {
  .main {
    display: flex;
    justify-content: space-evenly;
  }
  .aside {
    max-width: 300px;
  }
}
h2 {
  font-size: 1rem;
  margin-bottom: 0.1rem;
}
h3 {
  font-size: 0.9rem;
  margin-bottom: 0.1rem;
}
.requirements p {
  font-family: monospace;
  margin: auto 1rem;
  border-left: 0.3rem solid #aaa;
  padding: 0.5rem 0.5rem 0;
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
.search-params > div {
  display: flex;
  justify-content: center;
}
</style>
