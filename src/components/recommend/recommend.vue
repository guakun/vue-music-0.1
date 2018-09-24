<template>
  <div class="recommend">
    <div class="recommend-content">
      <div class="slider-wrapper"></div>
      <div class="recommend-list">
        <h1 class="list-title">热门歌单推荐</h1>
        <ul></ul>
      </div>
    </div>
  </div>
</template>

<script>
import { getRecommend } from 'api/recommend'
export default {
  name: 'Recommend',
  created () {
    console.log('hello')
  }
}
</script>

<style lang="stylus" scoped>
@import "~common/stylus/variable";
.recommend
  position fixed
  width 100%
  top 88px
  bottom 0
  .recommend-content
    height 100%
    overflow hidden
    .slider-wrapper
      position relative
      overflow hidden
    .recommend-list
      // border 10px solid #fff
      .list-title
        // border 10px solid red
        height 65px
        line-height 65px
        text-align center
        font-size $font-size-medium
        color $color-theme
        // padding 0 20px 20px 20px
</style>
