<template>
  <div id="app">
    <img src="./assets/logo.png">
    <HelloWorld/>
    <ListaProyectos></ListaProyectos>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import ListaProyectos from './components/proyectos'

export default {
  name: 'App',
  components: {
    HelloWorld,
    ListaProyectos
  }
}
</script>

<style>

</style>
