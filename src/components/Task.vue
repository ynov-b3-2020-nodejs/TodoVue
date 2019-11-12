<template>
  <div class="custom-control custom-checkbox">
    <input type="checkbox" class="custom-control-input" :id="'task-checkbox' + task.id" :checked="task.isdone" @change="change">
    <label :for="'task-checkbox' + task.id" :class="{done: task.isdone}" class="custom-control-label" style="color: white" data-toggle="modal" data-target="taskModal"> {{ task.title }} </label>
    <i class="fas fa-edit" v-b-modal="`modal-${task.id}`"></i>
    <i class="fas fa-trash m-1" style="color: #35495e" @click="erase"></i>

    <b-modal :id="`modal-${task.id}`" :title="task.title">
      <p class="my-4"> {{ task.description }} </p>
    </b-modal>
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
