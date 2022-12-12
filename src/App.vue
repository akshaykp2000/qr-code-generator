<template>
  <div>
    <QrCodeGenerator></QrCodeGenerator>
  </div>
</template>

<script>
import QrCodeGenerator from './components/QrCodeGenerator.vue'

export default {
  name: 'App',
  components: {
    QrCodeGenerator
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
