<template>
  <div>
    <input type="checkbox" :id="'task-checkbox' + task.id" :checked="task.isdone" @change="change">
    <label :for="'task-checkbox' + task.id" :class="{done: task.isdone}"> {{ task.title }} </label>
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
    change() {
        this.$emit('input')
    }
  }
};
</script>

<style lang="scss">
.done {
  text-decoration-line: line-through;
}
</style>
