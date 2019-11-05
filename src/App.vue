<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1> ToDo List</h1>
    <input id="create-task" type="text" v-model="inputTask" @keypress="addTask">
    <Task v-for="task in tasks" :key="task.id" :task="task" @input="onTaskChange"/>
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
          id: 0,
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
          id: this.tasks.length,
          title: this.inputTask,
          isdone: false
        };
        this.tasks.push(newTask);
        this.inputTask ='';
      }
    },
    onTaskChange(newTask){
      return this.tasks = [...this.tasks.filter(task => task.id !== newTask.id), newTask]
    },
  },
  computed: {
    filterByDone() {

    }, 
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
#create-task {

}
</style>
