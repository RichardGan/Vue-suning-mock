<template>
  <div>
    <div class="search">
      <!-- 设置keyword -->
      <input v-model="keyword" class="search-input" type="text" placeholder="输入城市名或拼音" />
    </div>
    <!-- 让其搜出的值进行滚动 -->
    <div
      class="search-content"
      ref="search"
      v-show="keyword"
    >
      <ul>
        <li
          class="search-item border-bottom"
          v-for="item of list"
          :key="item.id"
          @click="handleCityClick(item.name)"
        >
          {{item.name}}
        </li>
        <li class="search-item border-bottom" v-show="hasNoData">
          没有找到匹配数据
        </li>
      </ul>
    </div>
  </div>
</template>

<script>

import Bscroll from 'better-scroll'
import { mapMutations } from 'vuex'
export default {
  name: 'CitySearch',
  props: {
    cities: Object
  },
  data () {
    return {
      // 设置keyword
      keyword: '',
      list: [],
      timer: null
    }
  },
  computed: {
    // 没找到的话就不显示
    hasNoData () {
      return !this.list.length
    }
  },
  // 监听传过来的keyword
  watch: {
    keyword () {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      // 删除数据或者没有数据时，显示空数据框
      if (!this.keyword) {
        this.list = []
        return
      }
      this.timer = setTimeout(() => {
        // 定义result
        const result = []
        // 在city主组件传过来的json中遍历，查找每一个值，若json中数据的spell和name相等
        // 那么就把这个值push进result，然后传给list让他显示出来

        for (let i in this.cities) {
          this.cities[i].forEach((value) => {
            if (value.spell.indexOf(this.keyword) > -1 || value.name.indexOf(this.keyword) > -1) {
              result.push(value)
            }
          })
        }
        this.list = result
      }, 100)
    }
  },
  methods: {
    // 点击city，跳转页面，这个是是在vuex里面定义的
    handleCityClick (city) {
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.search)
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .search
    height: .72rem
    padding: 0 .1rem
    background: $bgColor
    .search-input
      box-sizing: border-box
      width: 100%
      height: .62rem
      padding: 0 .1rem
      line-height: .62rem
      text-align: center
      border-radius: .06rem
      color: #666
  .search-content
    z-index: 1
    overflow: hidden
    position: absolute
    top: 1.58rem
    left: 0
    right: 0
    bottom: 0
    background: #eee
    .search-item
      line-height: .62rem
      padding-left: .2rem
      background: #fff
      color: #666
</style>
