<template>
  <div id="app">
    <img class="bg-img" src="http://wx4.sinaimg.cn/large/d8eedf34gy1fxelf4x3fkj212w0px4qq.jpg">
    <sketchpad></sketchpad>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Sketchpad from './components/Sketchpad.vue';

export default Vue.extend({
  name: 'app',
  components: {
    Sketchpad,
  },
});
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.bg-img {
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
}
</style>
