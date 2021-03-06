<template lang="html">
  <div class="app">
    <h1>5 Minute Todos!</h1>
    <Todos />
  </div>
</template>

<script>
import Todos from './components/Todos/Todos.vue';

export default {
  name: 'App',
  components: {
    Todos,
  },
};
</script>

<style>
body {
  background: #333;
  color: #f2f2f2;
}

.app {
  margin-top: 50px;
  font-family: Helvetica, Arial, serif;
  text-align: center;
}

h1 {
  font-family: 'Brygada 1918', serif;
  font-size: 2.5rem;
  font-weight: 500;
}
</style>
