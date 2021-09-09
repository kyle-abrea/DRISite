<template>
  <div id="app">
    <!-- <img alt="Vue  logo" src="./assets/dri-logo.jpg"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <Header/>
    <Registration/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Registration from './components/Registration.vue'

export default {
  name: 'App',
  components: {
    Header,
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


