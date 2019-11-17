<template>
 <div id="app">
  <img alt="Vue logo" src="./assets/logo.png">
  <h1 style="color: #41b883"> ToDo List</h1>
  <i class="fas fa-plus-square" @click="addBoard" style="color: white"></i>
  <div class="container">
  <div class="row">
   <div v-for="(board, boardId) in boards" class="col" :key="boardId">
    <div style="border-color: white; border: white">
     <br>
     <input type="text" class="input-title-board" v-model="board.title" @keypress="changeTitleBoard">
     <i class="far fa-trash-alt" @click="removeBoard(board.id)"></i>
     <div class="control-bar">
      <input id="create-task" type="text" v-model="board.inputTask" @keypress="addTask($event, boardId)"
             class="m-2 p-1"
             style="border-radius: 15px; background-color: #383d41; color: white; border-color: #383d41">
     </div>
     <draggable
      :list="board.tasks"
      :group="{ name: 'g1'}"
     >
      <transition-group>
       <Task
        v-for="(task, index) in board.tasks"
        :key="task.id + board.id"
        :task="task"
        @input="onTaskChange($event, boardId)"
        class="p-0"
        @erase="eraseTask(index, boardId)"
       />
      </transition-group>
     </draggable>
    </div>
    </div>
  </div>
 </div>
 </div>
</template>

<script>
import draggable from 'vuedraggable';
import Task from './components/Task.vue';

export default {
  name: 'app',
  components: {
    Task,
    draggable,
  },
  data() {
    return {
      countBoard: 1,
      boards: [
        {
          id: 1,
          title: 'Perso',
          inputTask: '',
          count: 0,
          sort: 'all',
          tasks: [
            {
              id: 0,
              title: '1',
              isdone: false,
              job: '',
              boardId: 0,
            },
          ],
        },
      ],
    };
  },
  methods: {
    changeTitleBoard() {
      localStorage.setItem('board', JSON.stringify(this.boards));
    },
    removeBoard(id) {
      this.boards = this.boards.filter(board => board.id !== id);
    },
    addBoard() {
      this.countBoard = this.countBoard + 1;
      const newBoard = {
        id: this.countBoard,
        title: 'Nouveau tableau',
        inputTask: '',
        count: 0,
        sort: 'all',
        tasks: [],
      };
      this.boards.push(newBoard);
    },
    eraseTask(e, index) {
      this.boards[index].tasks.splice(e, 1);
      localStorage.setItem('board', JSON.stringify(this.boards));
    },
    addTask(e, index) {
      if (e.code === 'Enter') {
        const newTask = {
          id: this.boards[index].count + 1,
          title: this.boards[index].inputTask,
          isdone: false,
          boardId: this.boards[index].id,
        };
        this.boards[index].count = this.boards[index].count + 1;
        this.boards[index].tasks.push(newTask);
        this.boards[index].inputTask = '';
        localStorage.setItem('board', JSON.stringify(this.boards));
      }
    },
    onTaskChange(newTask, index) {
      this.boards[index].tasks = [...this.boards[index].tasks.filter(task => task.id !== newTask.id), newTask];
      localStorage.setItem('board', JSON.stringify(this.boards));
    },
  },
  computed: {
    // filterByDone() {
    //   return this.tasks.filter((task) => {
    //     switch (this.sort) {
    //       case 'all':
    //         return true;
    //         break;
    //       case 'done':
    //         if (!task.isdone) {
    //           return task;
    //         }
    //         break;
    //       case 'undone':
    //         if (task.isdone) {
    //           return task;
    //         }
    //         break;
    //     }
    //     return true;
    //   });
    // },
  },
  mounted() {
    if (localStorage.getItem('board')) {
      try {
        this.boards = JSON.parse(localStorage.getItem('board'));
      } catch (e) {
        localStorage.removeItem('board');
      }
    }
    if (localStorage.getItem('count')) {
      try {
        this.countBoard = parseInt(localStorage.getItem('count'), 10);
      } catch (e) {
        localStorage.removeItem('count');
      }
    }
  },
  watch: {
    boards() {
      localStorage.setItem('board', JSON.stringify(this.boards));
    },
    countBoard() {
      localStorage.setItem('count', this.countBoard);
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

 .custom-control-input:checked ~ .custom-control-label::before {
  color: #fff;
  border-color: #41b883;
  background-color: #41b883;
 }

 .input-title-board {
  color: white;
  background-color: #1b1e21;
  border: none;
  border-color: transparent;
  text-align: center;
 }
</style>
