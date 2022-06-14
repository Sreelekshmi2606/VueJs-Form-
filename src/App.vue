<template>
  <div id="app">
    <LoGin/>
  </div>
</template>

<script>
import LoGin from './components/login.vue'

export default {
  name: 'App',
  components: {
    LoGin
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
