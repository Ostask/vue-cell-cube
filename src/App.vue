<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab-wrapper">
      <tab :tabs="tabs"></tab>
    </div>
  </div>
</template>

<script>
import VHeader from 'components/v-header/v-header'
import Tab from 'components/tab/tab'
import { getSeller } from 'api/index'
import Goods from 'components/goods/goods'
import Ratings from 'components/ratings/ratings'
import Seller from 'components/seller/seller'

export default {
  name: 'app',
  components: {
    VHeader,
    Tab,
    Goods,
    Ratings,
    Seller
  },
  data () {
    return {
      seller: {}
    }
  },
  computed: {
    tabs () {
      return [{
        label: '商品',
        component: Goods,
        data: {
          text: 'i am goods'
        }
      }, {
        label: '评论',
        component: Ratings,
        data: {
          text: 'i am ratings'
        }
      }, {
        label: '商家',
        component: Seller,
        data: {
          text: 'i am seller'
        }
      }]
    }
  },
  created () {
    this._getSeller()
  },
  methods: {
    _getSeller () {
      getSeller().then((seller) => {
        this.seller = seller
      })
    }
  }
}
</script>
<style lang="stylus" scoped>
  #app{
    .tab-wrapper{
      position:fixed;
      top:136px;
      left:0;
      right:0;
      bottom:0;
    }
  }
</style>
