<template>
  <li class="goods__item product">
    <div class="product__number">
      <label class="checkbox">
        <input class="checkbox__fake" type="checkbox">
        <span class="checkbox__styled"></span>
      </label>
      <span class="number"></span>
    </div>
    <div class="product__img">
      <img src="" alt="">
    </div>
    <div class="product__name">{{product.name}}</div>
    <div class="product__price">
      <span class="price">{{product.price}} Р</span>
      *
      <span class="amount"><input type="text" v-model="amount" v-on:click="openModal"></span>
      =
      <span class="total" >{{totalPrice}} Р</span>
    </div>
    <modal v-if="showModal" @close="showModal = false"
           :count="amount"
           :price="product.price"
           :coords="coords"
           v-on:updateCount="updateCounts">
    </modal>
  </li>
</template>

<script>
    import modal from './modal.vue'
    export default {
        name: 'product',
        props: {
            product: Object
        },
        data: function () {
            return {
                showModal: false,
                amount: this.product.count,
                coords: []
            }
        },
        computed: {
            totalPrice: function () {
                return this.product.price * this.amount
            }
        },
        methods: {
            openModal: function (e, count) {
                this.showModal = true;
                this.coords = [e.clientY, e.clientX];
            },
            updateCounts: function (count) {
                return this.amount = count;
            }
        },
        components: {
            modal
        }
    }
</script>

<style lang="scss">
  .goods__item {
    &:nth-child(even) {
      background-color: #f1f1f1;
    }
  }

  .product {
    display: flex;
    align-content: center;
    /*align-items: center;*/
    height: 75px;
    & > div {
      vertical-align: middle;
      /*:not(:last-child) {*/
        /*border-right: 1px dotted #000000;*/
      /*}*/
    }

    &__number, &__img {
      flex: 1;
    }
    &__name {
      flex: 6;
    }
    &__price {
      flex: 3;
      display: flex;
      justify-content: space-around;
      align-items: center;

      input {
        width: 57px;
        padding: 8px 0;
        border: none;
        border-radius: 3px;
        box-shadow: inset 0 0 5px rgba(#000000, 0.36);
        text-align: center;
        cursor: pointer;
      }
    }
  }
</style>