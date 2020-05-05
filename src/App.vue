<template>
  <div>
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings" tag="a">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller" tag="a">商家</router-link>
      </div>
    </div>
    <keep-alive>
      <router-view :seller="seller"></router-view>
    </keep-alive>
  </div>
</template>

<script type="text/ecmascript-6">
  import {urlParse} from 'common/js/util.js';
  import header from './components/header/header.vue';
  const ERR_OK = 0;
  export default {
    data() {
      return {
        seller: {
          id: (() => {
            let queryParam = urlParse();
            console.log(queryParam);
            return queryParam.id;
          })()
        }
      };
    },
    created() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
      this.$http.get('/api/seller?id=' + this.seller.id).then((responce) => {
        responce = responce.body;
        if (responce.errno === ERR_OK) {
          this.seller = Object.assign({}, this.seller, responce.data);
          console.log(this.seller);
        }
      });
    },
    components: {
      'v-header': header
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import './common/stylus/mixin.styl'
  .tab
    display: flex
    width: 100%
    line-height: 40px
    height: 40px
    //border-bottom: 1px solid rgba(1,17,27,0.1)
    border-1px(rgba(1, 17, 27, 0.1))
    .tab-item
      flex: 1
      text-align: center
      & > a
        display: block
        font-size: 14px
        color: rgb(77, 85, 93)
        &.active
          color: rgb(240, 20, 20)
</style>
