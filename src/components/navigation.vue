<template>
  <nav class="menu">
    <ul class="menu__list">
      <li class="menu__item">
        <span >Каталог продукции</span>
      </li>
      <li class="menu__item">
        <span >Все бренды</span>
      </li>
      <li class="menu__item">
        <span >подарки на 14 февраля</span>
      </li>
      <li class="menu__item">
        <span >подарки на 23 февраля</span>
      </li>
      <li class="menu__item">
        <span >подарки на 8 марта</span>
      </li>
    </ul>
  </nav>
</template>

<script>
    export default {
        name: 'menu'
    }
</script>

<style lang="scss">

  .menu {
    width: 100%;
    margin-bottom: 45px;
    text-align: center;
    &__list {
      width: 100%;
      display: flex;
    }
    &__item {
      flex-grow: 1;
      padding: 20px 0;

      border-radius: 3px 3px 0 0;
      text-transform: uppercase;
      background: #92c8e1;
      background: -moz-linear-gradient(left, #92c8e1 0%, #b1daed 100%);
      background: -webkit-linear-gradient(left, #92c8e1 0%, #b1daed 100%);
      background: linear-gradient(to right, #92c8e1 0%, #b1daed 100%);
      filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#92c8e1', endColorstr='#b1daed', GradientType=1);

      &:after {
        content: '';
        display: inline-block;
        width: 5px;
        height: 5px;
        /*margin-left: 11px;*/
        border: 2px solid transparent;
        border-left-color: #000000;
        border-bottom-color: #000000;
        transform: rotate(-45deg) translateY(-5px);
        transform-origin: 50% 50%;
      }
      span {
        margin-right: 15px;
      }
    }
  }
</style>