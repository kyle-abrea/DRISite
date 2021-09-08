<template>
  <div id="app">
    <!-- <img alt="Vue  logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <Navigation/>
    <Registration/>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Navigation from './components/Navigation.vue'
import Registration from './components/Registration.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld,
    Navigation,
    Registration
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
  /* color: hot; */

  margin:0;
  height:100%;
  border: 5px black solid; 
  background-color: #2c3e50;

}
</style>


