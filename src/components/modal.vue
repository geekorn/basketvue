<template>
  <transition name="modal">
    <div class="modal-wrapper" @click="$emit('close')">
      <div class="modal" @click.stop
           :style="{ top: coords[0] + 'px', left: coords[1] + 'px' }">
        <div class="modal__header">Изменить количество</div>
        <div class="modal__body">
          <div class="product__price">
            <span class="price">{{price}}</span>
            x
            <span class="amount">
            <button class="amount__btn" type="button" v-on:click="productAmountDec">-</button>
            <input type="text" v-model="amount">
            <button class="amount__btn" type="button" v-on:click="productAmountInc">+</button>
          </span>
            =
            <span class="total">{{totalPrice}} P</span>
          </div>
        </div>
        <div class="modal__footer">
          <button class="modal__btn modal__btn--save" type="button" @click="saveChange">Сохранить</button>
          <button class="modal__btn modal__btn--cancel" type="button" @click="$emit('close')">Отменить</button>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
    export default {
        name: 'modal',
        data: function () {
            return {
                amount: this.count
            }
        },
        props: {
            id: Number,
            count: Number,
            price: Number,
            coords: Array
        },
        computed: {
            totalPrice: function () {
                return this.price * this.amount
            }
        },
        methods: {
            productAmountDec: function () {
                return this.amount--;
            },
            productAmountInc: function () {
                return this.amount++;
            },
            saveChange: function () {
                this.$emit('updateCount', this.id, this.amount);
                this.$emit('close');
            }
        }
    }
</script>

<style lang="scss">
  .modal-wrapper {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background-color: rgba(#000000, 0.3);
  }
  .modal {
    position: absolute;
    transform: translate(-50%, 25px);
    padding: 20px 30px;
    border-radius: 5px;
    background-color: #ffffff;
    box-shadow: 0 0 13px rgba(#000000, 0.25);
    z-index: 1000;

    &__header {
      margin-bottom: 21px;
      font-weight: bold;
      color: #05689b;
    }
    &__body {
      margin-bottom: 24px;
      vertical-align: middle;
      .price {
        margin-right: 8px;
      }
      .total {
        margin-left: 8px;
      }
    }
  }

  .amount__btn {
    width: 20px;
    height: 20px;
    margin: 0 8px;
    border: none;
    background-color: #559abc;
    color: #ffffff;
  }

  .modal__btn {
    border: none;
    background-color: transparent;
    text-decoration: underline;
    text-transform: uppercase;
    &:hover {
      text-decoration: none;
    }
    &--save {
      margin-right: 20px;
      font-weight: 500;
      color: #05689b;
    }
  }
</style>