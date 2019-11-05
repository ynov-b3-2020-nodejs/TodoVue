<template>
  <div>
    <input type="checkbox" id="task-checkbox">
    <label for="task-checkbox"> {{ msg }}</label>
    <i class="fas fa-times"></i>
  </div>
</template>

<script>
export default {
  name: 'Task',
  props: {
    msg: {
      type: String,
      default: 'Type...',
    },
  },
};
</script>

<style lang="sass">

</style>
