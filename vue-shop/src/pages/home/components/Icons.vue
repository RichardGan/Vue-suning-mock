<template>
<div class="icons">
  <swiper :options="swiperOption">
    <!--用swiper来循环输出图标 -->
    <swiper-slide v-for="(page, index) of pages" :key="index">
    <div class="icon" v-for="item of page" :key="item.id">
      <div class="icon-img">
      <img  class="icon-img-content" :src='item.imgUrl'>
      </div>
      <p class="icon-desc">{{item.desc}}</p>
    </div>
    </swiper-slide>
  </swiper>
</div>
</template>
<script>
export default {
  name: 'icons',
  props: {
    list: Array
  },
  data () {
    return {
    // 图标设置成不自动滚动
      swiperOption: {
        autoplay: false
      }
    }
  },
  computed: {
  // 计算页数，在一页上若有9个图标，用pages代表页数，0-7用math.floor来取1，然后一个接一个把page推进pages里面
    pages () {
      const pages = []
      this.list.forEach((item, index) => {
        const page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(item)
      })
      return pages
    }
  }
}
</script>
<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .icons >>> .swiper-container
    height 0
    padding-bottom 50%
  .icons
    margin-top .1rem
    .icon
      float left
      position relative
      overflow hidden
      width 25%
      height 0
      padding-bottom 25%
      .icon-img
        position absolute
        top 0
        left 0
        right 0
        bottom .44rem
        box-sizing border-box
        padding .1rem
        .icon-img-content
          height: 100%
          display block
          margin 0 auto
      .icon-desc
        position absolute
        left 0
        right 0
        bottom 0
        line-height .44rem
        text-align center
        height .44rem
        color $textColor
</style>
