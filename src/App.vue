<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <InfoList />
  </div>
</template>

<script>
import test from 'node:test';
import InfoList from './components/InfoList.vue'

export default {
  name: 'App',
  components: {
    InfoList
  },
  methods() {
    //测试
  } //测试冲突
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center;
  color: #2c3e50;
  margin-top: 60px; */
}
</style>
