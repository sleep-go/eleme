<template>
  <div class="cartcontrol">
    <transition name="move">
      <div class="cart-decrease" v-show="food.count>0" @click.prevent.stop="decreaseCart($event)">
        <i class="sell-icon icon-jian"></i>
      </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{ food.count }}</div>
    <div class="cart-add sell-icon icon-jia" @click.prevent.stop="addCart"></div>
  </div>
</template>

<script type="text/ecmascript-6">
  import Vue from 'vue';
  export default {
    props: {
      food: {
        type: Object
      }
    },
    methods: {
      addCart(event) {
        if (!event._constructed) {
          return;
        }
        if (!this.food.count) {
          Vue.set(this.food, 'count', 1);
        } else {
          this.food.count++;
        }
        this.$emit('addCart', event.target);
      },
      decreaseCart(event) {
        if (!event._constructed) {
          return;
        }
        if (this.food.count) {
          this.food.count--;
        }
      }
    }
  };
</script>

<style lang="scss" rel="stylesheet/scss">
  .cartcontrol {
    font-size: 0;
    color: rgb(0, 160, 220);
    .cart-decrease {
      transition: all 0.4s linear;
      &.move-enter-active {
        opacity: 1;
        transform: translate3d(0, 0, 0) rotate(0deg);
        display: inline-block;
      }
      &.move-enter, &.move-leave-active {
        opacity: 0;
        transform: translate3d(24px, 0, 0) rotate(180deg);
      }
    }
    .cart-decrease, .cart-add {
      transition: all 0.4s linear;
      display: inline-block;
      padding: 6px;
      font-size: 24px;
      line-height: 14px;
    }
    .cart-count {
      display: inline-block;
      vertical-align: top;
      width: 12px;
      padding-top: 4px;
      line-height: 24px;
      text-align: center;
      font-size: 10px;
      color: rgb(147, 153, 159);
    }
    .cart-add {
      font-size: 16px;
      margin-right: 20px;
      vertical-align: super;
    }
  }
</style>
