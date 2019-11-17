<template>
  <div class="custom-control custom-checkbox mt-2">
     <input type="checkbox" class="custom-control-input" :id=" task.boardId+'task-checkbox' + task.id  " :checked="task.isdone" @change="change">
     <label :for=" task.boardId+'task-checkbox' + task.id  " :class="{done: task.isdone}" class="custom-control-label" style="color: white"> {{ task.title }} </label>
     <i class="fas fa-trash m-1" style="color: #35495e" @click="erase"></i>
  </div>
</template>

<script>
export default {
  name: 'Task',
  props: {
    task: {
      type: Object,
      required: true,
    },
  },
  methods: {
    change(e) {
      this.$emit('input', { ...this.task, isdone: e.target.checked });
    },
    erase() {
      this.$emit('erase', { ...this.task });
    },
  },
};
</script>

<style lang="scss">
    .done {
        text-decoration-line: line-through;
    }
</style>
