<template>
  <div id="app">
    <todo-app></todo-app>
  </div>
</template>

<script>
import todo from './components/TodoApp.vue'

export default {
  name: 'app',
  components:{
    'todo-app': todo,
  }
}
</script>

<style>
#app{
  width: 90%;
}
</style>