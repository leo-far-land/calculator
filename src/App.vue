<template>
  <div id="app">
    <p class="font-weight-bold" style="font-size: 24pt;">Vue Calculator</p>
    <img src="./assets/logo.png" alt="">
    <Output :current="current"/>
    <Calculator @current="current = $event" style="padding: 20px"/>
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'
import Output from './components/Output.vue'

export default {
  name: 'App',
  data() {
    return {
      current: "",
      operator: null,
      previous: null,
    }
  },
  components: {
    Calculator, Output
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
