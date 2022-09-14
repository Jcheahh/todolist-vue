<template>
  <AppHeader />
  <TodoList />
  
</template>

<script>
  import TodoList from './components/TodoList.vue'
  import AppHeader from './components/AppHeader.vue'

export default {
  name: 'App',
  components: {
    TodoList,
    AppHeader,
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
