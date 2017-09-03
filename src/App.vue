<template>
  <div id="app">
    <div class="container">
      <appHeader></appHeader>
      <navigation></navigation>
      <breadcrumbs></breadcrumbs>
      <basket></basket>
    </div>
  </div>
</template>

<script>
    import appHeader from './components/header.vue'
    import navigation from './components/navigation.vue'
    import breadcrumbs from './components/breadcrumbs.vue'
    import basket from './components/basket.vue'

    export default {
        name: 'app',
        data () {
            return {
                // empty
            }
        },
        components: {
            appHeader,
            navigation,
            breadcrumbs,
            basket,
        }
    }
</script>

<style lang="scss">
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #333333;
  }

  h1, h2 {
    font-weight: normal;
  }

  ul,ol {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }

  li {
    padding: 0;
    margin: 0;
  }

  button {
    cursor: pointer;
    padding: 0;
  }

  .container {
    width: 1110px;
    margin: 0 auto;
  }
</style>
