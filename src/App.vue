<template>
  <div id="app" :class="[showBg ? 'show-bg' : '']">
    <HelloWorld @show="changeBg"/>
  </div>
</template>

<script>
import HelloWorld from './components/Index.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data() {
    return {
      showBg: false
    }
  },
  methods: {
    changeBg() {
      this.showBg = true;
    }
  }
}
</script>

<style lang="less">
html {
  height: 100%;
}
body {
  height: 100%;
  margin: 0;
}
#app {
  display: flex;
  justify-content: center;
  height: 100%;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  &.show-bg {
    background: pink;
  }
}
</style>
