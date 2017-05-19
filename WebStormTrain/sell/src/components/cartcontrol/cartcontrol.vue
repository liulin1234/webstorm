<template>
  <div class="cartcontrol">
    <div class="cart-decrease " v-show="food.count>0" @click="decreaseCart"
        name="move" >
      <span class="inner icon-remove_circle_outline"  ></span>
    </div>
    <div class="cart-count" v-show="food.count>0">{{ food.count }}</div>
    <div class="cart-add icon-add_circle" @click="addCart"></div>
  </div>

</template>

<script type="text/ecmascript-6">
  import Vue from 'vue';

  export default {
    props: {
        // 接收外部模板传来的属性
        food: {
            type: Object
        }
    },
    data() {
        return {
          afg: 111
        };
    },
    created() {
        // 作为当前vue(实例)对象的属性
        // created 作为一个生命周期钩子，在实例创建之后被调用
//        console.log(this.food);
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
      },
      decreaseCart(event) {
            if (!event._constructed) {
                return;
            }
            if (this.food.count >= 1) {
                this.food.count--;
            }
      }
    }

  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .cartcontrol
    font-size: 0
    .cart-decrease
      display: inline-block
      padding: 6px
      .inner
        line-height: 24px
        font-size: 24px
        color: rgb(0,160,220)


    .cart-count
      display: inline-block
      vertical-align: top
      width: 12px
      padding-top: 6px
      line-height: 24px
      text-align: center
      font-size: 10px
      color: rgb(147,153,159)

    .cart-add
      display: inline-block
      padding: 6px
      line-height: 24px
      font-size: 24px
      color: rgb(0,160,220)


</style>
