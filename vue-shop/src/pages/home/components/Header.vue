<template>
  <div class="header">
    <div class="header-left">
      <div class="letter">分类</div>
      <span class="iconfont icon-choose">&#xe652;</span>
    </div>
    <div class="header-input">
      <span class="iconfont icon-select">&#xe632;</span>
      珠宝超品满399减200</div>
      <router-link to="/city">
    <div class="header-right">武汉
      <span class="iconfont">&#xe64e;</span>
      </div>
      </router-link>
  </div>
</template>
<script>
export default {
  name: 'HomeHeader',
  props: {
    city: String
  }
}
</script>
<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .header
    display: flex
    line-height 1rem
    background: $bgColor
    color: #fff
    .header-left
      position relative
      width: .64rem
      float: left
      margin-top -0.1rem
      .letter
        position absolute
        margin-top .3rem
      .icon-choose
        margin-bottom .3rem
        font-size: .4rem
    .header-input
      flex:1
      height .64rem
      line-height .64rem
      margin-top .12rem
      padding-left .2rem
      margin-left: .2rem
      background: #fff
      color: #333
      border-radius .4rem
      .icon-select
       text-align: center
       font-size: .4rem
    .header-right
      min-width: 1.04rem
      float: right
      text-align: center
      color: #fff
      .arrow-icon
        margin-left: -0.4rem
        font-size: .24rem
</style>
