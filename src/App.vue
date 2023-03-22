<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="28" height="28" />

    <div>
      <HelloWorld msg="用户名" />
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
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

nav {
  width: 100%;
  font-size: 16px;
  margin-top: 2rem;
  margin-left: 1rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}
</style>
