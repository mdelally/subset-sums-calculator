<template>
  <div id="app">
    <h1>Subset Sums Calculator</h1>
    <hr>
    <calculator />
  </div>
</template>

<script>


import Calculator from './components/Calculator';
export default {
  name: 'app',
  components: {
    Calculator
  },
};
</script>

<style>
#app {
  padding-top: 1em;
  margin: auto;
  max-width: 950px;
}
</style>
