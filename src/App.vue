<template>
  <img id="logo" alt="Vue logo" src="./assets/helm.svg" >
  <AvailableCharts/>
</template>

<script>
import AvailableCharts from './components/AvailableCharts.vue'

export default {
  name: 'App',
  components: {
    AvailableCharts
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
#logo {
  width: 150px;
}
</style>
