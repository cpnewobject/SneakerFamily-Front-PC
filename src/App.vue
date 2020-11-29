<template>
  <div id="app">
    <system-header></system-header>
    <router-view></router-view>
    <system-footer></system-footer>
  </div>
</template>

<script>
import Header from '@/components/Header.vue'
import Footer from '@/components/Footer.vue'
export default {
  name: 'app',
  components: {
    'system-header': Header,
    'system-footer': Footer
  }
}
</script>

<style lang="scss">
  @import "assets/layui/css/layui.css";
  @import "assets/css/global.css";
  @import "assets/layui/css/modules/layer/default/layer.css";
</style>
