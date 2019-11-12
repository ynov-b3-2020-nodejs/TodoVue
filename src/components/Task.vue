<template>
    <div class="custom-control custom-checkbox">
        <input id="checkTask" type="checkbox" :id="'task-checkbox' + task.id" :checked="task.isdone" @change="change" class="custom-control-input">
        <label :for="'task-checkbox' + task.id" :class="{done: task.isdone}" style="color: white" class="custom-control-label" for="checkTask"> {{ task.title }} </label>
        <i class="far fa-times-circle m-1" style="color: white" @click="erase"></i>
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
