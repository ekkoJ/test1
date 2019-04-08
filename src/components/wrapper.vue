<template>
  <div class="wrapper">
    <div class="wrapper-slider">
      <div class="header-rule">
        <span
          class="cols"
          v-for="n in cols"
          :key="n"
        >
          {{ n }}
        </span>
      </div>
      <div class="points-wrapper" @mouseleave="handleMouse">
        <div
          class="rows"
          v-for="n in rows"
          :key="n"
        >
          <div
            v-for="col in cols"
            :key="col"
            :class="['points cols', { 'active': n === activePoint.row && col === activePoint.col }]"
            @mouseenter="handleMouse(n, col)"
          >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'wrapper',
  data () {
    return {
      rows: 10,
      cols: 40,
      activePoint: {
        row: -1,
        col: -1
      }
    }
  },
  methods: {
    handleMouse (row, col) {
      this.activePoint.row = row || -1
      this.activePoint.col = col || -1
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
pointSize = 5px
wrapperSize = 60px
.wrapper
  overflow hidden
  white-space nowrap
  width 90%
  display block
  margin-left 2%
  // padding 0 50px
  .cols
    display inline-block
    width wrapperSize
    height wrapperSize
    text-align center
    color #fff
  .rows
    line-height inherit
    font-size 0
  .points
    display inline-flex
    justify-content center
    flex-direction column
    align-items center
    // justify-content center
    &:after
      display inline-block
      content ""
      width pointSize
      height pointSize
      border-radius 50%
      background #fff
    &.active
      background rgba(0, 0, 0, 0.2)
      &:after
        background red
</style>
