<template>
  <div id="app">
    <users-page />
  </div>
</template>

<script>
import UsersPage from './components/UsersPage/App.vue';

export default {
  components: {
    UsersPage,
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  color: #2c3e50;
}

* {
  box-sizing: border-box;
}
</style>
