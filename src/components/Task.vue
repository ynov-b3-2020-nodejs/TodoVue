<template>
  <div>
    <input type="checkbox" id="task-checkbox" v-model="value.isdone">
    <label for="task-checkbox"> {{ value.title }}</label>
    <i class="fas fa-times"></i>
  </div>
</template>

<script>
export default {
  name: 'Task',
  props: {
    value: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style lang="sass">

</style>
