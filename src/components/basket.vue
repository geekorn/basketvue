<template>
  <section class="basket">
    <div class="title">Корзина</div>
    <div class="goods">
      <div class="goods__header">
        <div class="selected">Выделено <span class="selected__count">{{count}}</span></div>
        <button class="del-selected"><span class="del-selected__icon"></span>Удалить выделенные</button>
      </div>
      <ol class="goods__list">
        <goodsItem v-for="product in goods" :product="product" :key="product.id"></goodsItem>
      </ol>
      <div class="subtotal">
        <div class="subtotal__total">Промежуточный итог по корзине: {{subtotal}} Р</div>
        <div class="subtotal__nds">В том числе НДС: {{nds}} Р</div>
      </div>
    </div>
  </section>
</template>

<script>
  import goodsItem from './product.vue'
    export default {
        name: 'basket',
        data: function () {
            return {
                subtotal: 150,
                count: 3,
                goods: [
                    {
                        id: 123,
                        name: 'нож',
                        price: 990,
                        count: 2,
                        img: ''
                    },
                    {
                        id: 5234,
                        name: 'рюкзак',
                        price: 3990,
                        count: 1,
                        img: ''
                    }
                ]
            }
        },
        computed: {
            nds: function () {
                return this.subtotal * 18 / 100;
            }
        },
        components: {
            goodsItem
        }
    }
</script>

<style lang="scss">
  .title {
    margin-bottom: 40px;
    font-size: 30px;
    color: #0a7eb5;
  }
  .goods__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px;
    background-color: #d9e8ef;
  }
  .selected{
    &__count {
      font-weight: bold;
    }
  }
  .del-selected {
    border: none;
    background-color: transparent;
    text-decoration: underline;

    &__icon {
      position: relative;
      display: inline-flex;
      justify-content: center;
      align-items: center;
      width: 20px;
      height: 20px;
      border-radius: 3px;
      background-color: gray;
      margin-right: 6px;
      vertical-align: middle;
      &:before, &:after {
        content: '';
        position: absolute;
        top: 50%;
        left: 50%;
        display: block;
        width: 2px;
        height: 13px;
        background-color: #d9e8ef;
        border-radius: 3px;
      }
      &:before {
        transform:  translate(-50%, -50%) rotate(45deg);
      }
      &:after {
        transform:  translate(-50%, -50%) rotate(-45deg);
      }
    }
    &:hover {
      text-decoration: none;
    }
  }
  .goods__list {
    counter-reset: productsCounter;
  }
</style>