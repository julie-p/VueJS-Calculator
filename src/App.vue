<template>
  <div id="app">
    <h1>VueJS Calculator</h1>
    <Calculator />
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Merriweather:wght@300&family=Montserrat:wght@200&family=Source+Serif+Pro&display=swap');

body {
  background: #FAACA8;
  background-image:
    radial-gradient(50% 30% ellipse at center top, #FAACA8 0%, rgba(0,0,0,0) 100%),
    radial-gradient(60% 50% ellipse at center bottom, #DDD6F3 0%, #FAACA8 100%);
  /* background-color: #FAACA8;
  background-image: linear-gradient(19deg, #FAACA8 0%, #DDD6F3 50%, #ffffff 100%); */
  background-attachment: fixed;
  color: #6cacc5;
}

h1 {
  color: #eee;
  margin-top: -10px;
}

#app {
  font-family: 'Montserrat', sans-serif; 
  /* font-family: 'Merriweather', serif; */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
