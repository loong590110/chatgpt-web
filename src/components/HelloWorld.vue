<script setup>
defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h3 style="margin-left: 30px;">VIP过期: 2023-6-6</h3>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 1.5rem;
  top: -5px;
}

h3 {
  font-size: 0.9rem;
}

.greetings h1,
.greetings h3 {
  text-align: left;
}
</style>
