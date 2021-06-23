<template>
  <HelloWorld msg="Hello World of Science!"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: rgba(44, 62, 80, 0.9);
  background: rgba(44, 62, 80, 0.05);
  padding: 1px;
  min-height: 100vh;
}
</style>
