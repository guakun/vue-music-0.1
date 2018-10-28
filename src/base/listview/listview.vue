<template>
  <scroll class="listview" :data="data" ref="listview" :listenScroll="listenScroll" @scroll="scroll">
    <ul>
      <li v-for="(group, index) in data" class="list-group" :key="index" ref="listGroup">
        <h2 class="list-group-title">{{group.title}}</h2>
        <ul>
          <li v-for="(item, index) in group.items" class="list-group-item" :key="index">
            <img class="avatar" :src="item.avatar" alt="我是一张头像咯">
            <span class="name">{{item.name}}</span>
          </li>
        </ul>
      </li>
    </ul>
    <div class="list-shortcut" @touchstart="onShortcutTouchStart" @touchmove.stop.prevent="onShortcutTouchMove">
      <ul>
        <li v-for="(item, index) in shortcutList" class="item" :data-index="index" :key="item">{{item}}</li>
      </ul>
    </div>
  </scroll>
</template>

<script>
import Scroll from 'base/scroll/scroll'
import { getData } from 'common/js/dom'

const ANCHOR_HEIGHT = 18

export default {
  name: 'ListView',
  components: {
    Scroll
  },
  props: {
    data: {
      type: Array,
      default: () => []
    }
  },
  computed: {
    shortcutList () {
      return this.data.map((group) => {
        return group.title.substr(0, 1)
      })
    }
  },
  created () {
    this.touch = {},
    this.listenScroll = true
  },
  methods: {
    scroll (pos) {
      console.log('pos', pos)
    },
    onShortcutTouchMove (e) {
      let firstTouch = e.touches[0]
      this.touch.y2 = firstTouch.pageY
      let delta = ( this.touch.y2 - this.touch.y1 ) / ANCHOR_HEIGHT | 0
      let anchorIndex = this.touch.anchorIndex + delta - 0
      this._scrollTo(anchorIndex)
    },
    onShortcutTouchStart (e) {
      let anchorIndex = getData(e.target, 'index')
      let firstTouch = e.touches[0]
      this.touch.y1 = firstTouch.pageY
      this.touch.anchorIndex = anchorIndex
      this._scrollTo(anchorIndex)
    },
    _scrollTo (index) {
      this.$refs.listview.scrollToElement(this.$refs.listGroup[index], 0)
    }
  }
}
</script>

<style lang="stylus" scoped>
@import "~common/stylus/variable"

.listview
  position relative
  width 100%
  height 100%
  overflow hidden
  background $color-background
  .list-group
    padding-bottom 30px
    .list-group-title
     height 30px
     line-height 30px
     padding-left 20px
     font-size $font-size-small
     color: $color-text-l
     background $color-highlight-background
    .list-group-item
      display flex
      align-items center
      padding 20px 0 0 30px
      .avatar
        width 50px
        height 50px
        border-radius 50%
      .name
        margin-left 20px
        color $color-text-l
        font-size $font-size-medium
  .list-shortcut
    // border 1px solid red
    position absolute
    right 0
    top 50%
    transform translateY(-50%)
    width 20px
    padding 20px 0
    border-radius 10px
    background $color-background-d
    text-align center
    font-family Helvetica
    .item
      padding 3px
      line-height 1
      color $color-text-l
      font-size $font-size-small
      &.current
        color $color-theme
</style>
