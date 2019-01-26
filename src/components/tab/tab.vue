<template>
  <div class="tab">
    <cube-tab-bar
      :showSlider="true"
      v-model="selectedLabel"
      :data="tabs"
      ref="tabBar"
      class="border-bottom-1px">
    </cube-tab-bar>
    <div class="slide-wrapper">
      <cube-slide
        ref="slide"
        @change="onChange"
        @scroll="onScroll"
        :showDots="false"
        :loop="false"
        :autoPlay="false"
        :initial-index="index">
        <cube-slide-item>
          <goods></goods>
        </cube-slide-item>
        <cube-slide-item>
          <ratings></ratings>
        </cube-slide-item>
        <cube-slide-item>
          <seller></seller>
        </cube-slide-item>
      </cube-slide>
    </div>
  </div>
</template>

<script>
import Goods from 'components/goods/goods'
import Ratings from 'components/ratings/ratings'
import Seller from 'components/seller/seller'

export default {
  data () {
    return {
      index: 0,
      tabs: [{
        label: '商品'
      }, {
        label: '评论'
      }, {
        label: '商家'
      }]
    }
  },
  components: {
    Goods,
    Ratings,
    Seller
  },
  computed: {
    selectedLabel: {
      get () {
        return this.tabs[this.index].label
      },
      set (newVal) {
        this.index = this.tabs.findIndex((value) => {
          return newVal === value.label
        })
      }
    }
  },
  methods: {
    onChange (current) {
      this.index = current
    },
    onScroll (data) {
      console.log(data)
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import "~common/stylus/variable"
  .tab{
    display:flex;
    flex-direction :column;
    height:100%;
    >>> .cube-tab{
      padding:16px 0;
    }
    .slide-wrapper{
      flex:1;
      overflow:hidden;
    }
  }
</style>
