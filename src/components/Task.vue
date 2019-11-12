<template>
  <div class="custom-control custom-checkbox">
    <input type="checkbox" :id="'task-checkbox' + task.id" :checked="task.isdone" @change="change" class="">
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
    change(e) {
        this.$emit('input', {...this.task, isdone: e.target.checked});
    },
  },
};
</script>

<style lang="scss">
.done {
  text-decoration-line: line-through;
}
</style>
