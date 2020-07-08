<template lang="pug">
  #app
    Exchange
</template>

<script>
import Exchange from './components/Exchange.vue'

export default {
  name: 'App',
  components: {
    Exchange
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
