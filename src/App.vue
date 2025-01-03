<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <header>
    <div class="wrapper">
      qNote
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 1000;

  align-self: flex-start;
}

main {
  height: 100%;
  width: 100vw;
  display: flex;
  justify-content: center;
  grid-row: 2;
}
</style>
