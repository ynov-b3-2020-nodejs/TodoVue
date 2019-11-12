<template>
    <div id="app">
        <img alt="Vue logo" src="./assets/logo.png">
        <h1> ToDo List</h1>
        <input id="create-task" type="text" v-model="inputTask" @keypress="addTask" class="m-2 p-1">
        <Task v-for="task in filterByDone" :key="task.id" :task="task" @input="onTaskChange" class="p-0" @erase="eraseTask"/>

        <input type="radio" name="sortValue" id="done" value="done" @click="sortTask">
        <label for="done"><i class="far fa-square"></i></label>
        <input type="radio" name="sortValue" id="undone" value="undone" @click="sortTask">
        <label for="undone"><i class="far fa-check-square"></i></label>
        <input type="radio" name="sortValue" id="all" value="all" @click="sortTask">
        <label for="all"><i class="fas fa-globe-africa"></i></label>
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
            eraseTask(e) {
                this.tasks.splice(e.id , e.id);
                localStorage.removeItem(JSON.stringify(this.tasks.find(task => task.id === e.id)))
            },
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
