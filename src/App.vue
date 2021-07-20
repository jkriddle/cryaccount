<template>
  <div id="app">
    <Portfolio />
  </div>
</template>

<script>
import Portfolio from './components/Portfolio.vue'

export default {
  name: 'App',
  components: {
    Portfolio
  }
}
</script>

<style>
#app {
  margin:20px;
}
</style>
