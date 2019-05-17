<template>
  <div id="app">
    <Edit></Edit>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
// import QR from './components/QR.vue'
import Edit from './components/Edit.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    // QR,
    Edit
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
/* .dont-print{
  display: block;
} */


</style>
