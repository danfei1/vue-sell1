<template>
  <div class="cartcontrol">
    <transition name="move">
      <div class="cart-decrese icon-remove_circle_outline" v-show="food.count>0" @click.stop="decreseCart($event)">
      </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click.stop="addCart($event)"></div>
  </div>
</template>

<script type="text/ecmascript-6">
  import Vue from 'vue';
  export default {
    props: {
      food: {
        type: Object,
        default() {
          return {};
        }
      }
    },
    data() {
      return {};
    },
    created() {
    },
    methods: {
      addCart(event) {
        // 处理windows 两次触发
        if (!event._constructed) {
          return true;
        }
        if (!this.food.count) {
          Vue.set(this.food, 'count', 1);
        } else {
          this.food.count++;
        }
        this.$emit('cart-add', event.target);
      },
      decreseCart($event) {
        // 处理windows 两次触发
        if (!event._constructed) {
          return true;
        }
        if (this.food.count > 0) {
          this.food.count--;
        }
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .cartcontrol
    font-size: 0
    .cart-decrese
      display: inline-block
      padding: 6px
      display: inline-block
      line-height: 24px
      font-size: 24px
      color: rgb(0, 160, 220)
      &.move-enter-active, &.move-leave-active
        transition: all 0.4s linear
      &.move-enter-to, &.move-leave
        opacity: 1
        transform: translate3D(0, 0, 0) rotate(0)
      &.move-enter, &.move-leave-to
        opacity: 0
        transform: translate3D(24px, 0, 0) rotate(180deg)
    .cart-count
      display: inline-block
      vertical-align: top
      width: 12px
      padding-top: 6px
      line-height: 24px
      text-align: center
      font-size: 10px
      color: rgb(147, 153, 159)
    .cart-add
      display: inline-block
      padding: 6px
      line-height: 24px
      font-size: 24px
      color: rgb(0, 160, 220)
</style>
