<template>
  <div id="app">
    <ListaFotos />
  </div>
</template>

<script>
import ListaFotos from './components/ListaFotos.vue'

export default {
  name: 'App',
  components: {
    ListaFotos
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
