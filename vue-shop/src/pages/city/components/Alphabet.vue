<template>
  <ul class="list">
    <li
      class="item"
      v-for="item of letters"
      :key="item"
      :ref="item"
      @touchstart.prevent="handleTouchStart"
      @touchmove="handleTouchMove"
      @touchend="handleTouchEnd"
      @click="handleLetterClick"
    >
      {{item}}
    </li>
  </ul>
</template>

<script>
export default {
  name: 'CityAlphabet',
  props: {
    cities: Object
  },
  computed: {
    letters () {
      const letters = []
      for (let i in this.cities) {
        letters.push(i)
      }
      return letters
    }
  },
  data () {
    return {
      touchStatus: false,
      startY: 0,
      timer: null
    }
  },
  updated () {
    // 函数节流
    this.startY = this.$refs['A'][0].offsetTop
  },
  methods: {
    // 实现点击字母跳转list的事件，首先@click事件绑定到字母点击上，然后用方法
    // 把点击的letter传回给city主组件，然后再通过绑定该数据向list中传送，在list中
    // 设置一个监听器watch，同时绑定area区域ref，操作bs-scroll来操作
    handleLetterClick (e) {
      this.$emit('change', e.target.innerText)
    },
    // 实现滚动的功能,首先算出a距离顶部的距离
    // ，在算当前距离顶部的距离，这个差值得出来后再除以每个字母的高度，就能得到是哪个字母了
    handleTouchStart () {
      this.touchStatus = true
    },
    handleTouchMove (e) {
      if (this.touchStatus) {
        if (this.timer) {
          clearTimeout(this.timer)
        }
        this.timer = setTimeout(() => {
          // Touches[0]是手指触碰的位置,79是offsettop高度
          const touchY = e.touches[0].clientY - 79
          const index = Math.floor((touchY - this.startY) / 20)
          if (index >= 0 && index < this.letters.length) {
            this.$emit('change', this.letters[index])
          }
        }, 16)
      }
    },
    handleTouchEnd () {
      this.touchStatus = false
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .list
    display: flex
    flex-direction: column
    justify-content: center
    position: absolute
    top: 1.58rem
    right: 0
    bottom: 0
    width: .4rem
    .item
      line-height: .4rem
      text-align: center
      color: $bgColor
</style>
