<template>
  <div id="app">
    <my-header></my-header>
    <router-view></router-view>
  </div>
</template>

<script>
import MyHeader from 'components/m-header/m-header'
export default {
  name: 'App',
  components: {
    MyHeader
  }
}
</script>

<style lang="stylus" scoped>
@import "common/stylus/variable";
</style>
