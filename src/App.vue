<template>
  <div id="app">
    <QR></QR>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import QR from './components/QR.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    QR
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
