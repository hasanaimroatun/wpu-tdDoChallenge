<template>
  <div>
    <ToDo />
  </div>
</template>

<script>
import ToDo from './components/ToDoContainer.vue'

export default {
  name: 'App',
  components: {
    ToDo,
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
  margin-top: 32px;
}
</style>
