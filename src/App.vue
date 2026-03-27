<script setup>
import HousewarmingInvitation from './components/HousewarmingInvitation.vue'
</script>

<template>
  <div class="app">
    <HousewarmingInvitation />
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html, body {
  height: 100vh;
  overflow: hidden;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
    Ubuntu, Cantarell, 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
    'Microsoft YaHei', 'PingFang SC', 'Hiragino Sans GB', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.app {
  width: 100%;
  height: 100vh;
}

#app {
  width: 100%;
  height: 100vh;
}
</style>
