<template>
  <div id="app">
    <urinal-calculator/>
  </div>
</template>

<script>
import urinalCalculator from './components/urinalCalculator'
document.title = 'URIMAT Urinal Saving Calculator'
export default {
  name: 'App',
  components: {
    urinalCalculator
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
