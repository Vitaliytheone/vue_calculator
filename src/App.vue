<template>
  <div id="app">
    <Calculator />
  </div>
</template>

<script>
import Calculator from './components/Calculator'

export default {
  name: 'app',
  components: {
    Calculator
    }
  }
</script>

<style>
    #app {
      margin: 200px;
    }
</style>
