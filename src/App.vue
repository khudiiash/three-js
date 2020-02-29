<template>
  <div id="app">
    <Scene/>
  </div>
</template>

<script>
import Scene from './components/Scene.vue'
export default {
  name: 'app',
  components: {
    Scene
  }
}
</script>

<style>
body, .app{
  margin: 0;
  padding: 0;
    background: #000;

  overflow: hidden;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>