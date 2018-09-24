<template>
  <div id="app">
    <my-header></my-header>
    <my-tab></my-tab>
    <keep-alive>
      <router-view></router-view>
    </keep-alive>
  </div>
</template>

<script>
import MyHeader from 'components/m-header/m-header'
import MyTab from 'components/tab/tab'
export default {
  name: 'App',
  components: {
    MyHeader,
    MyTab
  }
}
</script>

<style lang="stylus" scoped>
@import "common/stylus/variable";
</style>
