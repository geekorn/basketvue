<template>
  <li class="goods__item product">
    <div class="product__number">
      <label class="checkbox">
        <input class="checkbox__fake" type="checkbox" v-model="product.checked" v-bind:id="product.id">
        <span class="checkbox__styled"></span>
      </label>
      <span class="number">{{index}}</span>
    </div>
    <div class="product__img">
      <img :src="getImgUrl(product.img)" alt="">
    </div>
    <div class="product__name">{{product.name}}</div>
    <div class="product__price">
      <span class="price">{{product.price}} Р</span>
      x
      <span class="amount"><input type="text" v-model="product.count" v-on:click="openModal" readonly></span>
      =
      <span class="total" >{{totalPrice}} Р</span>
    </div>
  </li>
</template>

<script>
    import modal from './modal.vue'
    export default {
        name: 'product',
        props: {
            index: Number,
            product: Object
        },
        computed: {
            totalPrice: function () {
                return this.product.price * this.product.count
            }
        },
        methods: {
            getImgUrl: function (imgName) {
                let images = require.context('../assets/', false, /\.png$/)
                return images('./' + imgName + ".png")
            },
            openModal: function (e) {
                let coords = [e.clientY, e.clientX];
                this.$emit('showModal', this.product.id, coords)
            }
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
    height: 75px;
    & > div {
      position: relative;
      display: flex;
      align-items: center;
      &:not(:last-child) {
        &:after {
          content: '';
          position: absolute;
          top: 0;
          right: 0;
          bottom: 0;
          display: block;
          width: 2px;
          border-right: 1px dotted #000000;
        }
      }
    }

    &__number, &__img {
      flex: 1;
    }
    &__number {
      display: flex;
      justify-content: space-around;
    }
    &__img {
      img {
        margin: 0 auto;
      }
    }
    &__name {
      flex: 6;
      padding: 0 20px;
      font-family: Arial;

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

  .checkbox__fake {
    position: absolute;
    left: -9999px;
    &:checked {
      ~ .checkbox__styled {
        background-image: url(../assets/shape.png);
      }
    }
  }
  .checkbox__styled {
    display: inline-block;
    width: 20px;
    height: 20px;
    padding: 5px;
    border-radius: 3px;
    box-shadow: inset 0 0 5px rgba(#000000, 0.12);
    background-repeat: no-repeat;
    background-size: 75%;
    background-position: 50% 25%;
  }
</style>