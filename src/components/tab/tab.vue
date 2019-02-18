<template>
  <div class="tab">
    <cube-tab-bar
      :showSlider="true"
      v-model="selectedLabel"
      :data="tabs"
      :useTransition="false"
      ref="tabBar"
      class="border-bottom-1px">
    </cube-tab-bar>
    <div class="slide-wrapper">
      <cube-slide
        ref="slide"
        @change="onChange"
        @scroll="onScroll"
        :options="options"
        :showDots="false"
        :loop="false"
        :autoPlay="false"
        :initial-index="index">
        <cube-slide-item v-for="( tab , index ) in tabs" :key="index">
          <component :is="tab.component" :data="tab.data"></component>
        </cube-slide-item>
      </cube-slide>
    </div>
  </div>
</template>

<script>

export default {
  props: {
    tabs: {
      type: Array,
      default () {
        return []
      }
    }
  },
  data () {
    return {
      index: 0,
      options: {
        listenScroll: true,
        probeType: 3,
        directionLockThreshold: 0
      }
    }
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
      const tabWidth = this.$refs.tabBar.$el.clientWidth
      const scrollWidth = this.$refs.slide.slide.scrollerWidth
      const transform = -data.x / scrollWidth * tabWidth
      this.$refs.tabBar.setSliderTransform(transform)
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
