<template>
    <div id="app">
      <img alt="Vue logo" src="./assets/logo.png">
      <h1> ToDo List</h1>
      <input id="create-task" type="text" v-model="inputTask" @keypress="addTask">
      <Task v-for="task in filterByDone" :key="task.id" :task="task" @input="onTaskChange"/>

      <div class="custom-control custom-radio custom-control-inline">
        <input type="radio" name="sortValue" id="done" value="done" @click="sortTask" class="custom-control-input">
        <label for="done" class="custom-control-label"><i class="far fa-check-square"></i></label>
      </div>
      <div class="custom-control custom-radio">
        <input type="radio" name="sortValue" id="undone" value="undone" @click="sortTask" class="custom-control-input">
        <label for="undone" class="custom-control-label"><i class="far fa-square"></i></label>
      </div>
      <div class="custom-control custom-radio">
        <input type="radio" name="sortValue" id="all" value="all" @click="sortTask" class="custom-control-input">
        <label for="all" class="custom-control-label"><i class="fas fa-globe-africa"></i></label>
      </div>
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
                if (e.code === 'Enter') {
                    const newTask = {
                        id: this.tasks.length,
                        title: this.inputTask,
                        isdone: false
                    };
                    this.tasks.push(newTask);
                    this.inputTask = '';
                    localStorage.setItem('tasks', JSON.stringify(this.tasks));
                }
            },
            onTaskChange(newTask) {
                return this.tasks = [...this.tasks.filter(task => task.id !== newTask.id), newTask]
            },
            sortTask(e) {
                this.sort = e.target.value;
            },
        },
        computed: {
            filterByDone() {
                return this.tasks.filter(task => {
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
                })
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

    #create-task {

    }
</style>
