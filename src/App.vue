<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1> ToDo List</h1>
    <Task v-for="task in tasks" :value="task"/>
  </div>
</template>

<script>
import Task from './components/Task.vue';

export default {
  name: 'app',
  components: {
    Task,
  },
  data() {
    return {
      tasks: [
        {
          title: 'Faire les courses',
          isdone: true,
        },
      ],
    };
  },
};
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
