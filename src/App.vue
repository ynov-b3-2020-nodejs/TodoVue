<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1 style="color: #41b883"> ToDo List</h1>

    <div class="control-bar">
      <div class="custom-control custom-radio custom-control-inline">
        <input type="radio" name="sortValue" id="done" value="done" @click="sortTask" class="custom-control-input">
        <label for="done" class="custom-control-label"><i class="far fa-square" style="font-size: 15px; color: white "></i></label>
      </div>
      <div class="custom-control custom-radio custom-control-inline">
        <input type="radio" name="sortValue" id="undone" value="undone" @click="sortTask" class="custom-control-input">
        <label for="undone" class="custom-control-label"><i class="far fa-check-square" style="font-size: 15px; color: white"></i></label>
      </div>
      <div class="custom-control custom-radio custom-control-inline">
        <input type="radio" name="sortValue" id="all" value="all" @click="sortTask" class="custom-control-input">
        <label for="all" class="custom-control-label"><i class="fas fa-globe-africa" style="font-size: 15px; color: white"></i></label>
      </div>
    </div>
    <input id="create-task" type="text" v-model="inputTask" @keypress="addTask" class="m-2 p-1"
           style="border-radius: 15px">
    <br>
    <Task v-for="(task, index) in filterByDone" :key="task.id" :task="task" @input="onTaskChange"
          class="p-0" @erase="eraseTask(index)"/>
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
      sort: 'all',
      count: 1,
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
    eraseTask(e) {
      this.tasks.splice(e, 1);
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    addTask(e) {
      if (e.code === 'Enter') {
        const newTask = {
          id: this.count + 1,
          title: this.inputTask,
          isdone: false,
        };
        this.count = this.count + 1;
        this.tasks.push(newTask);
        this.inputTask = '';
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
        localStorage.setItem('count', this.count);
      }
    },
    onTaskChange(newTask) {
      this.tasks = [...this.tasks.filter(task => task.id !== newTask.id), newTask];
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    sortTask(e) {
      this.sort = e.target.value;
    },
  },
  computed: {
    filterByDone() {
      return this.tasks.filter((task) => {
        switch (this.sort) {
          case 'all':
            return true;
            break;
          case 'done':
            if (!task.isdone) {
              return task;
            }
            break;
          case 'undone':
            if (task.isdone) {
              return task;
            }
            break;
        }
      });
    },
  },
  mounted() {
    if (localStorage.getItem('tasks')) {
      try {
        this.tasks = JSON.parse(localStorage.getItem('tasks'));
      } catch (e) {
        localStorage.removeItem('tasks');
      }
    }
    if (localStorage.getItem('count')) {
      try {
        // eslint-disable-next-line radix
        this.count = parseInt(localStorage.getItem('count'));
      } catch (e) {
        localStorage.removeItem('count');
      }
    }
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
  .custom-control-input:checked~.custom-control-label::before {
    color: #fff;
    border-color: #41b883;
    background-color: #41b883;
  }
</style>
