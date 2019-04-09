<template>
  <div class="test1">
    <div class="left">
      <div
        class="blocks"
        v-for="com in coms"
        :key="com"
        @mousedown="el => dragStart(el, com)"
      >
        {{ com }}
      </div>
    </div>
    <div class="wrapper">
      <wrapper ref="wrapper"></wrapper>
    </div>
    <div
      class="active-block"
      v-if="activeComs"
      :style="{
        top: dragOffset.y + 'px',
        left: dragOffset.x + 'px'
      }"
    >
      {{ activeComs }}
    </div>
  </div>
</template>

<script>
import wrapper from '@/components/wrapper'
export default {
  data () {
    return {
      coms: ['com1', 'com2', 'com3', 'com4', 'com5'],
      activeComs: '',
      dragOffset: {
        x: -1,
        y: -1
      }
    }
  },
  components: {
    wrapper
  },
  mounted () {
    let self = this
    document.addEventListener('mouseup', () => {
      self.$refs.wrapper.showBlock(self.activeComs)
      self.activeComs = ''
    })
    document.addEventListener('mousemove', self.draging)
  },
  watch: {
    activeComs (val) {
      // if (!val) {
      //   document.removeEventListener('onmousemove')
      //   return
      // }
      // let self = this
      // document.addEventListener('onmousemove', el => self.draging(el))
    }
  },
  destroyed () {
    document.removeEventListener('mouseup', () => {
      self.activeComs = ''
    })
  },
  methods: {
    dragStart (el, com) {
      this.activeComs = com
      this.dragOffset.x = el.target.offsetLeft
      this.dragOffset.y = el.target.offsetTop
    },
    draging (el) {
      if (!this.activeComs) return
      this.dragOffset.x = el.pageX - 30
      this.dragOffset.y = el.pageY - 30
    }
  }
}
</script>

<style lang="stylus" scoped>
blockSize = 60px
.test1
  display flex
  .left
    flex 0 0 200px
    height 100vh
    background #000
    .blocks
      width blockSize
      height blockSize
      color #fff
      font-size 12px
      text-align center
      &:hover
        color red
  .wrapper
    flex 1
    overflow hidden
    background #333
  .active-block
    z-index 1
    width blockSize
    height blockSize
    color red
    border 1px solid red
    font-size 12px
    text-align center
    box-sizing border-box
    position absolute
    top 0
    left 0
</style>
