<template>
  <div id="app">
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
  margin:0;
  height:100%;
  background-color: #2c3e50;
  /* border: 5px black solid;  */
}
</style>


