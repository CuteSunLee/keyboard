<template>
  <div id="app">
    <HelloWorld />
  </div>
</template>

<script>
import HelloWorld from './components/Index.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  methods: {
    add() {
      document.getElementsByClassName('demo1')[0].style.width = 400 + 'px';
    },
    sub() {
      document.getElementsByClassName('demo1')[0].style.width = 200 + 'px';
    }
  }
}
</script>

<style lang="less">
body {
  margin: 0;
}
#app {
  display: flex;
  justify-content: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
