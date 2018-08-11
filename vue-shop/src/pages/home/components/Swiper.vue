<template>
  <div class="wrapper">
    <!-- 用slide来循环输出 -->
    <swiper :options="swiperOption" v-if="showSwiper">
    <swiper-slide v-for="item of list" :key="item.id">
      <img class= "swiper-img" :src="item.imgUrl" alt=""></swiper-slide>
    <div class="swiper-pagination"  slot="pagination"></div>
  </swiper>
  </div>
</template>
<script>
export default {
  name: 'HomeSwiper',
  props: {
    list: Array
  },
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        // slide里面循环的是slot插值里面的页面，设置一直循环
        loop: true
      }
    }
  },
  computed: {
    showSwiper () {
      // 因为一进来接受的是个空数组，所以用v-if判断，当list存在的时候才渲染轮播图
      return this.list.length
    }
  }
}
</script>
<style lang="stylus" scoped>
  // 让wrapper下面的这个子元素穿透scoped
  .wrapper >>> .swiper-pagination-bullet-active
    background #fff
  .wrapper
    overflow hidden
    width:100%
    height:0
    padding-bottom 49.1%
  .swiper-img
    width:100%
</style>
