<template>
  <div>
    <div class="title">推荐页</div>
    <ul>
      <router-link tag="li"
      class="item border-bottom"
      v-for="item of list"
      :key="item.id"
      :to="'/detail/' + item.id"
      >
          <img class="item-img" :src="item.imgUrl">
        <div class="item-info">
          <p class="item-title">{{item.title}}</p>
          <p class="item-desc">{{item.desc}}</p>
          <button class="item-button">查看详情</button>
        </div>
      </router-link>
    </ul>
  </div>
</template>
<script>
export default {
  name: 'HomeRecommend',
  props: {
    list: Array
  }
}
</script>
<style lang="stylus" scoped>
 @import '~styles/mixins.styl'
  .title
    margin-top: .2rem
    line-height: .8rem
    background: #eee
    text-indet: .2rem
  .item
    overflow :hidden
    display: flex
    height: 1.9rem
    bottom 0.1rem
    .item-img
      overflow: hidden
      width: 1.7rem
      height: 1.7rem
      padding: .1rem
    .item-info
      flex:1
      padding: .1rem
      min-width: 0
      .item-title
        font-size: .32rem
        line-height: 0.54rem;
        font-weight: 600;
        ellipsis()
      .item-desc
        line-height: .4rem
        color: #ccc
        ellipsis()
      .item-button
        line-height: .44rem
        background: #ff9300
        margin-top : .16rem
        padding: 0.2rem
        border-radius: .06rem
        color: #fff
</style>
