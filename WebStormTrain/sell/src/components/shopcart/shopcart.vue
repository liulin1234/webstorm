<template>
  <div class="shopcart">
    <div class="content">
      <div class="content-left">
        <div class="logo-wrapper">
          <div class="logo" :class="{'highLight': totalCount > 0}">
            <span class="icon-shopping_cart" :class="{'highLight': totalCount > 0}"></span>
          </div>
          <div class="num" ref="number" v-show="totalCount > 0">{{ totalCount }}</div>
        </div>
        <div class="price" :class="{'highLight': totalPrice > 0}">￥{{ totalPrice }}</div>
        <div class="desc">另需配送费￥{{ deliveryPrice }}元</div>
      </div>
      <div class="content-right" :class="payClass">
        <div class="pay">
          {{ payDesc }}
        </div>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
      props: {
        selectFoods: {
            type: Array,
            default() {
                return [
                  {
                      price: 30,
                      count: 0
                  }
                ];
            }
        },
        deliveryPrice: {
            type: Number,
            default: 0
        },
        minPrice: {
            type: Number,
            default: 0
        }
      },
      computed: { // 计算属性
        totalPrice() {
            let total = 0;
            this.selectFoods.forEach((food) => {
                total += food.price * food.count;
            });
            return total;
        },
        totalCount() {
//            debugger;
            let count = 0;
//            let numDom = this.$refs.number;
            this.selectFoods.forEach((food) => {
                count += food.count;
            });
            if (count === 0) {
                return;
            } else {
              return count;
            }
        },
        payDesc() {
            if (this.totalPrice === 0) {
                return `￥${this.minPrice}元起送`;
            } else if (this.totalPrice < this.minPrice) {
                let diff = this.minPrice - this.totalPrice;
                return `还差￥${diff}元起送`;
            } else {
                return `去结算`;
            }
        },
        payClass() {
            if (this.totalPrice < this.minPrice) {
                return 'not-enough';
            } else {
                return 'enough';
            }
        }
      }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .shopcart
    position: fixed
    left: 0
    bottom: 0
    z-index: 50
    width: 100%
    height: 48px
    background: #000
    .content
      display: flex
      background: #141d27
      font-size: 0
      color: rgba(255,255,255,0.4)
      .content-left
        flex:1
        .logo-wrapper
          display: inline-block
          position: relative
          top: -10px
          margin: 0 12px
          padding: 6px
          width: 56px
          height: 56px
          box-sizing: border-box
          vertical-align: top
          border-radius: 50%
          background: #141d27
          .logo
            width: 100%
            height: 100%
            border-radius: 50%
            text-align: center
            background: #2b343c
            &.highLight
              background: rgb(0,160,220)
            .icon-shopping_cart
              line-height: 44px
              font-size: 24px
              color: #80858a
              &.highLight
                color: #fff
          .num
            position: relative
            top: -48px
            left: 27px
            background: red
            color: #fff
            font-size: 10px
            width: 20px
            height: 15px
            line-height: 15px
            font-weight: 700
            text-align: center
            border-radius: 8px
            z-index: 50
            box-shadow: 0px 4px 8px 0px rgba(0,0,0,0.4)
        .price
          display: inline-block
          vertical-align: top
          margin-top: 12px
          line-height: 24px
          padding-right: 12px
          box-sizing: border-box
          border-right: 1px solid rgba(255,255,255,0.1)
          font-size: 16px
          font-weight: 700
          color: rgba(255,255,255,0.4)
          &.highLight
            color: #fff
        .desc
          display: inline-block
          vertical-align: top
          margin: 12px 0 0 12px
          line-height: 24px

          font-size: 10px
    .content-right
      flex: 0 0 105px
      width: 105px
      background: #2b343c;
      .pay
        height: 48px
        line-height: 48px
        text-align: center
        font-size: 12px
        font-weight: 700
      &.not-enough
        background: #2b343c;
      &.enough
        background: green;
        color: #fff


</style>
