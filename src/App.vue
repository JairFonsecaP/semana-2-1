<template>
  <div id="app">
    
    <clima :ciudades="ciudades"></clima>
  </div>
</template>

<script>
import clima from './components/ClimaActual.vue'
export default {
  name: 'App',
  components: {
    clima
  },
  data(){
    return {
      ciudades:[
        'Bogota',
        'Lima',
        'La Paz'
      ],
      ubicacion:'Jair'
    }
  }
}
</script>

<style>
#app {
  font-family:SF;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>