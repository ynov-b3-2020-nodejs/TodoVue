<template>
  <div class="custom-control custom-checkbox">
<<<<<<< HEAD
    <input type="checkbox" :id="'task-checkbox' + task.id" :checked="task.isdone" @change="change" class="custom-control-input" id="customCheck1">
    <label :for="'task-checkbox' + task.id" :class="{done: task.isdone}" class="custom-control-label" for="customCheck1"> {{ task.title }} </label>
=======
    <input type="checkbox" :id="'task-checkbox' + task.id" :checked="task.isdone" @change="change" class="">
    <label :for="'task-checkbox' + task.id" :class="{done: task.isdone}"> {{ task.title }} </label>
>>>>>>> f2981edde37c0535cbe76f300945d7281be84729
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
