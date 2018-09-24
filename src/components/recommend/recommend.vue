<template>
  <div class="recommend">
    <div class="recommend-content">
      <div v-if="recommends.length" class="slider-wrapper">
        <g-slider>
          <div
            v-for="(item, index) in recommends"
            :key="index"
          >
            <a :href="item.linkUrl">
              <img :src="item.picUrl" alt="">
            </a>
          </div>
        </g-slider>
      </div>
      <div class="recommend-list">
        <h1 class="list-title">热门歌单推荐</h1>
        <ul>
          <li
            v-for="(item, index) in discList"
            :key="index"
            class="item"
          >
            <div class="icon"><img :src="item.imgurl" alt="" width="60" height="60"></div>
            <div class="text">
              <h2 class="name" v-html="item.creator.name">{{item}}</h2>
              <p class="desc" v-html="item.dissname">{{item}}</p>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import { getRecommend, getDiscList } from 'api/recommend'
import { ERROR_OK } from 'api/config'
import GSlider from 'base/slider/slider'

export default {
  name: 'Recommend',
  components: {
    GSlider
  },
  data () {
    return {
      recommends: [],
      discList: []
    }
  },
  created () {
    this._getRecommend()
    this._getDiscList()
  },
  methods: {
    _getDiscList () {
      getDiscList().then(res => {
        if (res.code === ERROR_OK) {
          this.discList = res.data.list
        }
      })
    },
    _getRecommend () {
      getRecommend().then(res => {
        if (res.code === ERROR_OK) {
          this.recommends = res.data.slider
        }
      })
    }
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
      .list-title
        // border 10px solid red
        height 65px
        line-height 65px
        text-align center
        font-size $font-size-medium
        color $color-theme
      .item
        // border 10px solid #fff
        display flex
        box-sizing border-box
        align-items center
        padding 0 20px 20px 20px
      .icon
        flex 0 0 60px
        width 60px
        padding-right 20px
      .text
        display flex
        flex-direction column
        justify-content center
        flex 1
        line-height 20px
        overflow hidden
        font-size $font-size-medium
        .name
          margin-bottom 10px
          color: $color-text
        .desc
          color: $color-text-d
</style>
