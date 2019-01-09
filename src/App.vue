<template>
  <div id="app">
    <img class="bg-img" src="http://5b0988e595225.cdn.sohucs.com/images/20181212/da40e0fca16e4441a52654a14140801a.jpeg">
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
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
}
</style>
