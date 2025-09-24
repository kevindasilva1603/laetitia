<template>
  <div id="app">
    <TodoApp />
  </div>
</template>

<script>
import TodoApp from './views/TodoApp.vue'

export default {
  name: 'App',
  components: {
    TodoApp
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
  background-color: #f7f7f7;
}
</style>
