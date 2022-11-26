<template>
  <div id="app">
    <CalculatorItem></CalculatorItem>
    <!-- <calculator-item></calculator-item> -->
  </div>
</template>

<script>
import CalculatorItem from './components/CalculatorItem.vue'

export default {
  name: 'App',
  components: {
    CalculatorItem
  }
}
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
