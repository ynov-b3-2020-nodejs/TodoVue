<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1> ToDo List</h1>
    <input type="text" v-model="inputTask" @keypress="addTask">
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
      inputTask: '',
      tasks: [
        {
          title: 'Faire les courses',
          isdone: false,
        },
      ],
    };
  },
  methods: {
    addTask(e) {
        if (e.code === 'Enter'){
          const newTask = {
            title: this.inputTask,
            isdone: false
          };
          this.tasks.push(newTask);
          this.inputTask ='';
        }
    }
  }
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
