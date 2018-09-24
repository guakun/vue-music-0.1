<template>
  <div class="slider" ref="slider">
    <div class="slider-group" ref="sliderGroup">
      <slot></slot>
    </div>
    <div class="dots"></div>
  </div>
</template>

<script>
import { addClass } from 'common/js/dom'
import BScroll from 'better-scroll'

export default {
  name: 'MySlider',
  props: {
    loop: {
      type: Boolean,
      default: true
    },
    autoPlay: {
      type: Boolean,
      default: true
    },
    interval: {
      type: Number,
      default: 3000
    }
  },
  mounted () {
    setTimeout(() => {
      this._setSliderWidth()
      this._initSlider()
    }, 20)
  },
  methods: {
    _setSliderWidth () {
      this.children = this.$refs.sliderGroup.children
      let width = 0
      let sliderWidth = this.$refs.slider.clientWidth
      for (let i = 0; i < this.children.length; i++) {
        let child = this.children[i]
        addClass(child, 'slider-item')

        child.style.width = sliderWidth + 'px'
        width += sliderWidth
      }

      if (this.loop) {
        width += sliderWidth * 2
      }
      this.$refs.sliderGroup.style.width = width + 'px'
    },
    _initSlider () {
      this.slider = new BScroll(this.$refs.slider, {
        scrollX: true,
        scrollY: false,
        momentum: false,
        snap: true,
        snapLoop: this.loop,
        snapThreshold: 0.3,
        snapSpeed: 400,
        click: true
      })
    }
  }
}
</script>

<style lang="stylus" scoped>
@import "~common/stylus/variable"
.slider-group
  overflow hidden
  white-space nowrap
  .slider-item
    float left
    box-sizing border-box
    overflow hidden
    text-align center
    a
      display block
      width 100%
      overflow hidden
      text-decoration none
    img
      display block
      width 100%


</style>
