<template>
  <div id="app">

    <!--向模板传值-->
    <v-header :seller="seller"></v-header>

    <div class="tab border-1px">
      <router-link class="tab-item" to="/goods">商品</router-link>
      <router-link class="tab-item" to="/ratings">评价</router-link>
      <router-link class="tab-item" to="/seller">商家</router-link>
    </div>
    <router-view></router-view>

  </div>
</template>

<script>
  import header from './components/header/header.vue';

  const ERR_OK = 0;

//  var sellerData = '';

    export default {

    data() {
        return {
            seller: {}
        };
    },
//      created 这个钩子在实例被创建之后被调用
//      created: function () {
//        // `this` 指向 vm 实例
//        console.log('a is: ' + this.a)
//      }
    created() {
      this.$http.get('/api/seller').then((response) => {
          response = response.body;
//          console.log(response);
          if (response.errno === ERR_OK) {
              this.seller = response.data;
              console.log(this.seller);
//              sellerData = this.seller;
//              debugger;
          };
      });
    },
    components: {
      'v-header': header
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus" >
  @import "./common/stylus/mixin.styl";

  /*&是父元素的意思*/
  #app
    .tab
      display:flex
      width:100%
      height:40px
      line-height:40px
      /*border-bottom:1px solid rgba(7,17,27,0.1)*/
      border-1px(rgba(7,17,27,0.1))
      .tab-item
        flex:1
        text-algin:center
        font-size:14px
        color:rgb(77,85,93)
        &.active
          color:rgb(240,20,20)



</style>
