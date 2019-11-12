<template>

</template>

<script>
  import Content from "./Content.vue";

  export default {
    name: 'Modal',
    components: {Content},
    props: {
      title: 'Hello',
    },
    methods: {

    }
  };
</script>

<style lang="scss">
  .done {
    text-decoration-line: line-through;
  }
</style>
