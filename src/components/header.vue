<template>
  <header class="header">
    <img src="../assets/logo.png">
    <search></search>
  </header>
</template>

<script>
  import search from './search.vue'

  export default {
      name: 'header',
      components: {
          search
      }
  }
</script>

<style lang="scss">
  .header {
    display: flex;
    justify-content: space-between;
  }
</style>