<template>
  <div class="header">
    城市列表
    <router-link to="/">
      <div class="iconfont icon-right">&#xe624;</div>
      <div class="back">返回</div>
    </router-link>
  </div>
</template>
<script>
export default {
  name: 'cityheader'
}
</script>
<style lang="stylus" scoped>
  @import "~styles/varibles.styl"
  .header
    position relative
    overflow hidden
    height:$headerHeight
    line-height: $headerHeight
    text-align center
    background $bgColor
    font-size .32rem
    color #fff
    .icon-right
      position absolute
      left 0
      top 0
      width .64rem
      text-align center
      font-size .12rem
      color #fff
    .back
      position absolute
      left .45rem
      top 0
      margin-top 0.02rem
      font-size .32rem
      text-align center
      color #fff
</style>
