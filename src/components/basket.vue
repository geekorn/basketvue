<template>
  <section class="basket">
    <h2 class="title">Корзина</h2>
    <div class="goods">
      <div class="goods__header">
        <div class="selected">Выделено <span class="selected__count">{{checkedCount}}</span></div>
        <button class="del-selected" @click="deleteChecked"><span class="del-selected__icon"></span>Удалить выделенные


        </button>
      </div>
      <ol class="goods__list" v-if="goods">
        <goodsItem v-for="(product, index) in goods"
                   :index="index + 1"
                   :product="product"
                   :key="product.id"
                   v-on:showModal="openModal">
        </goodsItem>
      </ol>
      <div class="" v-else> В  корзине пусто!</div>
      <div class="subtotal">
        <div class="subtotal__total">Промежуточный итог по корзине: <span class="subtotal__price">{{subtotal}} Р</span>
        </div>
        <div class="subtotal__nds">В том числе НДС: <span class="subtotal__price">{{nds}} Р</span></div>
      </div>
      <div class="total-price">итого: <span class="total-price__value">{{totalPrice}} P</span></div>
    </div>
    <modal v-if="showModal" @close="showModal = false"
           :id="modalData.id"
           :count="modalData.count"
           :price="modalData.price"
           :coords="modalData.coords"
           v-on:updateCount="updateCounts">
    </modal>
  </section>
</template>

<script>
    import goodsItem from './product.vue'
    import modal from './modal.vue'

    export default {
        name: 'basket',
        data: function () {
            return {
                dataUrl: 'dist/goods.json',
                goods: [],
                showModal: false,
                modalData: {},
            }
        },
        created: function () {
            this.$root.getData(this.dataUrl)
                .then( res => this.goods = res.data )
                .catch(error => {
                // error callback
            });

        },
        computed: {
            checkedCount: function () {
                return this.goods.filter(item => item.checked).length
            },
            subtotal: function () {
                return this.goods.reduce((total, product) => {
                    return total + (product.price * product.count)
                }, 0)
            },
            nds: function () {
                return this.subtotal * 18 / 100;
            },
            totalPrice: function () {
                return this.subtotal ? this.subtotal + 300 : 0;
            }
        },
        methods: {
            deleteChecked: function () {
                this.goods = this.goods.filter(item => !item.checked)
            },
            updateCounts: function (id, count) {
                return this.goods.forEach(item => {
                    if (item.id === id) {
                        item.count = count
                    }
                });
            },
            openModal: function (id, coords) {
                // полифилл Array.find для IE 11
                if (!Array.prototype.find) {
                    Array.prototype.find = function (predicate) {
                        if (this == null) {
                            throw new TypeError('Array.prototype.find called on null or undefined');
                        }
                        if (typeof predicate !== 'function') {
                            throw new TypeError('predicate must be a function');
                        }
                        var list = Object(this);
                        var length = list.length >>> 0;
                        var thisArg = arguments[1];
                        var value;

                        for (var i = 0; i < length; i++) {
                            value = list[i];
                            if (predicate.call(thisArg, value, i, list)) {
                                return value;
                            }
                        }
                        return undefined;
                    };
                };


                this.modalData = this.goods.find(item => item.id === id);
                this.modalData.coords = coords;
                this.showModal = true;
            }
        },
        components: {
            goodsItem,
            modal
        }
    }
</script>

<style lang="scss">
  .basket {
    font-size: 14px;
  }

  .title {
    margin-bottom: 40px;
    font-size: 30px;
    font-weight: 300;
    text-transform: uppercase;
    color: #0a7eb5;
  }

  .goods__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px;
    background-color: #d9e8ef;
  }

  .selected {
    font-weight: 600;
    &__count {
      font-size: 18px;
      font-weight: bold;
    }
  }

  .del-selected {
    border: none;
    background-color: transparent;
    text-decoration: underline;
    font-weight: 600;

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
        transform: translate(-50%, -50%) rotate(45deg);
      }
      &:after {
        transform: translate(-50%, -50%) rotate(-45deg);
      }
    }
    &:hover {
      text-decoration: none;
    }
  }

  .goods__list {
    counter-reset: productsCounter;
    padding-bottom: 15px;
    border-bottom: 1px solid #000;
  }

  .subtotal {
    padding: 26px 0;
    text-align: right;
    border-bottom: 1px dotted #000;

    &__price {
      display: inline-block;
      width: 150px;
      font-size: 18px;
      font-weight: bold;
    }
  }

  .total-price {
    padding-top: 20px;
    text-align: right;
    color: #0a7eb5;
    text-transform: uppercase;

    &__value {
      font-size: 24px;
      font-weight: bold;
      margin-left: 20px;
    }
  }
</style>