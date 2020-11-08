<template>
  <div id="app">
    <VueSnake msg="Welcome to Vue Snake"/>
  </div>
</template>

<script>
import VueSnake from './components/VueSnake.vue'

export default {
  name: 'App',
  components: {
    VueSnake
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
