<template>
  <div class="breadcrumbs">
    <a href="#" class="breadcrumbs__link">Главная</a>
    /
    <a href="#" class="breadcrumbs__link">Корзина</a>
  </div>
</template>

<script>
    export default {
        name: 'breadcrumbs'
    }
</script>

<style lang="scss">
  .breadcrumbs {
    margin-bottom: 20px;
  }
  .breadcrumbs__link {
    margin: 0 5px;
    color: #333333;

    &:hover {
      text-decoration: none;
    }
    
    &:last-child {
      text-decoration: none;
      pointer-events: none; /* делаем ссылку некликабельной */
      cursor: default;
    }
  }
</style>