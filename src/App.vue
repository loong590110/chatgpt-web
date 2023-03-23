<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="28" height="28" />

    <div>
      <HelloWorld msg="用户名" />
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  flex-basis: 260px;
  height: 100vh;
  line-height: 1.5;
}

.logo {
  float: left;
  margin-left: 2rem;
  margin-right: 0.5rem;
}
</style>
